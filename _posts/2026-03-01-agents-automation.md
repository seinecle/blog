---
layout: post
title: "Piloting Claude and Gemini on Debian from Signal"
permalink: /claude-gemini-on-debian-from-signal/
published: true
date_readable: March 01, 2026
last_modified_at_readable: March 01, 2026
categories: [ai,productivity,coding,development,claude code,gemini CLI,signal,devops,debian,SSH]
---

I document the rapid evolution of tooling for my web app, [nocodefunctions.com](https://nocodefunctions.com).
The previous steps are documented in [From NetBeans to Claude Code (Jan 2026)](https://nocodefunctions.com/blog/from-netbeans-to-claude-cursor/).

In early January, I had left my coding environment in this configuration, which was great:

- one single Debian server for dev and prod
- Claude Code installed on it
- I connect on SSH to it, from my local Windows machine
- in the terminal (Putty), I "vibe code" the development of my web app
- I can also SSH to my server directly from [my Android phone using ConnectBot](https://nocodefunctions.com/blog/from-netbeans-to-claude-cursor/#january-2026-the-third-tipping-point): effectively coding while on a metro ride.

# 2 frustrations
This setup served me well, but I hit some real limits:

## 1. Coding from the terminal on the phone is OK but not fantastic
Sending instructions to Claude from a mobile with ConnectBot is not a great experience.
The app connects to the server so this is a terminal interface, and on a mobile phone there are some keys (arrows, escapes, tabs...) that are not readily available, necessitating to install an app with a more advanced keyboard on the phone.
In the end the experience is OK but not comfortable.
Here is how it looks:

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=UjBZaKcTeIY&t=1805" target="_blank" rel="noopener noreferrer">
    <img src="https://github.com/user-attachments/assets/475fa4aa-2357-4165-b4d3-5925fdee8419" alt="Connectbot on Android" style="max-width: 100%; width: 360px; height: auto;">
  </a>
</div>


## 2. Claude: token rate limits every 5 hours and every week
Vibe coding increases productivity for sure, and it comes with token spending. I became regularly blocked by the 5-hour token reset period imposed by Claude.
The weekly limit on token consumption was also looming large. I am on the 20\$ / month plan with Claude, and didn't want to jump to the 90\$ or 200\$ plan. The situation became very frustrating


# The solutions! ✨

## 1. Adding Gemini CLI to the server!
Google's most visible product to compete with Cursor or Claude is [AntiGravity](https://antigravity.google/) and so I had missed that Google has released a CLI version of Gemini (since summer 2025 as per [this Github repo](https://github.com/google-gemini/gemini-cli)).

Anyway, if I am limited by Claude's token limit, why not use the token allowance I have from my Gemini subscription? (20$ / month). Installing Gemini CLI on the server is straightforward.

At first, I switched between Claude and Gemini : launching one when the other's limit was reached.
If you wonder, Gemini 3.1 pro is good enough to work with on code.
It is at the same level as Claude sonnet or opus.
Gemini's other models are insufficient.

But then I thought naturally...

## 2. Getting Claude and Gemini to coordinate their efforts!
It is natural to try the next step: getting Claude, Gemini, and possibly other forthcoming CLI agents to coordinate their efforts on tasks I submit to them.

To create this, I started a conversation with Gemini to devise a plan. My entire prompt was:

```
On my debian server I installed in 2026 both Claude Code and Gemini CLI with flags to bypass human confirmation . I created scripts and md files so that they should coordinate work when I formulate a task to accomplish . works great.
only issue is that when one is finished on a set of subtasks, it returns to the command line and wait for my instructions. there is no mechanism for it to detect that the other has written down new subtasks in the md file to be picked up now.
how to solve that? i would love that I first give them both a general task, and then they remain active on it. they would also send their remarks, questions, progress reports... in a centralized place where I could then answer (to both at the same time) 
```

Gemini provided a simple plan, that I then asked my 2 agents (Claude and Gemini) on debian to implement.
It works great now, mostly through a mix of shared .md files where both agents report their progress and pick up instructions to work on the next steps.

## 3. Using the web then Signal to improve my comfort as an orchestrator!
Since I left the comfort of using an IDE like NetBeans (2010-2025) then Cursor (November-December 2025), working in the terminal with Claude and Gemini is not so bad, but is not entirely comfortable either. Especially, as I explained above, when connecting on the terminal from my phone, things get really tiny and typing messages is not super easy.

First thing I did was asking the agents to create a web page interface: a page that I could double tap to edit it, so that I could monitor progress and add tasks directly in the text. They found a Python lib for that:

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=UjBZaKcTeIY&t=1805" target="_blank" rel="noopener noreferrer">
    <img src="https://github.com/user-attachments/assets/a84ab09e-adef-46a3-808b-61c58af7531a" alt="web interface for agents coordination" style="max-width: 100%; width: 460px; height: auto;">
  </a>
</div>

Not bad at all. Then I remembered that levelsio / Pieter Levels had mentioned his use of Telegram to pilot his agents:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">✨ A dream I had finally came true: I can now chat directly with my sites to build any feature or fix any bug just via Telegram<br><br>I&#39;ve been playing with OpenClaw for 3 weeks now and it&#39;s great but I was always too scared to run it on any production server<br><br>And I was right a bit as… <a href="https://t.co/pfQf6EMKOd">pic.twitter.com/pfQf6EMKOd</a></p>&mdash; @levelsio (@levelsio) <a href="https://twitter.com/levelsio/status/2023960543959101938?ref_src=twsrc%5Etfw">February 18, 2026</a></blockquote>

I don't personally like or use Telegram, and I would have preferred WhatsApp or Signal. Turns out WhatsApp is not fit for this purpose, and Signal has a [community-supported CLI](https://github.com/AsamK/signal-cli) that fits the need. Claude and Gemini implemented that in an hour or two.

Done: I can now send instructions to my agents (Claude and Gemini) directly from Signal, either from my phone or from my Windows laptop (where Signal is installed as a desktop app). I can even attach pics to the message. Typically, screenshots of my web app to show them what I mean in terms of layout, when there is a defect or when I want an improvement.

# Money, money, money
No extra money spent here. I continue with my existing 20\$ Claude and 20\$ Gemini subscriptions. It' just that their token allowances are better spent now.

# Next steps
Thanks to these agents, I could develop 2 new functions that I wanted to develop for a long time:

## pdf or web pages to social graph

[Try it there](https://nocodefunctions.com/nergraph/nergraph.html)

Provide a pdf or a url, and the function will return the social graph of the persons mentioned in the document.

It works already pretty well. Here is the graph created from the phd of [my PhD dissertation](https://theses.hal.science/tel-00372263v1), that explored the relations between economics and biology in post-war US:

➡️ [interactive version available here](https://dev.nocodefunctions.com/user_created_files/vosviewer/index.html?json=public/vosviewer_5432624604758149090.json)

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=UjBZaKcTeIY&t=1805" target="_blank" rel="noopener noreferrer">
    <img src="https://github.com/user-attachments/assets/bf1d31c1-b08d-4ab4-90f7-df9b52927e65" alt="example of my phd thesis turned into a social graph" style="max-width: 100%; width: 460px; height: auto;">
  </a>
</div>


## Wiki social graph

Same, but with Wikipedia: pick a domain or provide a name, and the function will crawl wikipedia to return a social graph around this domain or name. [Try it there](https://nocodefunctions.com/wikinergraph/wikinergraph.html).


These 2 functions now need to be further tested and improved. Your feedback is welcome. I also have other ideas in store.

--- 
# About Me

I'm an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a point-and-click tool for exploring texts and networks. Try it out and let me know what you think. I'd love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
