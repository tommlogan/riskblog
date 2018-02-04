---
layout: post
title:  Better Coding Practice
author: Tom Logan
excerpt: Have you ever had to revisit a coding project? If you're like me, there's a sense of trepidation. Will I remember what I was doing? Will it still work?  Here are some techniques that may make you a happier and more efficient researcher.
date:   2018-01-31
categories: research-practice
comments: true
toc: true
---

Have you ever had to revisit a coding project? If you're like me, there's a sense of trepidation. Will I remember what I was doing? Will it still work?  
They say that your closest collaborator is your past self, except she/he doesn't respond to emails...

Well, I got a bit sick of that feeling and have learnt some techniques which my future self will be thankful for. And that's what I want to share with you. Note that many of these are adapted from [Jeff Leek's book, *How to be a Modern Scientist*](http://jtleek.com/book/).  

Also, I believe that these skills are an essential thing to learn, whether we plan on becoming academics, valley entrepreneurs, or other consultants - the internet is not going anyway, we will be collaborating in teams on code, and preparing ourselves for this is only to our advantage.

# Workshop and slides
I'm presenting a workshop for the INFORMS student chapter at the University of Michigan (Institute of Operations Research and Management Science) and the slides are available [here.](https://www.slideshare.net/TomLogan12/better-coding-practice)
<iframe src="https://www.slideshare.net/TomLogan12/slideshelf" width="615px" height="470px" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:none;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe>
# GitHub
Version control is essential. It is essential for research projects and any collaborative project.
Version control time stamps every change you or someone else makes on a project.
This means that you can return

# Directory structure
    |- <your project name>/
    |- .git
    |- \_scratch/
    |- data/
        |- raw/
        |- processed/
    |- fig/
        |- exploratory/
        |- final/
    |- report/
    |- code/ (or src)
    (e.g. the sub folders are project specific)
        |- processing/ or data_processing
        |- analysis/
        |- plotting/
        |- logger_config.py (for example)

# Atom



# Markdown and READMEs


# Rstudio


# ShareLaTeX
I refer you to my earlier blog on this, [here.](http://reckoningrisk.com/research-practice/2017/comparing-editors-for-reports/)

# Logging
Logging your code is an alternative to lots of print statements and it's more robust if you run your code on a server or other system that doesn't have a terminal.
It also timestamps statements so you know when and where the code broke.
[Here is my logging function](/post_assets/logger_config.py) which you can use in python.
If you add this file into your `code` directory and then in each of your .py scripts add the following code block where you import your libraries:
{% highlight python %}
# init logging
import sys
sys.path.append("code")
from logger_config import *
logger = logging.getLogger(__name__)
{% endhighlight %}

And a statement like this in each place you want to log:
{% highlight python %}
logger.info('Reading metadata')
{% endhighlight %}

# PaperPile
Check out our earlier blog on this, [here.](http://reckoningrisk.com/research-practice/2017/literature-reviews/)
