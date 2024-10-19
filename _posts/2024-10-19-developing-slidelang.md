---
layout: post
title: Developing slidelang, a translator for slides
permalink: /developing-slidelang/
published: false
date_readable:               Oct 19, 2024
last_modified_at_readable:   Oct 19, 2024
categories: [chatgpt,llm,development,slidelang]
---
This is a very short blog post about [slidelang](https://alpha.slidelang.com/), a new app I am developing.

# What is slidelang?
It is an app that translates Powerpoint documents.

# Why did I start developing it?
Because as a professor, I needed to translate a Powerpoint presentation containing my course on data science and AI, that contains ~ 300 slides. I found no solution on the market to do it.

# But DeepL, Google Translate... do it already?
Not for my need:

|| [DeepL](https://www.deepl.com/fr/pro)    | [Google translate](https://support.google.com/translate/answer/2534559?ref_topic=7011659&hl=en) |  [slidelang](https://alpha.slidelang.com/) |
| --------| --------| -------- | ------- |
|Max size|30 Mb 😲 |10 Mb 😲 |no limit 😄|
|Max number of translations per month| 100  | ?    | no limit    |
|Price| $50 / month | free     |  free for now   |
|Uses your data to train their models?|no | unclear (probably yes)     |  no   |
|Preserves layout| yes    | yes    | yes    |
|Quality of translation|excellent    |excellent    |excellent    |

# How does it work?
The translation is managed by calls to the OpenAI API. The preservation of the layout is achieved with a complex programmatic process that I designed.

# Is it going to stay free?
No so enjoy it now! I'll create plans that are super cheap compared to what DeepL offers.

# Next
[slidelang](https://alpha.slidelang.com/) is available, up and running. I develop it slowly but surely, aiming to add amazing, useful features. Coming first: translation of Google Slides, OpenOffice formats.

# About me
I am academic and independent web app developer. Besides slidelang, I build [nocode functions](https://nocodefunctions.com) 🔎, a free click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing my apps.
