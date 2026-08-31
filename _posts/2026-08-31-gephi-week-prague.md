---
layout: post
title: "Gephi week 2026 in Prague - impressions!"
permalink: /gephi-week-2026-prague/
published: false
date_readable: August 31, 2026
last_modified_at_readable: August 31, 2026
categories: [gephi, community, AI, coding, open source]
---

Gephi week 2026 - my impressions!
A "Gephi week" is an annual retreat organized by and for the core contributors of Gephi, the open source software for network visualization.
This year it took place in Prague, Czech Republic (Aug 24-27) and it was again a rich experience.

The place contributed much to this success.
We were kindly hosted by [professor Eva Luef](https://explorer.cuni.cz/person/1876309743579605?lang=cs) at Charles University, who provided  beautiful office space on the [Hybernska campus](https://www.kampushybernska.cz/en), very arty and "maker" in spirit:



Mathieu Bastian who is the architect of Gephi was also our local guide, and that helped discover great places to relax, chat and enjoy the local cuisine.

To dive in the accomplishments of this week, I'll rather choose a couple of sideways angles that struck me particularly, rather than going through the detailed schedule.

# The group grows in experience

With variations, roughly the same group of persons attend the Gephi week every year.
Getting to know each other helps moving to the matter faster and distributing roles in an informal and efficient manner.

The way I lived it, I knew form the start who I could turn to for pinpointed questions on frontend, tooling, Gephi code internals, the latest news in the community, and so forth.

The week was a bit shorter for me - just Monday through Wednesday - but intense.

## AI changes everything

Gephi is a very large and sophisticated software development project supported by volunteers - there is no one employed full or part time on it.

Hence, maintaining such a mammoth with limited human resources has always been a nagging issue. Late August 2026, things have turned completely. AI is such a cognitive aid in all domains that I felt we could finally do things without rushing desperately. 

In a prompt interface, developers can research a bug or explore options for the development of a new feature. Then, let Claude or GPT smash the bug or develop the feature. Also, revise coding examples cited in the tutorials, migrate the documentation to the latest version of Gephi, perform a bit of front-end work, and write most if not all git commands to push these modifications to their Github repositories.

Using AI can be a controversial topic depending on which environment you are in, so I'll just speak for myself. Here is what I could do in three days:

- [style cleaning](https://github.com/gephi/gephi/pull/3253) of the code for the Force Atlas algorithm
- maintenance of the tutorials on [how to develop Gephi plugins](https://github.com/gephi/gephi-documentation/pull/13)
- maintenance of the [tutorials for the Gephi Toolkit](https://github.com/gephi/gephi-documentation/pull/14)
- maintenance of the [Gephi Toolkit demos](https://github.com/gephi/gephi-toolkit-demos/pull/18)
- working prototype of a Gephi plugin that allows a user to [control Gephi with ChatGPT or Claude](https://github.com/seinecle/gephi-plugins-word-cloud/tree/feature/text2gephi/modules/Text2Gephi) (hat tip to [Matt Artz](https://www.mattartz.me/software/gephi-ai/), who created such a project first and that I piggy backed).
- and that still left me the time to shoot 10 video tutorials (short capsules) thanks to [Nicolas](https://www.linkedin.com/in/nicolasbouchaib/)

These are useful but relatively minor contributions compared to, for instance, the project to develop an "undo button" for Gephi. But since everyone in the core team of contributors has the same x5 or x10 increase in productivity, the needle is really moving for Gephi. (again, not every one present whas keen on using this capability).
---

## About Me

I lead higher-education programs in interactive design and video games at Gobelins Paris, and I develop independent web applications.

I created [Nocode Functions](https://nocodefunctions.com) and [SlideLang](https://slidelang.com). Try them out and let me know what you think. I'd love your feedback!

The views expressed here are my own and do not necessarily reflect those of my employer or any organization with which I am affiliated.

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on AI, coding, and higher education.
