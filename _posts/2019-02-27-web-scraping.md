---
layout: post
title:  Introduction to web scraping
author: Tom Logan
excerpt: There's so much data being produced and presented online, but often it vanishes as quickly as it arrives. Here's a quick guide and example to how to record it.
date:   2019-02-27
categories: research-practice coding
comments: true
toc: true
---

I have been asked to host a tutorial on web scraping for my research group. I figured I'd blog it so that it can be a reference in the future as well.


# GitHub
I'm not going to extol the virtues of GitHub, but rather assume that everyone is using it (or GitLab etc.).  
In your online account: create the repository, set up a .gitignore, and then clone it into the folder (in the parent folder of your project - i.e. if you want your `scraper` directory to be within `research`, be in the `research` folder when you clone.  

If you are unfamiliar with Git, check out the PowerPoint downloadable from my earlier [blog.](/research-practice/coding/2018/better-coding-practices/)

# Directory structure
Once your directory has been cloned, add the structure  

    |- <your project name>/
        |- .git (should be here already)
        |- .gitignore (should be here already)
        |- _scratch_/
        |- data/
        |- src/ (where the code will go)

# Code editor
I suggest working in Atom (because of it's Git integration). But Sublime or others are also good.

# Virtual Environment
My example will be for scraping in Python, so, as with any Python coding project, we'll be working in a virtual environment.  
Create one in the highest level of your project's directory.
That is, in the code terminal you're using (OS dependent)
0. (if you haven't already you'll need to install the ability to create virtual environments: `pip install virtualenv`)
1. cd to your project's directory.
2. `python3 -m virtualenv venv` or `python -m virtualenv venv`  

This will add `venv` directory into your project directory.
Remember to add `venv/` to the .gitignore file (this is easy in most code editors).  
Now Git commit.

# Prepare the virtual environment
There are a couple of packages that we will use to perform the web scraping, so install them into your virtual environment.
The first step to doing this is to `activate` the virtual environment.
To do this, type into your terminal (once you're in the project directory):  
Mac/Linux: `source venv/bin/activate`  
Windows: `venv\Scripts\activate`  
The result should be a `(venv)` showing on the left on your terminal active line.

We can now install packages into the virtual environment without administrator privileges.  
Go ahead and install the `requests`, `beautifulsoup`, and `schedule` packages with:
`pip install requests bs4 schedule`

# Scraping
The first example is scraping a website, this is most general.

## Power outage scraping
Let's scrape the electricity outages for the counties served by BGE.  
Open the BGE site that has these outages: https://outagemap.bge.com/

The irritating thing with many of these websites is how often they change, so I'll provide a generally description so (a) it's extendable to other sites, and (b) this tutorial isn't made completely redundant when they next update their website.

The aim here is to regularly record the number of customers in each county without power. So the first step is to find that information on the site.
In this case, this is available on the left hand side of the screen, click `summary` and then `Outages by County`. The result is a tabular popup that lists the information.

<img class="image" src="/assets/blog/2019-02-27-web-scraping/outages_gui.PNG" width="40%">

The next step is to figure out where that information is stored by the website. Most websites are comprised of data and code that formats and displays that data. We need to figure out where and how that data is stored. To look under-the-hood of the website we need to `Inspect` it (Chrome Windows: `Crtl+Shift+I`; Safari Mac: `Command+Option+i` - or Google the command for your browser and OS.) Once the inspector is open, refresh the page.

<img class="image" src="/assets/blog/2019-02-27-web-scraping/inspector.PNG" width="100%">

Now we need to find the data within this list of files. Often, and in this case, it's a .js file. For data such as this, it comes with a timestamp. Because of variation between websites, you need to search this list and look at the result in the box. Practice, and getting a feel for what you're looking for, makes this process faster.

<img class="image" src="/assets/blog/2019-02-27-web-scraping/outages_inspector.PNG" width="80%">

Now that you've found the information in the website that you want, you need to figure out how to access it. Right click on the name (in this case `report.js?timestamp=1551...` etc) and click `Open in new tab`. This is the text that we'll be downloading. (I can't stress enough, that websites are different and some will simply not let you do this. In those cases it does not mean that they cannot be scraped - but you need to dig more to figure out how. The ones that provide data in these json/js formats are ideal, but there are other formats that can be scraped.)
Now copy the URL: e.g. `https://s3.amazonaws.com/outagemap.bge.com/data/interval_generation_data/2019_02_28_12_26_08/report.js?timestamp=1551374668531`
(you can actually drop the info after the timestamp).

For this website, there's one more thing you need from the website and then we can turn to the code. That's where the datetime stamp is stored. We know what the URL is, but the datetime stamp is a variable and that comes from the website. Go back to the inspector and find where that datetime information is. In this case it is in metadata.xml

<img class="image" src="/assets/blog/2019-02-27-web-scraping/metadata.PNG" width="80%">

So, following the same steps, we can get the URL as: `https://s3.amazonaws.com/outagemap.bge.com/data/alerts/metadata.xml`
which is kindly datetime independent.

Now over to the code.

I recommend the structure of this code be along the lines of:
1. wrapper function that runs every x minutes.
2. function that scrapes and returns the data
3. function that writes to a text file or, preferably, a database.


### Scheduler
This is the basic code for a scheduler.

{% highlight python %}
```
import time
from datetime import datetime
import schedule

def main():
    '''
    creates an infinite loop and calls the scraper functions
    '''
    # if you were to initiate a database, now's a good time.

    # how long between scraping?
    minutes_between_scraping = 15 # minutes

    # this try/except loop is a good way to document errors
    try:
        # in this case "scraper_function" is the name of your scraper function
        schedule.every(1).minutes.do(scraper_function)
        # this is the infinite while loop
        while True:
            # you can change the unit of time here
            scrape_time = (time.localtime().tm_min%minutes_between_scraping==0)
            if scrape_time:
                # runs the scraper
                schedule.run_pending()
    except Exception as e:
        # log when there is an error -> see my previous blog with some brief intro to logging
        # e.g. log_error(e)
        # or just print an error
        print(e)
```
{% endhighlight %}

### Scraper code
First off, let's see if we can scrape that URL you found earlier.
Try: `content = requests.get(url).content`  
Now print `content` and see that it prints what you saw on the browser.

So here is an example of a scraping function.

We first get the datetime stamp, then update the data's URL so that we can download that. Finally we decode that data into a dictionary so we can access the data next.

{% highlight python %}
```
from bs4 import BeautifulSoup
import json
import requests

def scraper_function():

  metadata_url = 'https://s3.amazonaws.com/outagemap.bge.com/data/alerts/metadata.xml'
  # datetime of the latest report, which is reported in a metadata file.
  content = requests.get(metadata_url).content

  # Pull the date out of the xml file, should look like "2015_03_02_20_17_31"
  # Beauftifulsoup lets you find things in xml and html documents
  soup = BeautifulSoup(content, "html.parser")
  last_report_datetime = soup.find('root').find('directory').text

  # now update the report_url
  report_url = 'https://s3.amazonaws.com/outagemap.bge.com/data/interval_generation_data/{}/report.js'

  report_url = report_url.format(last_report_datetime)

  # now pull the content
  content = requests.get(report_url).content

  # decode the json data into a dictionary
  data_dict = json.loads(content.decode())

  write_data(data_dict)
```
{% endhighlight %}

Note that the last line calls a function `write_data`, so we need to figure this out!

### Storing data
An essential element of this is how you're storing storing this data.
I thoroughly recommend InfluxDB as it is a temporal database with great documentation. But that's for another time. So for now, we'll store it in a text file. But what is the structure of the data? Every data set is different and considering its future use is critical to how it is stored.

It would be easy to store the data with each row being a timestamp. But I think there are better ways. Instead, let's store each county outage as a row. That means that each timestamp will be repeated. Doing this means we can quickly filter by county, time, number of customers out etc.

That is, the data structure I suggest we use is:
```
datetime | county_name | custs_out | custs_total | provider
```
`Provider` is optional here and would come in handy if you were to have a single dataset for multiple utilities.

So, back to the code.

Look at the format of the data in `data_dict`.  
This is a dictionary in Python. This becomes very useful as we can access the different components.
Print `data_dict` and look at the keys. The county data is actually a list of dictionaries stored here: `data_dict['file_data']['curr_custs_aff']['areas'][0]['areas']`  
So what we'll do is loop through these and write them to rows in the textfile/database.

{% highlight python %}
```
import csv

def write_data(data_dict):

  # init the list of dictionaries that we will then write to the txtfile/db
  outages = []

  # loop through the rows in the data list
  data_list = data_dict['file_data']['curr_custs_aff']['areas'][0]['areas']
  for row in data_list:
      # add to outage dictionary
      outage = {
          "time": str(datetime.now()),
          "utility" : company_name,
          "county": row['area_name'],
          "custs_out": row['custs_out'],
          "custs_total": row['total_custs'],
          }
      outages.append(outage)

  # now write to the textfile or database
  filename = 'data/outages.csv'
  # check that the file exists
  file_exists = os.path.exists(filename)
  keys = outages[0].keys()
  if not file_exists:
      # if the file doesn't exist, write the header row
      with open(filename, 'w', newline='') as f:
          dict_writer = csv.DictWriter(f, keys)
          dict_writer.writeheader()
  # if the file does exist, open and append the results
  with open(filename, 'a', newline='') as f:
      dict_writer = csv.DictWriter(f, keys)
      dict_writer.writerows(outages)

```
{% endhighlight %}

# Putting it all together

And this should be all you need. Save this as something like `elect_scraper.py` and from the terminal, in the upper level of this directory, you can run it with `python src/elect_scraper.py` and it'll save data into the `data/` folder.

{% highlight python %}
```
import csv
from bs4 import BeautifulSoup
import json
import requests
import time
from datetime import datetime
import schedule

def main():
    '''
    Create an infinite loop and call the scraper function(s)
    '''
    # if you were to initiate a database, now's a good time.

    # how long between scraping?
    minutes_between_scraping = 15 # minutes

    # this try/except loop is a good way to document errors
    try:
        # in this case "scraper_function" is the name of your scraper function
        schedule.every(1).minutes.do(scraper_function)
        # this is the infinite while loop
        while True:
            # you can change the unit of time here
            scrape_time = (time.localtime().tm_min%minutes_between_scraping==0)
            if scrape_time:
                # runs the scraper
                schedule.run_pending()
    except Exception as e:
        # log when there is an error -> see my previous blog with some brief intro to logging
        # e.g. log_error(e)
        # or just print an error
        print(e)


def scraper_function():
  '''
    Scrape the website data
  '''

  metadata_url = 'https://s3.amazonaws.com/outagemap.bge.com/data/alerts/metadata.xml'
  # datetime of the latest report, which is reported in a metadata file.
  content = requests.get(metadata_url).content

  # Pull the date out of the xml file, should look like "2015_03_02_20_17_31"
  # Beauftifulsoup lets you find things in xml and html documents
  soup = BeautifulSoup(content, "html.parser")
  last_report_datetime = soup.find('root').find('directory').text

  # now update the report_url
  report_url = 'https://s3.amazonaws.com/outagemap.bge.com/data/interval_generation_data/{}/report.js'

  report_url = report_url.format(last_report_datetime)

  # now pull the content
  content = requests.get(report_url).content

  # decode the json data into a dictionary
  data_dict = json.loads(content.decode())

  write_data(data_dict)


def write_data(data_dict):
  '''
    Write the data to a csv or a database
  '''
  # init the list of dictionaries that we will then write to the txtfile/db
  outages = []

  # loop through the rows in the data list
  data_list = data_dict['file_data']['curr_custs_aff']['areas'][0]['areas']
  for row in data_list:
      # add to outage dictionary
      outage = {
          "time": str(datetime.now()),
          "utility" : company_name,
          "county": row['area_name'],
          "custs_out": row['custs_out'],
          "custs_total": row['total_custs'],
          }
      outages.append(outage)

  # now write to the textfile or database
  filename = 'data/outages.csv'
  # check that the file exists
  file_exists = os.path.exists(filename)
  keys = outages[0].keys()
  if not file_exists:
      # if the file doesn't exist, write the header row
      with open(filename, 'w', newline='') as f:
          dict_writer = csv.DictWriter(f, keys)
          dict_writer.writeheader()
  # if the file does exist, open and append the results
  with open(filename, 'a', newline='') as f:
      dict_writer = csv.DictWriter(f, keys)
      dict_writer.writerows(outages)


if __name__ == '__main__':
    # run the scraper
    main()

```
{% endhighlight %}
