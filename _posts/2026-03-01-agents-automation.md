---
layout: post
title: "Piloting Claude and Gemini on Debian from Signal"
permalink: /clauyde-gemini-on-debian-from-signal/
published: false
date_readable: March 01, 2026
last_modified_at_readable: March 01, 2026
categories: [ai,productivity,coding,development,claude code,gemini CLI,signal,devops,debian,SSH]
---

I document the rapid evolution of tooling for my web app, [nocodefunctions.com](https://nocodefunctions.com).
The previous steps are documented in [From NetBeans to Claude Code (Jan 2026)](https://nocodefunctions.com/blog/from-netbeans-to-claude-cursor/).

# January 2026: vibe coding with Claude Codeon Debian
In early January, I had left my coding environment in this configuration, which was great:

- one single Debian server for dev and prod
- Claude code installed on it
- I connect on SSH to it, from my local Windows machine
- in the terminal (Putty), I "vibe code" the development of my web app
- I can also SSH to my server directly from [my Android phone using ConnectBot](https://nocodefunctions.com/blog/from-netbeans-to-claude-cursor/#january-2026-the-third-tipping-point): effectively coding while on a metro ride.

# 2 frustrations
This setup served me well, but I hitted some real limits:

## 1. Coding from the terminal on the phone is OK but not fantastic
Sending instructions to Claude from a mobile with ConnectBot is not a great experience.
The app connects to the server so this is a terminal interface, and on a mobile phone there are some keys (arrows, escapes, tabs...) that are not readily available, necessitating to install an app with a more advanced keyboard on the phone.
In the end the experience is OK but not comfortable.
Here is how it looks:

<img width="945" height="2048" alt="image" src="https://github.com/user-attachments/assets/475fa4aa-2357-4165-b4d3-5925fdee8419" />

## 2. Claude : token rate limits every 5 hours and every week
Vibe coding increases productivity for sure, and it comes with token spending. I became regularly blocked by the 5-hour token reset period imposed by Claude.
The weekly limit on token consumption was also looming large. I am on the 20$ / month plan with Claude, and didn't want to jump to the 90$ or 200$ plan. The situation became very frustrating


# The solutions! ✨

## 1. Adding Gemini CLI to the server!
Google's most visible product to compete with Cursor or Claude is [AntiGravity](https://antigravity.google/) and so I had missed that Google has released a CLI version of Gemini (since summer 2025 as per [this Github repo](https://github.com/google-gemini/gemini-cli)).

Anyway, if I am limited by Claude's token limit, why not use the token allowance I have from my Gemini subscription? (20$ / month). Installing Gemini CLI on the server is straightforward.

At first, I switched between Claude and Gemini : launching one when the other's limit was reached.
If you wonder, Gemini 3.1 pro is good enough to work with on code.
It is at the same level as Claude sonnet or opus.
Gemini's other models are insufficient.

But then I thought naturally...

## 2. Getting Claude and Gemini to coordinate their efforts
It is natural to try the next step: Claude, Gemini, and possibly other forthcoming CLI agents, to coordinate their efforts on tasks I submit to them.

To create this, I started a conversation with Gemini to devise a plan. My entire prompt was:

```
On my debian server I installed in 2026 both Claude code and Gemini CLI with flags to bypass human confirmation . I created scripts and md files so that they should coordinate work when I formulate a task to accomplish . works great.
only issue is that when one is finished on a set of subtasks, it returns to the command line and wait for my instructions. there is no mechanism for it to detect that the other has written down new subtasks in the md file to be picked up now.
how to solve that? i would love that I first give them both a general task, and then they remain active on it. they would also send their remarks, questions, progress reports... in a centralized place where I could then answer (to both at the same time) 
```

Gemini provided a simple plan, that I then I asked my 2 agents (Claude and Gemini) on debian to implement.
It works great now, mostly through a mix of shared .md files where both agents report their progress and pick up instructions to work on the next steps.

## 3. Using the web then Signal to improve my comfort as an orchestrator
Since I left NetBeans then Cursor, working in the terminal with Claude and Gemini is not so bad, but is not entirely comfortable either. Especially, as I explained above, when connecting on the terminal from my phone.

First thing I did was asking the agents to create a web page interface where I could add tasks and monitor progress. 

<img width="3817" height="1948" alt="image" src="https://github.com/user-attachments/assets/a84ab09e-adef-46a3-808b-61c58af7531a" />

Not bad at all. Then I remembered that levelsio / Pieter Levels had mentioned his use of Telegram to pilot his agents:



# Summer and Fall 2025: removing PrimeFaces, JSF, and Jakarta EE — htmx + Javalin all the way
This happened through a series of logical steps (the first ones are retraced in a [previous post](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)):

1. I wanted to improve the UI of my app, but PrimeFaces makes CSS customization painful. What if I removed PrimeFaces and styled JSF components directly? ChatGPT would help a lot.
2. But JSF components live in `.xhtml` files, which can't be previewed in ChatGPT's canvas. The constant back-and-forth-copy-pasting between NetBeans and ChatGPT, adapting XHTML to HTML and vice versa was a drag (and I did spend time doing it).
3. Do I really need JSF components at all, or [could I just use native HTML with htmx to interact with Jakarta EE](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)? Probably yes. Let's go htmx + Alpine on the frontend.
4. **But if I don't use JSF, do I still need Jakarta EE?** Maybe [Jakarta MVC](https://jakarta.ee/specifications/mvc/) would suffice? Let's try the slimmer option.
5. But wait: why keep Jakarta MVC at all? If it's mainly for session management, does that justify an entire framework? I could learn via ChatGPT how to manage sessions directly in Javalin (CSRF and all).
6. I ended up removing Jakarta EE entirely and using Javalin end-to-end for the backend.

# November 2025: Cursor, the tipping point
At this stage, I was no longer relying on JSF or Jakarta EE: a break from 15 years of habits! I now depended heavily on copy-pasting code into ChatGPT or Gemini for advice, and for full rewrites from Jakarta EE logic to Javalin.

It became so impractical. I was zipping entire source folders just to give enough context to a conversational interface. **It worked, but it was silly.**

The obvious alternative: what if an AI tool could edit my source files directly on my machine, exploring the context as needed, without browser copy-paste gymnastics?

I had heard of Cursor, but the $20/month made me hesitate. This is a side project with zero revenue, and I was already paying:
- $20/month for Gemini
- $20/month for ChatGPT
- $50/month for server costs (yes, that's a big server)

I tried free alternatives: [aider](https://aider.chat/) and [Zed](https://zed.dev/ai), and found them disappointing. Eventually, I caved and added another $20/month for Cursor.

**And… whoosh. Cursor is in a different category.** You ask, it codes correctly, across the codebase. It just works. My recent re-architecture helped: htmx + Javalin is simple enough that models reason effectively over it.

My workflow changed radically in a few weeks:
- giving instructions to Cursor
- keeping NetBeans open to check compiler errors, stop microservices, rebuild and relaunch
- copy-pasting error traces into Cursor and asking it to “fix it”
- virtually no hand coding 😮

Yes, vibe coding. Did I miss manual coding? Not at all. I enjoy focusing on architecture and design decisions instead of minute implementation details.

But after a few weeks, another friction appeared: why manually copy error traces, or stop/restart services, if Cursor already has access to my machine?

# December 2025: Claude Code
Yes, two tipping points in two months.

Just like for Cursor, I had seen very positive feedback about Claude Code. So I posted a [question on Hacker News](https://news.ycombinator.com/item?id=46185230), asking whether Claude Code was meaningfully different or better than Cursor. The replies were few but very positive, even with this direct comparison with Cursor.

So during the Christmas break, I spent another \$20/month on Claude Code 😭. After the change I had lived with Cursor and that I thought were huge already, it forced me to change 15 years of habits:

- **From Windows to Linux for development.** I couldn't get Claude Code working on Windows (my fault probably, and I can't install WSL on my machine), so I installed it on my Debian server and effectively moved my codebase there. Psychologically difficult: I'm not an IT-trained developer, and "Windows for dev, Linux via PuTTY for prod" already felt geeky enough*. Going full Linux felt risky. But it worked out.
- **Not using NetBeans or an IDE to code** I now [connect over SSH with Cursor](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) to connect to Claude on the server. Cursor can show and edit files, but I rarely do manual edits.

Claude Code delivers: with proper guidelines it can stop, rebuild, and restart my microservices; read logs and use them as context; navigate directories; grep, sed, push: whatever is needed. Contrary to Cursor it takes full advantage of having access to the file system and the command line. Friction is almost gone. I give instructions and they get executed. It writes tests (so does Cursor to be fair), which was a sore point in my practice.

# January 2026: the third tipping point
(Sorry for the exaggeration but it really felt like it.)

A few days ago, I remembered [ConnectBot](https://play.google.com/store/apps/details?id=org.connectbot), an Android SSH app I had installed years ago and never used. **Could I "vibe code" on the go?**

Yes. Easily.

I now do it for real. The setup was trivial. I can test results of my feature additions directly on the browser of my phone by visiting the [dev version of nocodefunctions.com](https://dev.nocodefunctions.com/) (ssl certificate warnings for now, add an exception). When something breaks, I report it to Claude, ask for a fix, and keep walking.

# Money, money, money
Spending \$80/month on AI-assisted coding is not sustainable for me:
- I downgraded my ChatGPT subscription from "Plus" (\$20) to "Go" (\$4), which is sufficient since I no longer use it for coding.
- I cancelled Cursor.

# Next steps
As I wrote earlier, switching tooling (even shiny AI tooling) is initially a [productivity drain](https://nocodefunctions.com/blog/ai-coding-tool-productivity-paradox/). 

Since this summer, I've been in near-constant tooling transition, eating up the few weekly hours I have for this project.

So I hope [Google's antigravity](https://antigravity.google/) will flop and won't justify another switch away from Claude Code :-) That way, I can finally focus on better UI, better UX, and new features for nocodefunctions.com.

\* Thanks to [Miguel Biraud](https://bsky.app/profile/mgilbir.bsky.social) for introducing me to PuTTY and Linux back then. Your help was transformative.

--- 
# About Me

I'm an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a point-and-click tool for exploring texts and networks. Try it out and let me know what you think. I'd love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
