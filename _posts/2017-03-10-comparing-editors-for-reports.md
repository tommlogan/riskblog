---
layout: post
title:  Comparing Editors for Reports
author: Tom Logan
excerpt: I've spent some time comparing Google Docs, Word, Sharelatex, and Overleaf on their suitability for writing academic papers. This is my personal evaluation.
date: 2017-03-10
categories: research-practice
comments: true
toc: true
---

*Note: ShareLaTeX and Overleaf have announced a pending merger.*

I’ve spent a bit of time comparing the two main online latex providers and am sharing my evaluation here.

# Why?
I want to improve my authoring workflow.
I want a platform which does the following:
* Large document writing (no lag)
* Secure and backed up
* Easy citation management
* Simple figure insertion and referencing
* Collaboration
    * Comments
    * Track changes
    * Shared
* Keeps everything in one place (I don’t want documents in too many directories)

Reasonable enough, right? The options I considered were:
* Google Docs with Paperpile
* Word and OneDrive with Mendeley
* ShareLaTeX with Git integration
* Overleaf with Google Drive and Git integration

# Google Docs
We started our collaboration on Google Drive because Tim wanted to use Paperpile and I didn’t really care. Paperpile is the citation manager which has a Google Doc add-on for cite-while-you-write. This worked really well in the early stages of our project for brainstorming etc and even during the writing it was great. The issues started to emerge with figures and the straw that broke the camel’s back was an issue with the citation manager.

## Figure referencing limitation
In Google Docs you can not use figure referencing. In Word it is possible to automatically number figures and reference them in text so that if you add a figure before Figure 4, then the original fourth figure becomes Figure 5 and all the in-text references change from 4 to 5. Google Docs doesn’t have that capability.

## Heading numbering
I realize as I’m writing this that Google Doc doesn’t automatically number headings. So if I add a heading before 1.1.1, then I’ll have to change 1.1.1, 1.1.2, … ad nauseum.

## Multiple in-text citations
If you click ctrl+alt+p with paperpile add on enabled it’ll open up a little drop down menu from which you can choose a reference to add from your PaperPile reference library. This is really cool. I actually really like paperpile, however when I added multiple citations e.g.
“Of the 5.25 trillion particles of plastic estimated in the oceans, 95% is smaller than a grain of rice (Eriksen, 2014). A single fleece jacket can release as many as 250,000 plastic fibers and the scale of plastic released into our ocean is devastating the ecosystems and the food chains upon which we depend (Hartline, 2016; Wilson, 2017)”
<!-- <img align="right" src="/img/blog/trump_wrong.gif" width=50%> -->
The citations are super easy, but I realized that the 2nd citation, Wilson 2017, was omitted from the reference list at the end of the document.

So Google Docs is out until that's fixed.

# Microsoft Word
Next attempt, Microsoft Word. A classic. I downloaded the article from Google Docs and added the figure references and re-did all of the citations in Mendeley (fortunately you can export paperpile library to Mendeley).
With Word and OneDrive I could collaborate realtime, it’s not as good as Google, but it’s ok.
But then it started to lag. The size of the document is so inefficient due to figures or equations that the whole thing slows down. It was unbearable. So I got through that, but now I was looking for something better.

# Online LaTeX
I’d heard of Latex, but I don’t use lots of equations so I didn’t think it was catering for me. But I read a little bit about it, heard from others using it, read a bit more, and my interest was piqued. Latex is a language, and you can download software and GUIs for it on your desktop, but to avoid the issues you can also use online latex editors: ShareLaTeX or Overleaf. Both also come with citation managers, version control, and varying integration with git, DropBox, or GoogleDrive. Basically, the online tools remove many of the barriers to using latex and allow for online, realtime, collaboration.

In the following sections I’m going to outline and discuss the differences between these, state my preference, and provide examples of how to use them.

## Integration with Git
### ShareLaTeX
Once you register your (paid, $8/month or $80/year) account, go to account settings and integrate your github account. Note this is GitHub, not GitLab, so you’ll need a GitHub account. As a student you have unlimited private repos on GitHub. (Discussion about integrating GitLab and GitHub can occur another time - what I do is have many of my projects in GitHub and the ones that I want to share with the group or when I want to share specific code I put into GitLab. It is possible to have a sync).
Back at the main page, click New Project -> Import from GitHub and select the repository from the menu.
<img align="center" src="/img/blog/latex-compare/share-1.png">
So COOL!

This pulls in the entire repository directory, and doesn’t care where the .tex (latex file) is located.

Now, if you make any changes to the .tex file then you click Menu and under Sync choose GitHub.
<img align="center" src="/img/blog/latex-compare/share-2.png">

This lets you push or pull changes to GitHub:
<img align="center" src="/img/blog/latex-compare/share-3.png">

For example, if I want to add a figure into the document, I’ll drop it into my folder on my desktop, push the changes to github, then pull them into ShareLaTeX (the top option).
Or if I’ve finished modifying, I’ll push my ShareLaTeX to github.

