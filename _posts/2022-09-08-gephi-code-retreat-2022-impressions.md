---
layout: post
title: Gephi code retreat for 2022 - why did I participate?
permalink: /gephi-code-retreat-2022-why-participating/
published: false
date_readable:               Sept 08, 2022
last_modified_at_readable:   Sept 08, 2022
---

*Some background on why I participated to the Gephi Code Retreat - 2022 edition, which took place in Paris last week*

<div align="center">
   <img src="https://upload.wikimedia.org/wikipedia/commons/0/04/Gephi-logo.png" title="The Gephi logo" width="300px"/>
</div>  

# Quick background on Gephi

Two-line summary if you don't know Gephi. Born around 2010, [Gephi](https://gephi.org) is the leading software for the visualization and exploration of networks.
It is open source and free. It is used by analysts, professors, journalists, students. It useful to find patterns and connecting the dots in rich and unstructured datasets, for instance: finding communities, people with key roles in a crowd, identifying connections between items or products, etc.

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/189077290-65d51016-df16-4b8c-a154-0cf64ee01eb9.png" title="A screenshot of Gephi" width="500px"/>
</div>                                                                                                                                  

**Gephi has been downloaded [millions of times](https://seinecle.github.io/gephi-tutorials/generated-html/history-en.html#_a_cumulative_downloads) since its creation**, and the original paper describing Gephi has been cited by close to **[10,000 academic publications from a huge variety of scientific fields](https://scholar.google.fr/citations?view_op=view_citation&hl=fr&user=fEDLILQAAAAJ&citation_for_view=fEDLILQAAAAJ:u5HHmVD_uO8C)**.

The Gephi Code retreat is a one-week event organized by the founding members of Gephi to accelerate the development of the software and help the community of Gephi enthusiasts meet and cohere. That is the second year such a retreat is organized, after a first edition in Copenhagen.


# My relation to Gephi


## From a historian to discovering Gephi

Gephi is the reason I transitioned from being a historian of science to a social scientist using computational (data-intensive) approaches.
As a post-doc at the [KNAW](https://www.knaw.nl/en) in the Netherlands in 2008, Gephi had just appeared (there was also [GUESS](http://graphexploration.cond.org/) that I used as well).

I realized that to explore and find insights in networks of neuroeconomists (that was my interest at the time), Gephi was going to be much more useful than by scrolling through big tables in Excel (see two publications [1](https://www.nature.com/articles/nrn3354) [2](https://www.frontiersin.org/articles/10.3389/fnhum.2016.00336/full) of this research project that used Gephi and VOSviewer).

## Killer features

The classic workflow in Gephi is super effective at delivering insights:

1. get the big picture: with a dynamic layout you get immediately a sense of the size, patterns of relations, core / periphery structure... that characterize the network:

<div>
   <img src="http://www.martingrandjean.ch/wp-content/uploads/2016/05/Airports-network.gif"/>
</div>   



3. detect communities (in one-click): quickly see how a crowd divides in sub-groups, based on the pattern of connections between the members of the group
4. find central nodes: which member of the group has the most connections? Who is placed "in the middle", relation to the others?
5. zoom on sub-regions: what if we filter out all the network except for one group of nodes and their relations: can we identify local communities within this subnetwork? Who are the central actors within this region?

The killer feature of Gephi is that these 3 operations have an intuitive, **illustrated** expression in Gephi:

1. Paint different communities in different colors
2. Scale the size of the nodes according to their centrality
3. hide the parts of the network you want to ignore, continue working on the visible part
4. 




I started asking a lot of questions on the [now defunct Gephi forum](https://forum-gephi.org/), and answering lots of questions as well.
The community of users is now the most active in a [private Facebook group](https://www.facebook.com/groups/gephi) (join!), where I continue being active.

Quickly as a user of Gephi, I was frustrated not being able to access basic functions I needed.
"Gephi can be extended with plugins" is a reply I often got.
As I am not a computer scientist, this sounded too hard.
But if I just need, you know, a plugin to change the colors of my nodes - surely it can't be *that* hard to create? 

In the end, in 2011, I jumped in this strange world of Java, [buying a book for complete beginners](https://www.amazon.fr/Java-Beginners-Guide-Herbert-Schildt-dp-1260463559/dp/1260463559/) and learning how the thing works. Besides a book, everything is free: the software to code (I still use [NetBeans](https://netbeans.apache.org)), and the Java language itself. Not costly to try!

I got hooked when I realized it was a zillion time faster than Excel - literally waiting for half an hour to end up crashing Excel became a 10 seconds operation!
I used Java first to create custom gexf files (custom made networks!!) and finally [some plugins for Gephi](https://gephi.org/plugins/#/browse/search/levallois).

Another big help in learning how to program was Stackoverflow.
This is THE Q&A website for programming issues, and browsing back to the first question I asked on it, you see it really shows that I was [transitioning from Excel to Java](https://stackoverflow.com/revisions/7200090/1)!

Knowing how to program came with exponential benefits, beyond Gephi and right away. Java is a versatile language which enabled me to easily [analyze text](https://aclanthology.org/S13-2068/), create [web apps](https://nocodefunctions.com), [desktop apps](https://github.com/seinecle/Gaze), publish courses [in fancy formats](https://seinecle.github.io/mk99/), [grade large groups of students without going mad](https://github.com/emlyon/GradingPicsOnBrightspace), [teach a course on how to create mobile apps](https://seinecle.github.io/codapps/), [create silly personal projects](https://github.com/seinecle/lescalanquessontellesouvertes), and more.

I wrote [tutorials for Gephi](https://seinecle.github.io/gephi-tutorials/), and I continued using Gephi in most of my research projects to this day (on [collusion in European markets](https://onlinelibrary.wiley.com/doi/full/10.1111/jcms.12232), [dynamic inter-banking financial networks](https://www.risk.net/journal-of-network-theory-in-finance/2462066/dynamic-visualization-of-large-financial-networks), and new ways to identify [communities on Twitter](https://management-aims.com/index.php/mgmt/article/download/4245/10254?inline=1).

# What did I do / deliver?

I worked the full week on creating a plugin for Gephi that will allow a user, directly while using Gephi, to export the network they are working on to the web.
The network will be viewable and explorable from the browser, and shareable with a simple url.

[A short video with a live demo available here](https://www.twitch.tv/videos/1579615061?t=01h28m54s) explains all the details.

It is important and fair to note that the plugin leverages 2 key resources that I did not develop myself - [Alexis Jacomy](https://twitter.com/jacomyal) and [Ouestware](https://www.ouestware.com/en/) developed and designed them:

- the library to visualize the networks on the web, which is called [Retina](https://ouestware.gitlab.io/retina/beta/)
- the roadmap to actually export the network to the web, which involves creating a Gist on Github, and [which is publicly discussed here](https://github.com/gephi/gephi-plugins/issues/262#issuecomment-1231627948).

The plugin is not released yet, as it needs to be reviewed and will probably be released with a bunch of other deliverables produced by other contributors during this week.
You can [check the code here](https://github.com/gephi/gephi-plugins/tree/web-publish-plugin/modules/WebPublishPlugin), and see that I continue to push updates to refine it.

# If you'd like to see the Gephi week or what I'm doing

- Check the [Twitch stream of the Gephi week](https://www.twitch.tv/datalgo) - I'll try to say hi this afternoon (Paris time)
- Get fresh news from the [Gephi Twitter account](https://twitter.com/Gephi) and also from [Datalgo](https://twitter.com/nicolasbchb)
- Here are the [Gephi plugins I have developed over the years](https://gephi.org/plugins/#/browse/search/levallois)

I have written [tutorials for Gephi](https://seinecle.github.io/gephi-tutorials/).
I also build [nocode functions](https://nocodefunctions.com) 🔎 that can also serve the needs of the community of Gephi users. It is [fully open source](https://github.com/seinecle/nocodefunctions).
Try it and give some feedback, I would appreciate it!

* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about my journey as a social scientist and app developer.
