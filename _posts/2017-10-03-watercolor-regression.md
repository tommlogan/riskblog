---
layout: post
title:  "Watercolor (aka Visually Weighted) regressions in Python"
author: Tom Logan
excerpt: Scatter plots with coloured bands for the distribution.
date:   2017-10-03
categories: coding
comments: true
---
I first saw a watercolour regression in a paper by my colleague Andrea Staid on [wind prediction for wind energy](http://pierrepinson.com/docs/Staid2013_maxwind_revised.pdf).
She had this neat figure here which shows a probabilistic prediction band:
<img class ="image" src="/img/blog/staid.png"  width = "70%">
I want something similar to this for a research project and came across the work of [Schönbrodt](http://www.nicebread.de/visually-weighted-watercolor-plots-new-variants-please-vote/) and [Hsiang](http://www.fight-entropy.com/2012/08/watercolor-regression.html).
<p class ="image cent">
  <img src = '/img/blog/schonbrodt.jpeg' width="40%">
  <img src = '/img/blog/schonbrodt_2.jpeg' width="40%">
</p>
Seriously, how cool is that.

Basically, the figure on the left shows the scatter and the 1st, 2nd, and 3rd standard deviation away from the median. The figure on the right shows this with some smoothing.

But! Their code is in R and Matlab respectively and I want it in Python. A quick Google didn't turn anything up (except this [Stack question](https://stackoverflow.com/questions/12465608/python-scatter-plot-with-median-and-ci)).

I'm going to start off easy and not run any regression.
  I just want a line which goes through the median value and has bands at the 25th and 75th percentile, the 10th and 90th, and the 5th and 95th.
  A couple of options from my attempts below.
  Option 1 (Top left) uses the colour palette from Schönbrodt's figures. It has three distinct, albeit similar colours.
  The second option uses different transparencies of the same colour.
  The final option reverts the scatter points to their default style provided through the style context option - using this approach will ensure consistency between figures.

<div class="cent">
  <img src = '/img/blog/fig1.png' width="30%">
  <img src = '/img/blog/fig2.png' width="30%">
</div>
<img class ="image" src="/img/blog/fig3.png"  width = "70%">

If this is of use to anyone, the code is on my [github](https://github.com/tommlogan/watercolor).
