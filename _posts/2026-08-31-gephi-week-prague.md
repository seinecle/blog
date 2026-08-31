---
layout: post
title: "Gephi week 2026 in Prague - impressions!"
permalink: /gephi-week-2026-prague/
published: true
date_readable: August 31, 2026
last_modified_at_readable: August 31, 2026
categories: [gephi, community, AI, coding, open source]
---
[Gephi](https://gephi.org) is the leading desktop platform for the visualization and exploration of large graphs. It is free and open-source.
It has a [web version](https://lite.gephi.org) and a [headless (programmatic) version](https://gephi.org/toolkit/) as well.

The "Gephi week" is the annual retreat organized by and for the core contributors of Gephi (devs or not).
This year it took place in Prague, Czech Republic (Aug 24-27) and it was again a rich experience.
My participation was made possible thanks to the support of my employer, [Gobelins Paris](https://www.gobelins.fr/).

We were kindly hosted by [professor Eva Luef](https://explorer.cuni.cz/person/1876309743579605?lang=cs) at Charles University, who provided  beautiful office space on the [Hybernska campus](https://www.kampushybernska.cz/en), very arty and "maker" in spirit.
Most pics kindly provided by our dev and photographer [Matthieu Totet](https://matthieu-totet.fr/) 🙏:

<img width="2326" height="1550" alt="Prague building" src="https://github.com/user-attachments/assets/9d66b578-ac99-489d-9795-1d821da8de49" />
<img width="2048" height="1536" alt="Gephi week Prague" src="https://github.com/user-attachments/assets/9f86ffd3-72e3-40a0-9cdc-2c3d33a98c04" />
<img width="2325" height="1550" alt="Gephi week Prague" src="https://github.com/user-attachments/assets/ad4de111-bc04-4908-a024-ea5b66aa26af" />
<img width="2400" height="1600" alt="Hybernska campus" src="https://github.com/user-attachments/assets/89ee750b-b038-48b6-82af-7bea6ff9208d" />
<img width="1600" height="2400" alt="Filming tutorials" src="https://github.com/user-attachments/assets/80b36d87-c5b4-4586-86dd-b4c407967b1e" />
<img width="2400" height="1600" alt="Hybernska campus" src="https://github.com/user-attachments/assets/430aae28-a459-4f0c-952c-25c0f7a5ef90" />

Mathieu Bastian, the architect of Gephi, was also our local guide, and that helped us discover great places to relax, chat and enjoy the Czech cuisine.

<img width="2400" height="1600" alt="_Q9A4399" src="https://github.com/user-attachments/assets/985ac2f4-8196-4ca5-a246-507bb581c8ff" />

Rather than going through the detailed schedule, I’ll choose a couple of side angles that struck me particularly.

# Gephi 0.11: a beautiful release

Gephi has many advantages, one of them being that it offers very practical exploration tools **on large graphs**.
What is "a large graph"?

On a laptop, Gephi used to be able to handle graphs of 10,000 nodes and edges easily (and that is already quite a feast).
It could also handle graphs ten time this size, but that required some patience because basic operations became very slow.
Zooming, panning, and especially changing the layout of the graph: you could go and grab a coffee before the rendering was complete.

The new viz engine released in May 2026 with [Gephi version 0.11](https://gephi.wordpress.com/2026/05/05/gephi-0-11-major-performance-upgrade-and-new-features/) makes it effortless to handle graphs the size of hundreds of thousands of nodes, and millions of edges 🥹.
Wow.
You can move such a huge graph with a click and drag of the mouse, instantly.
Just look at this graph comparing it with the previous viz engine:

<img width="2537" height="1437" alt="perf comparison, Gephi 0.10 and 0.11" src="https://github.com/user-attachments/assets/b3df0b33-4b22-4304-9a35-14ee6b10c8c0" />

This release in Spring 2026 was the result of a work of several years by the core developers of Gephi (clarification: not my role!).

As a consequence, the Gephi week of 2026 felt to me like a major hurdle had just been cleared, and the perspectives for the future of the software felt comparatively easier and comfortable. We could consolidate and polish, on solid grounds.

# The group grows in experience

Roughly the same group of participants attends the Gephi week each year.
Over time, we get to know each other pretty well in this context, even if we actually rarely meet in person.

The way I experienced it, I knew form the start where I could make distinctive contributions, and who I could turn to for specific questions on Gephi code internals, frontend matters, tooling, the latest news in the community, and so forth.

Given that the week was a bit short for me (just Monday to Wednesday), this helped me make the very best of those 3 days.

# AI? Yes, that had an impact

Gephi is a very large and sophisticated desktop + web-based software development project supported by a small group volunteers - there is no one employed full or part time on it.

Hence, maintaining such a mammoth with limited human resources has always been a challenge.
Late August 2026, we are definitely in a better place in this regard.
AI is such a cognitive aid in all domains that I felt we could finally do things without rushing like crazy during the week. 

Using AI can be a controversial topic depending on which environment you are in, so I'll just speak for myself.
Here is what I was able to do in three days:

- [style cleaning](https://github.com/gephi/gephi/pull/3253) of the code for the Force Atlas algorithm, which is arguably Gephi's core graph layout. Not a super advanced task but one that can be pretty brittle - you don't want to break what has worked for the last 15 years.
- maintenance of the tutorials on [how to develop Gephi plugins](https://github.com/gephi/gephi-documentation/pull/13)
- maintenance of the [tutorials for the Gephi Toolkit](https://github.com/gephi/gephi-documentation/pull/14)
- maintenance of the [Gephi Toolkit demos](https://github.com/gephi/gephi-toolkit-demos/pull/18)
- working prototype of a Gephi plugin that allows a user to [control Gephi with ChatGPT or Claude](https://github.com/seinecle/gephi-plugins-word-cloud/tree/feature/text2gephi/modules/Text2Gephi) (hat tip to [Matt Artz](https://www.mattartz.me/software/gephi-ai/), who created such a project first and on whose work I piggybacked).
- and that still left me the time to participate in the filming of 10 video tutorials (short capsules) thanks to [Nicolas](https://www.linkedin.com/in/nicolasbouchaib/), take part in discussions about the direction of Gephi on Monday, hear about Mathieu Jacomy's semantic networks on Wednesday morning and attend a seminar on Wednesday afternoon.

My contributions are useful but relatively minor compared to, for instance, the project to develop an "undo button" for Gephi.
But since everyone in the core team of contributors enjoys the same increase in productivity, the needle has really moved for Gephi (again, not everyone present was keen on using this capability).

# Meeting the community
We were hosted by Professor Luef and her team and, while we were left alone to work during the first few days, we met for a seminar on Wednesday afternoon with presentations by colleagues and students who use Gephi in their academic research.

<img width="2048" height="1536" alt="phonological networks" src="https://github.com/user-attachments/assets/ea688ee6-fc15-48ee-a83c-79d64028958e" />

<img width="2048" height="1536" alt="phonological networks" src="https://github.com/user-attachments/assets/bc9a2275-5a76-428b-aeee-f2212a1b50c0" />


Interacting directly with members of the community provided great insights: use cases can never be fully anticipated and they often create a bit of a surprise. I remember:

- using Gephi to model attackers and defenders as a directed graph (attack is an edge pointing to the attackee). Sounds obvious and with lots of potential, but I personally had never thought of this use case.
- the need that the portion of the graph currently selected (by pointing the mouse on it) remains highlighted in the exported image, for better readability.
- the need to clarify that Force Atlas is probably the better performing algorithm in the family of force-based algorithms.
- not super surprising but interesting to see it exemplified: discussions about how the logic of community detection and force-base layouts parallel each other, but not perfectly and what to do about it.

# Next steps
The new viz engine, the stability of the core team, the relief that AI provides for small teams of developers, and the size and generosity of the community of Gephi users: all that makes me confident Gephi has bright days ahead.
Enjoy exploring your graphs!

---

## About Me

I lead higher-education programs in interactive design and video games at Gobelins Paris, and I develop independent web applications.

I created [Nocode Functions](https://nocodefunctions.com), [SlideLang](https://slidelang.com) and [new projects](https://posermesvalises.fr/). Try them out and let me know what you think. I'd love your feedback!

The views expressed here are my own and do not necessarily reflect those of my employer or any organization with which I am affiliated.

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on AI, coding, and higher education.
