---
layout: post
title: A call to grow an ecosystem of apps for text and network analysis on new data sources
permalink: /call-growing-ecosystem-apps-text-network-analysis-new-data-sources/
published: false
date_readable:               Jul 23, 2023
last_modified_at_readable:   Jul 23, 2023
---
With the end of the free Twitter API, network and text analysts are looking for new data sources. This is an opportunity to stimulate the ecosystem of apps that specialize in data import, text mining and transformation to networks.

# End of the Twitter API: a problem, and an opportunity
A large crowd of diverse actors relied on the Twitter API to collect data for text analysis, network analysis or both.
Just taking academics, you find a rapidly growing number of publications mentioning the "Twitter API" in recent years:

|  year | count of publications mentioning the Twitter API  |
|---|---|
| 2018  | 2,480  |
| 2019  | 2,620  |
| 2020  |3,100   |
| 2021  | 3,890  |

This is over with the new plans for API access [set at prohibitive prices](https://developer.twitter.com/en/products/twitter-api).

## What's next?
Academics but others as well (OSINT, journalists, marketers, developers, etc.) turn to other data sources.
Here are the data sources that I personally consider, or that I heard others considering:

- [Open Street Map](https://www.openstreetmap.org/#map=5/46.449/2.210) ([API](https://wiki.openstreetmap.org/wiki/API))
- Wikipedia / [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page) ([API](https://www.wikidata.org/wiki/Wikidata:Data_access/en))
- Spotify ([API](https://developer.spotify.com/documentation/web-api))
- Reddit (well... [not anymore](https://en.wikipedia.org/wiki/2023_Reddit_API_controversy))
- Mastodon ([API](https://docs.joinmastodon.org/api/))
- [OpenAlex](https://openalex.org/) (this one is quite specialized but really worth a look: gigantic, free access to global scientometric data).

The obvious reaction is: none of these are an equivalent to Twitter.
It will take a mourning period but yes, we'll have to move on.
Not saying that Twitter data will not become available once more, one day, but waiting for this to happen, human curiosity must find other objects to apply to.

> **Prediction 🔮: we are going to see, in the next months and over 2024, an intense activity of developing importers and user interfaces for these alternative data sources mentioned above.**

# New data importers, new analytics, new user interfaces: a call to talk and exchange
In informal discussions and reading posts from specialists on Twitter, I see that:

- there is strong interest in new data importers, either for one's consumption or as a service to offer
- accordinly, tech-savy individuals, organizations and app developers are building new data importers
- the same actors are developing transformers for this data: text and network analysis methods (otherwise offering raw data is not of great value)
- this also triggers a re-thinking of exisiting user interfaces, and the development of new ones

**Why would we need to do this in isolation?**
After giving it some thoughts, I think that there are two big reasons not to engage in collaborations, and one of them is a false one.

**One reason not to engage in collaborations** is to keep one's product secret and non reproducible, to build a competitive advantage.
A data importer with some clever data transformation added to it can deliver insights of great value, so let's not share it.

A second reason could be technical and resources constraints.
Working alone can let you go faster, as collaborating adds coordination and interfacing costs and delays.

**This second reason is less strong, I believe.**
Coordination and interfacing costs are real, but setting up a collaboration also helps distribute work among many, instead of doing everything by one's self.

Let's consider the steps for a service consisting in, say, creating a word cloud from the most common expressions used in a set of Wikipedia pages.
*Constructing the word cloud is far from the only operation we need to build*.

> Are you ready to design and implement each of these 7 operations, and especially the 8th one?

1. Creating a interface (web, mobile app or desktop?) where the user will express their query
2. Hosting this interface (server costs, maintenance of the app for multiple OS...)
3. Finding the API client for Wikipedia and querying the data, keeping track of the changes in the API
4. Parsing and cleaning the data
5. Constructing the word cloud
6. Formatting the results: a picture of the cloud, a table view of the underlying words, a gexf network format for the underlying network of relations?
7. An interface to export the results: showing the picture on screen, downloading the picture in different formats (svg, png?), exporting to Excel and Google Sheets, visualize the word cloud in an interactive way with Gephi Lite, VOSviewer online or a custom D3 view, export a gexf or GraphML to be opened by Gephi or NodeXL?
8. Maintaining steps 1 to 7 through time 😅.

I believe that relatively big for-profit organizations have a motive and the resources to handle these 8 steps all by themselves (even then, they rely and contribute to open source solutions for parts of the process!)

For smaller organizations (for profit or not) and individuals, there is a strong case to join forces when and if possible, to help each other on one or several steps of the process above.

# I go first: what I am happy to help with 🤗

The list below are functional blocks that I can relatively easily provide to you, in a format that suits your needs.

## Tools

- methods to [extract words](https://github.com/seinecle/umigon-tokenizer) and [n-grams](https://github.com/seinecle/umigon-ngram-ops) from a given text
- methods to convert [co-occurring words into a network of words](https://github.com/seinecle/cowo-function)
- methods to infer the [sentiment from a text](https://github.com/seinecle/umigon-family/tree/main/umigon-core)
- methods to [detect key topics in text](https://github.com/seinecle/topics-detection-function)

## Interfaces

-  you are free to add your method to [https://nocodefunctions.com](https://nocodefunctions.com)
-  we can work at interfacing your app and nocodefunctions.com

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

I am happy to work on these interfaces with you.

Let's get in touch, either privately ([analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)) or let's discuss pubblicly on [Twitter](https://twitter.com/seinecle) or [Mastodon](https://ioc.exchange/@seinecle).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

