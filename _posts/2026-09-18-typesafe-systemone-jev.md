---
layout: post
title: "Jev - not your usual breakthrough model"
permalink: /typesafe-jev-systemone-RLCD/
published: true
date_readable: September 18, 2026
last_modified_at_readable: September 18, 2026
categories: [AI, RLCD, RLHD]
---
## A model worth your time
Jev is a new model that came out 2 days ago ([Sept 15, 2026](https://typesafe.ai/blog/introducing-system-one-models-and-jev)).

(this post started as a draft on Sept 17).

It is a highly unusual kind of model and I expected it to make the headlines even in the general press, but it didn't.
It trended on [Hacker News for a day or two](https://news.ycombinator.com/item?id=49717558). Conversations are flaring on X but that's about it.

The model is worth making bigger headlines because:

- 😱 it is ~100 times cheaper than one of the best models of OpenAI
- 💣 it responds in milliseconds, not seconds or dozens of seconds. That is 40x to 200x quicker than other models
- 🔥 responses come with a score of confidence. This provides a degree of certainty in the answers, which is absent in LLM models

## What are the use cases?

Typesafe lists use cases [on their website](https://docs.typesafe.ai/concepts/use-case-map), and here are the ones I tested with success:

### 1st use case: "Poser mes valises"
[Poser mes valises](https://posermesvalises.fr) is a website that I created in August, during the crazy hot summer.
Discussions with friends and family could quickly take an anxious turn: "even Brittany [famous for being wet and cold] is actually becoming unbearably hot!".
So where in France would be a good place to live?

> [!IMPORTANT]  
> The answer is a map where you can apply a series of filters, showing regions that meet your criteria.

The tool includes the search for practical aspects of where to live: proximity to supermarkets because you might still need them, schools if you have kids, proximity to a general hospital if you retire and prefer to be close to health services, etc.

<img width="515" height="760" alt="image" src="https://github.com/user-attachments/assets/75e19339-135b-4baa-92e6-b71e10bd2aed" />

The website uses a classic user interface: buttons and sliders to apply the filters. **With Jev, I experimented with a conversational interface instead:**

1. The user writes their preferences in natural language (example below),
2. **The text is sent to Jev**, with the following instruction: detect in the text the mention or absence of criteria that are available in the tool: schools, hospitals, geological risks, etc.
3. For each criteria detected in the text written by the user, the corresponding filters are applied and the map updates to reflect these.

Using Jev for that is very simple, at near zero cost and with near perfect accuracy.


I didn't finish the development so it doesn't work on all available criteria / filters yet, but [you can try it there](https://posermesvalises.fr/labs/system-one/?inactiveDefaults=&exploration=0&journeys=0&care=0&air=0&references=0).

(try it with "Je veux vivre près du littoral mais avec un faible risque d'inondations", for instance).

<img width="250" height="400" alt="image" src="https://github.com/user-attachments/assets/8810f999-2eb6-4a4f-a5dd-3bd3f89a4112" />

**How does it beat an LLM?**

- Cost: it is 100x cheaper to send a request to Jev
- Simplicity: Jev makes a potentially complex task simple. With an LLM, I would have had to design / engineer / the fact that I expect scores of confidence on each criteria. I would have had to test extensively the correct implementation of these scores. I would have had to search LLM models which actually handle structured responses. Jev just handles all that natively, and again: much more cheaply, and much faster.

### 2nd use case: "Entourages"
[Entourages](https://nocodefunctions.com/entourages/) is a social network of people in France who have a page on Wikipedia.

While retrieving the pages of people living or working in France is relatively easy, **tracing the connections between any two persons is not straightforward**.

<img width="955" height="445" alt="image" src="https://github.com/user-attachments/assets/4ff21afb-bf4c-41cf-8d3c-82c5f3f43b6c" />

Earlier in 2026, I had tried using LLMs to analyze the content of a Wikipedia bio and spot people of significance, and how they relate to each other. **Results with LLMs were costly so not scalable, with imperfect results, and with a high effort in development.**

**With Jev**: the task consists simply in sending a given Wikipedia page to Jev, with the request to spot the names on it that score high on one of these possibilities: family members, mentor / mentored, co-author relationship, long time collaboration, etc.

The result is astonishingly accurate, fast to get and cheap. It took me less than 3 days and less than 20$ to reconstruct a network which, as of Sept 27, comprises 12k persons and close to 6k connections.


## Jev: only for software developers?
X / Twitter and Hacker News are raging about Jev, but not much elsewhere. [Simon Willison](https://simonwillison.net/) and [Ethan Mollick](https://www.oneusefulthing.org/) who are 2 important relays for significant AI novelties to academia and other spheres have not yet blogged about Jev, AFAIK.

This weekend (so a week after the release of Jev), the [Financial Times](https://www.ft.com/content/456884ea-2558-4648-8036-a77b73733430?syn-25a6b1a6=1) has published an article on it [which supports my case to students that reading the FT (at least the weekend edition) is an excellent investment for their time!]

Anyway, the FT correctly characterizes Jev as a tool for software developers, not end users. Right, but: today, the barrier to develop software has lowered dramatically. Teenagers do it, employees do it, etc. So there is a case to be made, I believe, that a large crowd (really not just IT) should get acquainted with the kind of development that Jev represents.

Go and try Jev!

---

## About Me
I am [Clement Levallois](https://clementlevallois.net) and I lead higher-education programs in interactive design and video games at Gobelins Paris.
I also develop independent web applications to learn, have fun and be of service if I can.

I created [Nocode Functions](https://nocodefunctions.com), [SlideLang](https://slidelang.com), [poser mes valises](https://posermesvalises.fr/) and [entourages](https://nocodefunctions.com/entourages/). Try them out and let me know what you think. I'd love your feedback!

The views expressed here are my own and do not necessarily reflect those of my employer or any organization with which I am affiliated.

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on AI, coding, and higher education.