### Overleaf
Overleaf operates slightly differently to ShareLaTeX. It exists as a repository. You create your project in Overleaf, then clone it to your desktop folder [here](https://www.overleaf.com/blog/195-new-collaborate-online-and-offline-with-overleaf-and-git-beta#.WMQVG_krLb0). Or you can set it up as a [second origin](https://www.overleaf.com/help/230-how-do-i-push-a-new-project-to-overleaf-via-git#.WMQVUvkrLb0). So you would have the gitlab or github repository and then once you set up the overleaf origin you can use git push overleaf master or git pull overleaf master. The changes are automatic.
This is also pretty cool. I’ve had minor issues with this, in particular with merge conflicts. Also you have to have the .tex file in the main directory (not a subfolder) which means you can’t have a “report” or “submission” folder.

## Citation Manager
Both ShareLaTeX and Overleaf integrate well with Mendeley.
Citations are super easy. The .bib file automatically has all of your articles with last name and date e.g. Lempert2002a and when you type e.g. \citep{} it provides a drop down list so you can choose your citation.
Some citation examples are [here](https://www.economics.utoronto.ca/osborne/latex/BIBTEX.HTM).

### ShareLaTeX
ShareLaTeX has a nice import and sync feature with Mendeley however it doesn’t support Mendeley groups which is devastating to collaboration. How is a collaborator of mine able to add a new reference and then inline citation if the whole project is linked to my .bib file. Argh.
But there’s a work around, it’s just sad that they were so close. Basically, in Mendeley you have groups and these include your collaborators. Anyone can add references to these lists. To update the list, you could export the .bib file from the group
<img align="center" src="/img/blog/latex-compare/mendley-1.png">

Sync it to or copy it to the file with your .git and then push the changes. And pull the changes into ShareLaTeX.

### Overleaf
Mendeley integration here is easy. You can import the entire library from Mendeley. To update it though it seems you have to delete and re import which is a bit odd so I think I’m missing something.
Overleaf does groups great!

Click on the drop down arrow by files, click Bibliography

<img src="/img/blog/latex-compare/overleaf-1.png">

Choose Mendeley
If you have a group, choose it:
<img src="/img/blog/latex-compare/overleaf-2.png">
Tots amazeballs.

## Comments and Track Changes
### ShareLaTeX
ShareLaTeX comments and track changes are hands down awesome.
Select some writing and in the RHS you’ll see a little comment icon. Click it.  
<img src="/img/blog/latex-compare/share-4.png">  
<img src="/img/blog/latex-compare/share-5.png">    
Seriously cool.  
When you do this it automatically enables review mode. You can also do this at the top RHS:
<img src="/img/blog/latex-compare/share-6.png">  
For track changes, you need to set on <img src="/img/blog/latex-compare/share-7.png"> you need to pay for this (commenting is free)
Check out their [examples](https://www.sharelatex.com/track-changes-and-comments-in-latex).
I’m very impressed.

### Overleaf
Overleaf has two options for comments. One is a package called \todo ([example here](https://www.overleaf.com/8555149xcnnfbpmgchb)). Which is pretty neat.  

The other is a rich text option so change your view to rich text: <img src="/img/blog/latex-compare/overleaf-3.png">  
Then with your cursor in the document you want the comment you click the comment button <img src="/img/blog/latex-compare/overleaf-4.png"> and insert the comment
<img src="/img/blog/latex-compare/overleaf-5.png">

Track changes is a little different. It requires you to save a version and then compare versions.
<img src="/img/blog/latex-compare/overleaf-6.png">
I think ShareLaTeX is better. But Overleaf isn’t bad.

# Final Thoughts
I like both. Overleaf is cool with its rich text option for sending to collaborators who want to add comments and make changes who aren’t comfortable with latex. It also provides all of these features for free, except for having private/protected files. E.g. with the right link anyone can see your paper. ShareLaTeX files are all private.

ShareLaTeX is superior in it commenting and git integration and the directory structure. It’s for this reason that I’m in favor of ShareLaTeX. Overleaf is nice with its sync to Google Drive, but if you’re using git properly, git can be smoother.

ShareLaTeX requires you to pay for Git integration. But you’re going to have to pay for either if you want to actually use them securely and to their best extent. It’s not that much.

| Feature        | ShareLaTeX           | OverLeaf  |
| ------------- |-------------| -----|
| No lag with large documents [Also check out this for giant documents like theses](http://tex.stackexchange.com/questions/29577/splitting-a-large-document-into-several-files)     | 1= | 1= |
| Secure and backed up      | 1=      |   1= (paid) |
| Citation | 2      |   1 |
| Figures | 1 | 2 |
| Comments | 1 | 2 |
| Track changes | 1 | 2- |
| Shared/real time collaboration writing | 1 | 1 |
| Directory structure | 1 | 2 |
| Git Integration | 1 (paid) | 2 |
| Google Drive integration | - | 1 |
| DropBox integration | possible, untested | possible, untested |
| Price (annum) | $80 | $72 |

Note that ShareLatex has group pricing which the research group, department, or college could look into. E.g. 10 people $500/year, 12 people = $600, 15 people = $700.
