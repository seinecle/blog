---
layout: post
title: Detecting the voice of the customer
permalink: /voice-of-the-customer/
published: true
date_readable:               Jul 6, 2023
last_modified_at_readable:   Jul 6, 2023
---

A new function is now available: identify the voice of the customer

# Filtering out content that has a "sponsored / commercial" tone, to identify the voice of the customer

At the very beginning of my work on [sentiment analysis](https://nocodefunctions.com/umigon/sentiment_analysis_tool.html), I was struck by the fact that most of the positive tweets I collected were simply some promoted content written by brands or communication agencies.

So I thought: surely, analysts and academic researchers have designed procedures to remove this content, before they measure the sentiment of a corpus of tweets?
Otherwise what is measured is not the "genuine" voice of the customer (in a business context), and it is very much tainted by stakeholders who publish positive things, just to push an agenda for their (commercial) interest.

As it turns out, there is no library or service that I know of which does this preprocessing / cleaning step. So I made a prototype of such a function.

# How does it work?
First, you can try it on the [homepage of nocodefunctions](https://nocodefunctions.com), or on the dedicated [page for the detection of promoted content](https://nocodefunctions.com/organic/organic_listening_voice_of_customer_tool.html).
Let me know what you think!

It works in the simplest way: the premise is that promoted content doesn't sound natural.
For the fans of the TV series Friends, I remember this episode where Phoebe works at a massage chain.
The receptionist, who addresses Rachel then Phoebe, keeps adopting a formal, commercial tone with them - which sounds weird given the relatively informal settings:

[![Watch the video](https://img.youtube.com/vi/IDDKr_W08WU/default.jpg)](https://youtu.be/IDDKr_W08WU)

Similarly, a piece of text which has been written by a corporate agent or someone set to promote a service or product, will probably be phrased in a way that doesn't feel natural.
These unnatural phrasings are captured through simple lists. That's it?
These lists are public, see [the one for English](https://github.com/seinecle/umigon-lexicons/blob/main/src/main/resources/net/clementlevallois/umigon/heuristics/lexicons/en/9_commercial%20tone.txt) and [the one for French](https://github.com/seinecle/umigon-lexicons/blob/main/src/main/resources/net/clementlevallois/umigon/heuristics/lexicons/fr/9_commercial%20tone.txt).

# See it in action:

![image](https://github.com/seinecle/blog/assets/1244100/4cecca50-280d-45a7-99dd-ccc727996969)

As you see, we benefit from the fact that the underlying logic is made entirely transparent and interpretable thanks to the approach we chose: the decision is explained entirely, in plain language.

# Next steps
The function is at the embryonic stage. If you are interested in it, get in touch (see below) to participate!
For it to perform adequately, we need much bigger lists of expressions that would signal a "non-natural" discourse.
As the function is using the same underlying logic as the one for sentiment analysis, it can leverage the fact that the terms included in the list can be supplemented by heuristics: simple rules assessing basic facts about the context where the word is being used.
See the full list of available [conditions / heuristics there](https://github.com/seinecle/umigon-lexicons/tree/main/src/main/java/net/clementlevallois/umigon/heuristics/booleanconditions).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

