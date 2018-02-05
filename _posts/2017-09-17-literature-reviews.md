---
layout: post
title:  Documenting literature reviews
author: Tim Williams and Tom Logan
excerpt: How we organize our academic readings.
date: 2017-09-17
categories: research-practice
comments: true
toc: true
---

[Click here to download our spreadsheet](/assets/blog/2017-09-17-literature-reviews/reading_list.xlsm)

Reading is an integral part of being a PhD student, researcher, or academic.
Without knowing the state of the literature, you cannot evaluate the merit of your work.
And without being confident in the merit of your work, you run the risk of unknowingly reinventing the wheel.
And that's generally not highly valued in academia.
Long story short - you're wasting your time.

Conducting a literature review can appear to be a daunting task.
But with the right tools at hand, literature reviews can be satisfying, and even fun.

In this blog post we're going to present our approach to documenting and managing a literature review.
We've developed a very functional (and might I say it, pretty beautiful) excel spreadsheet that can be used to store information about papers you've read, and most importantly the notes you've taken while reading these papers.
You can filter your library of notes by various keywords, allowing you to methodically assess what you've read.

After looking online for something that achieved what we wanted, we drew a blank.
So we created it ourselves.
The spreadsheet is included on this page so that you can download and use it yourselves.

But first things first, we can't write this post without mentioning Paperpile.

# Paperpile

Paperpile is a web-based citation manager. It's great. The focus of this post isn't meant to be Paperpile, but we love it so much we can't resist.

## Our favorite features:

**1\.** If you install the Paperpile extension in Google Chrome (and it's only available in Chrome), whenever you search Google Scholar you'll see this:

<p align="center">
  <img src = '/assets/blog/2017-09-17-literature-reviews/scholar.png' width="70%">
</p>

To add a paper to your library, just click the Paperpile button.
The green tick on the first one means I've already got it in my library.

**2\.** You can add papers into different folders (and sub-folders, and sub-sub-folders, ...) within Paperpile to sort your papers.
Each paper can be in multiple folders.

<p align="center">
  <img src = '/assets/blog/2017-09-17-literature-reviews/paperpile.png' width="70%">
</p>

**3\.** You can sync Paperpile with Google Drive. After you add a paper to your library it will automatically download to your computer (if you sync Google Drive with your computer, which I would also highly recommend). Papers are sorted by author's last name.

<p align="center">
  <img src = '/assets/blog/2017-09-17-literature-reviews/files.png' width="55%">
</p>

**4\.** You can have collaborative projects (i.e. shared Paperpile libraries).

**5\.** You can highlight and take notes in papers within Paperpile in Google Chrome itself (or in your favorite PDF editor on your computer).

**6\.** There's a Google Docs add-in, which lets you cite papers from Paperpile directly and create bibliographies.

## Cons of Paperpile:
**1\.** It costs $3 per month (but we think it's worth it).

**2\.** There's no user-friendly way to create and save notes that you take while reading.

We can't do anything about Con#1, but Con#2 we can....

# Our super-spreadsheet

When conducting a literature review it's useful to be able to:

1. Highlight important parts of the papers you read;
2. Take notes summarizing main ideas, insights, etc.; and
3. Somewhat methodically order and sort the various papers you've read.

Our spreadsheet is a user-friendly and functional way to achieve #2 and #3.

<p align="center">
  <img src = '/assets/blog/2017-09-17-literature-reviews/excel.png' width="70%">
</p>

## Taking notes

The user can input details of the paper in the first few columns, and then take notes in the right-hand columns. This way, if you're thinking to yourself "what's that paper from PNAS I read last week?", the answer is right there.

The column headings that you choose for your notes can also be changed to suit your preferences. We've chosen "Main ideas", "Methods", "Results", ..., but if other column headings are more relevant to your field, then that's fine. You can also add additional columns (although this may require some tweaking of the filter formulae -- see the README in the spreadsheet).

This part of the spreadsheet is pretty standard.

## Filtering

Here is where the magic comes in. We've built a few simple macros into the spreadsheet that allow you to filter your library of notes by various keywords. After trawling the internet for blogs and help forums that addressed this issue we found a lot of questions, but no satisfying answers. Here it is.

<p align="center">
  <img src = '/assets/blog/2017-09-17-literature-reviews/filter_bar.png' width="60%">
</p>

There are two ways to filter: the "OR" search allows you to input multiple keywords and return all papers that contain at least one of these search terms (e.g. all papers either written by "Logan" or containing the word "regression" in the notes columns); the "AND" filter returns results that match all criteria you specify (e.g. all papers written by "Logan" that contain the word "regression" in the notes columns).

This is great, and allows you to quickly and methodically browse through your library of reading notes.

The in-built Microsoft Excel filter and sort features can also be used, for example if you want to sort your papers (or your search results) by publication date.

# Last words

We hope you've found this useful. While this tool doesn't actually read the papers for you (maybe talk to a CS major if you're interested in this), it should make the process of documenting what you've read a whole lot easier. We've included this spreadsheet at the top of this blog post. Have fun with it!
