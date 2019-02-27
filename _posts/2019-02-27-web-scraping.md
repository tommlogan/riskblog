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
Go ahead and install the `requests` and `beautifulsoup` packages with:
`pip install requests bs4`

# To be continued
