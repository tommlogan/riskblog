---
layout: post
title: Code Snippets
categories: Design
excerpt: Quick overview on how to post code snippets using Liquid tags and how to escape or not escape markdown and HTML in your blog entries.
---

Note: To start up the server and view drafts, use:
1. powershell  
2. `bash`
3. `bundle exec jekyll serve --drafts`


Whenever you need to post a code snippet, use the liquid tags `highlight` and `endhighlight` like this:

{% highlight ruby %}
# some code goes here
puts "Hello World!"
{% endhighlight %}

Now for some python

{% highlight python %}
def foo:
    x = 5
    return(x)
{% endhighlight %}
