---
layout: post
title:  "Realtime Resilience? On the uses of social media for understanding communitites"
author: Ben Rachunok
excerpt: Hurricane Dorian continues to move up the east coast of the US, causing catastrophic damage to communities. In the era of big data, what kind of analysis can we do to understand how communities respond to disasters in real time?
date:   2019-09-20
categories: research
comments: true
---

>*Disasters are acts of God, but damages are acts of Man'
>--(1945) Gilbert White. 

<img class ="image" src="/assets/blog/2019-09-03-resilience-fingerprint/overview_figure.jpeg"  width = "80%">

When disaster strikes, what makes a community more or less resilient? A landmark [2008 paper by Cutter, Barns, Berry et al.](https://doi.org/10.1016/j.gloenvcha.2008.07.013) proposed a framework for overall community reslience into a series of categories. They propose that community resilience is mutidimensional, built on *ecological, social, economic, institutional, infrastructure, and community competance* dimensions. 

My paper, “[Twitter and Disasters: A Social Resilience Fingerprint](https://doi.org/10.1109/ACCESS.2019.2914797)”, was pubsished recently in IEEE Access and aims to investigate how these elements of community resilience can be analyzed in real time using social media. That is, **what can we learn about a communitiy's resilience by analyzing their tweets?** We develop an algorithm which reads in tweets related to a natural disaster, processes them relative to the categories developed by Cutter et al., and determines how community resilience manifests itself through social media. I apply this algorithm, called Social Resilience Fingerprinting, to 14 different disasters and major events.

From this, we find two important contributions: (1) *types* of disasters have a unique fingerprint which is easily detectable through social media. That is we can learn -in an unsupervised way based only on the community resileince categories- whether a disaster is a hurricane, earthquake, political event etc. And (2) when dealing with disasters which pose imminent threats to the US (such as hurricanes), we see the incluence of the **ecological** category as a primary driver between the similarity of social media responses.

In the folling picture, for example, is a visualization of a *fingerprint* in the heatmap on the left. For the tweets from a disaster (in this case, the 2018 Hurricane Florence), a more red square indicates a stronger presence of the two elements of resilience occurring together in the data after adjusting. The figure on the right shows all the disasters, plotted based on their principle components demonstrating the similarities in the patterns of tweets.
<img class ="image" src="/assets/blog/2019-09-03-resilience-fingerprint/algorithms.png"  width = "909px">

The key takeaway is that if we assume Tweets represnt a version of how individuals respond to disasters, we find that different **types** (hurricanes, earthquakes, political) events have commonalities in how they impact communitites. This work forms the basis of a new body of work in which we hope we can make *predictions* about how a community will respond to a disaster in the future. The goal is to be able to predict the future outcomes of community resilience in real time!


[For more information, the UN office of Disaster Risk Reduction has written a fun summary](https://www.preventionweb.net/news/view/66690) and the paper can be found here:

Rachunok, Benjamin A., Jackson B. Bennett, and Roshanak Nateghi. "Twitter and Disasters: A Social Resilience Fingerprint." IEEE Access 7 (2019): 58495-58506. [DOI: 10.1109/ACCESS.2019.2914797](https://doi.org/10.1109/ACCESS.2019.2914797)

(And it's open access!!)

