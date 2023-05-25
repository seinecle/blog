---
layout: post
title: Speeding up pairwise comparisons in Java on a regular laptop
permalink: /optimizing-pairwise-comparisons-java/
published: false
date_readable:               May 25, 2023
last_modified_at_readable:   May 25, 2023
---

*Notes on coding strategies to speed up pairwise comparisons on the elements of a collection*

It started at 140,000 comparisons per second and ended up at 3 million / seconds

# Context / goal / hardware

➡ *Context*

This is part of a project to build maps of science, similar to this one:

![Rafols, Porter and Leydesdorff, (2010), "Science overlay maps: a new tool for research policy and library management"](https://github.com/seinecle/MapsOfScience/blob/main/assets/img/rafols-porter-leydesdorff-2010.png)

Th project is live streamed every Wednesday at 3pm (Paris time) [there on Twitch](https://twitch.tv/clementlevallois) and is made [fully open on Github](https://github.com/seinecle/MapsOfScience).


➡ *Goal*

Using OpenAlex data, I retrieve **20 million** journal articles, from which I extracted the journal name and author ids, resulting in a **65Gb json file**.
I transformed this into a list where each entry is a journal with all the authors who published in it. There are **200,000 journals** and with the list of their authors this fills a **0.9Gb file**.

Now the goal is to compute the **similarity between each pair of journals**, "similarity" being measured as the number of authors that jointly published in both.

**This makes 2 billion pairs to evaluate**: 200,000 x 200,000 divided by 2 (because when we compared journal A to B, no need to compare journal B to A again).

➡ *Hardware and stack*

It is a conscious decision not to go for clusters, GPUs and cloud infrastructure where possible, in order to lower the barrier of entry for those who would like to contribute or just fork and run the project by themselves.

In this spirit, so far the project needs:
- a laptop with 8Gb of RAM
- Java installed
- continuous access to the Internet for a period of ~ 24h to retrieve the data from [OpenAlex](https://openalex.org/) (one time operation).

which means:
- no server, no database, no GPU, no framework.


# Methods and results

## Handling Longs, not Strings
Journal ids and authors ids are represented as a String by OpenAlex, but most of the String is just a url, the actual identifier is a Long Integer at the end of the url.

Hence, the first trivial operation consisted in reducing the String ids to Longs.

# Using the Fastutil library to handle Longs in a memory efficient way, as primitive "long"
It



# About me

I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
