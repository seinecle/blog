---
layout: post
title: A call to grow an ecosystem of apps for text and network analysis on new data sources
permalink: /call-growing-ecosystem-apps-text-network-analysis-new-data-sources/
published: true
date_readable:               Jul 23, 2023
last_modified_at_readable:   Jul 23, 2023
categories: [nocodefunctions, data, Twitter,community]
---
With the end of the free Twitter API, network and text analysts are looking for new data sources. This is an opportunity to stimulate the ecosystem of apps that specialize in data import, text mining and transformation to networks.

# End of the Twitter API: a problem, and an opportunity
A large crowd of diverse actors relied on the Twitter API to collect data for text analysis, network analysis or both.
Just taking academics, you find a rapidly growing number of publications mentioning the "Twitter API" in recent years:

|  year | count of publications mentioning the Twitter API  |
| --- | --- |
| 2017  | 2,200
| 2018  | 2,480
| 2019  | 2,620
| 2020  | 3,100
| 2021  | 3,890

(source: [Google Scholar](https://scholar.google.com/scholar?q=%22twitter+API%22&hl=fr&as_sdt=0%2C5&inst=3539827323569926917&as_ylo=2017&as_yhi=2017))

With the new plans for API access [set at prohibitive prices](https://developer.twitter.com/en/products/twitter-api), this stream of publications will run dry.

## What's next?
Passed a moment of shock and disbelief, academics and others (OSINT, journalists, marketers, developers, etc.) start turning to other data sources.

![meme from the office](/blog/assets/image/again.gif)

Here are the data sources that I personally consider, or that I heard others considering:

- [Open Street Map](https://www.openstreetmap.org/#map=5/46.449/2.210) ([API](https://wiki.openstreetmap.org/wiki/API))
- Wikipedia / [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page) ([API](https://www.wikidata.org/wiki/Wikidata:Data_access/en))
- Spotify ([API](https://developer.spotify.com/documentation/web-api))
- Reddit (well... [not anymore](https://en.wikipedia.org/wiki/2023_Reddit_API_controversy))
- Mastodon ([API](https://docs.joinmastodon.org/api/))
- [OpenAlex](https://openalex.org/) (this one is quite specialized but really worth a look: gigantic, free access to global scientometric data).

The obvious reaction is: none of these are an equivalent to Twitter.
It will take a mourning period but yes, we'll have to move on (I won't engage here on Threads, just: I don't wait or count on an API access to it).
Human curiosity must find other objects to apply to.

> **Prediction 🔮: we are going to see, in the next months and over 2024, an intense activity of developing importers and user interfaces for these alternative data sources mentioned above.**

# New data importers, new analytics, new user interfaces: a call to talk and exchange
In informal discussions and reading posts from specialists on Twitter, I see that:

- there is strong interest in new data importers, either for one's consumption or as a service to offer
- accordinly, tech-savy individuals, organizations and app developers are building new data importers
- the same actors are developing transformers for this data: text and network analysis methods (otherwise offering raw data is not of great value)
- this also triggers a re-thinking of exisiting user interfaces, and the development of new ones

This means that we are at the start of an intense period of thinking, tool building and new services that are going to be created.
This is a great occasion to address the makers of these solutions-to-come, and my question to them is:

**Why would we need to do this in isolation?**
I think that there are two big reasons not to engage in collaborations, and one of them is a false one.

**One reason not to engage in collaborations** is to keep one's product secret and non reproducible, to build a competitive advantage.
A data importer with some clever data transformation added to it can deliver insights of great value, so let's not share it.

A second reason could be technical and resources constraints.
Working alone can let you go faster, as collaborating adds coordination and interfacing costs and delays.

**This second reason is less strong, I believe.**
Coordination and interfacing costs are real, but setting up a collaboration also helps distribute work among many, instead of doing everything by one's self.

Let's consider the steps for a service consisting in, say, creating a word cloud from the most common expressions used in a set of Wikipedia pages.
*Constructing the word cloud is far from the only operation we need to build*.

> Are you ready to design and implement each of these 9 operations, and especially the 9th one?

1. Creating a interface (web, mobile app or desktop?) where the user will express their query and choose their parameters
2. Hosting this interface (server costs, maintenance of the app for multiple OS...)
3. Choosing and familiarizing with an API client for Wikipedia, writing the code to fetch the any query
4. Storing the data - issues of scale and OS specificity
5. Parsing and cleaning the data (are you supporting different languages?)
6. Constructing the word cloud
7. Formatting the results: a picture of the cloud, a table view of the underlying words and their counts, a [gexf](https://gexf.net/) network format for the underlying network of relations?
8. An interface to export the results: showing the picture on screen, downloading the picture in different formats (svg, png?), exporting to Excel and Google Sheets, visualize the word cloud in an interactive way with [Gephi Lite](https://gephi.org/gephi-lite/), [VOSviewer online](https://app.vosviewer.com/) or a custom [D3](https://d3js.org/) view, export a gexf or [GraphML](https://fr.wikipedia.org/wiki/GraphML) to be opened by [Gephi](https://gephi.org/) or [NodeXL](https://www.smrfoundation.org/nodexl/)?
9. Maintaining steps 1 to 7 through time 😅😱.

I believe that relatively big for-profit organizations have a motive and the resources to handle these 9 steps all by themselves (even then, they rely and contribute to open source solutions for parts of the process!)

For smaller organizations (for profit or not) and individuals, there is a strong case to join forces when and if possible, to help each other on one or several steps of the process above.

# I go first: what I am happy to help with 🤗

The list below are functional blocks that I can relatively easily provide to you, in a format that suits your needs.

## Tools

- methods to [extract words](https://github.com/seinecle/umigon-tokenizer) and [n-grams](https://github.com/seinecle/umigon-ngram-ops) from a given text
- methods to convert [co-occurring words into a network of words](https://github.com/seinecle/cowo-function)
- methods to infer the [sentiment from a text](https://github.com/seinecle/umigon-family/tree/main/umigon-core)
- methods to [detect key topics in text](https://github.com/seinecle/topics-detection-function)

## Interfaces

-  you are free to add your method to [https://nocodefunctions.com](https://nocodefunctions.com), which sorts out interfacing and hosting issues
-  we can work at interfacing your app and nocodefunctions.com, which means your app integrates some of the functions of nocodefunctions.

*(this one seems like: "ah ah I see your ulterior motive for all this, you want to grow your web app!" I would be happy to, that is true. I also know that many developers don't have the time to maintain their own web app, so I offer this for them).*

## Import / export

- from a csv, txt, pdf or Excel file to the plain text they contain
- from a gexf or graphML file to a url to visualize this file on the web

# "How to start collaborating? I code in R / Python / JS and I don't know how to do X, Y or Z"
## The first immense step is *psychological*
I know from experience that it is very hard to share one's code or application.
For the first 10 years of my coding career, I did not really open sourced my apps completely, because of an inner fear that I would be "copied" or robbed of the value that I had created.
I thought that maybe, someday, I could monetize what I produced, so it would be silly to publish the result of my hard work and get anyone to use it before me.
It took ten years but I am past that.
I still believe that there is a tiny chance that one day I'll be able to earn something from what I create, but in the meantime this should not keep what I do hidden and unproductive.

## The second step is technical: how to integrate or interface codes from 2 different persons? 
This is not hard actually, we'll figure out a way to coordinate.
The general idea would be to keep the two projects separate, and to build interfaces to join the two.
These interfaces can be of different sorts:

- creating a web API which takes project's A output and format it so that project B can use it
- creating a command line interface for the same result
- harmonizing data formats to facilitate exchanges

I am happy to work on these interfaces with you, let's connect!

![a hand shake](/blog/assets/image/handshake.jpg)

Let's get in touch, either privately ([analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)) or let's discuss pubblicly on [Twitter](https://twitter.com/seinecle) or [Mastodon](https://ioc.exchange/@seinecle).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

