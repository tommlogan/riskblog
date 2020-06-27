---
layout: post
title:  Better Coding Practice
author: Tom Logan
excerpt: Have you ever had to revisit a coding project? If you're like me, there's a sense of trepidation. Will I remember what I was doing? Will it still work?  Here are some techniques that may make you a happier and more efficient researcher.
date:   2018-01-31
categories: research-practice coding
comments: true
toc: true
---

Have you ever had to revisit a coding project? If you're like me, there's a sense of trepidation. Will I remember what I was doing? Will it still work?  
They say that your closest collaborator is your past self, except she/he doesn't respond to emails...

Well, I got a bit sick of that feeling and have learnt some techniques which my future self will be thankful for (or darn well better be). And that's what I want to share with you. Note that many of these are adapted from [Jeff Leek's book, *How to be a Modern Scientist*](http://jtleek.com/book/).  

Also, I believe that these skills are an essential thing to learn, whether we plan on becoming academics, valley entrepreneurs, or other consultants - the internet is not going anyway, we will be collaborating in teams on code, and preparing ourselves for this is only to our advantage.

# Workshop and slides
I'm presenting a workshop for the INFORMS student chapter at the University of Michigan (Institute of Operations Research and Management Science) and the slides are available [HERE.](/assets/blog/2018-01-31-better-coding-practices/informs_better-coding-practices.ppsx)

{% include button.html button_name="Slides available here" button_class="outline-primary" url="/assets/blog/2018-01-31-better-coding-practices/informs_better-coding-practices.ppsx" %}

The blog below is really a complement to the slides, rather than stand alone, so check them out!

# GitHub
Version control is essential. It is essential for research projects and any collaborative project.
Version control time stamps every change you or someone else makes on a project.
This means that you can return to every previous instance of your code, which is incredibly relieving if you make a mistake or the code stops working.
It is also great to see how, when, and (providing the commit messages are decent) why different things were added or changed in the code.

# Directory structure
    |- <your project name>/
    |- .git
    |- `_scratch`/
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
Atom is currently my favourite code editor when I'm writing in python or css/html etc.
I'm also a fan of sublime, although I haven't got it to integrate with git like Atom does.
By clicking ctrl+shift+9 in Atom you toggle the git tab and can then stage, commit, push, and pull from the GitHub repo.
I find that this significantly lowers the barrier to making regular and contained commits, which makes the repo cleaner and easier to interpret.

# Markdown and READMEs
Another thing that I love about Atom is how it renders a preview of Markdown (.md) documents.
Markdown is a plain text language, with very easy inclusion of code and math.
It renders on the README of GitHub repositories and READMEs are crucial for understandable repos.
When you're reading or editing a .md document in Atom, clicking ctrl+shift+m opens the preview pane.
A decent readme on a project's repo outlines the steps and assumptions taken.
It makes the whole project much more accessible to future collaborators and yourself when you return to the project.
It also looks more professional when potential collaborators or employers are looking at your GitHub repos.
The README.md file could also include variable names and descriptions if your project includes a statistical analysis.

# Rstudio
Rstudio can do many of the things Atom can, and is the go-to option if you're coding in R. (Although I still prefer to write my README.md in Atom, even when coding in R).
The slides show how Rstudio can be used to regularly make git commits and write and preview markdown.

# ShareLaTeX
I refer you to my earlier blog on this, [here.](http://reckoningrisk.com/research-practice/2017/comparing-editors-for-reports/)

# Logging
Logging your code is an alternative to lots of print statements and it's more robust if you run your code on a server or other system that doesn't have a terminal.
It also timestamps statements so you know when and where the code broke.
[Here is my logging function](/assets/blog/2018-01-31-better-coding-practices/logger_config.py) which you can use in python.
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
