---
layout: post
title: "From NetBeans to Claude Cursor"
permalink: /from-netbeans-to-claude-cursor/
published: false
date_readable: January 04, 2026
last_modified_at_readable: January 04, 2026
categories: [ai,productivity,coding,development,netbeans,vibe coding,cursor,claude,devops,ide]
---

I document the rapid evolution of tooling for my web app with a focus on Java. I will highlight how changes in "tooling" cooccurred with an evolution of my tech stack and the wider dev environment.

# 2010-2025: NetBeans all the way
- **Code editor, refactoring, Git interface, debugger, maven builds and executions**: all from inside NetBeans
- **front end**: JSF + Primefaces
- **back end**: JakartaEE
- **microservices**: Javalin
- **OS for dev**: Windows
- **OS for prod**: Debian
- **devops**: Putty, WinSCP (and pushing to Git from NetBeans)
- **AI assisted coding**: copy-pasting to ChatGPT and Gemini
- **tests**: none

# Summer and Fall 2025: removal of Primefaces, JSF and JakartaEE. htmx + Javalin all the way
It happened in these logical steps (the first ones were retraced in a [previous post](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)):

1. I want to improve the UI of my app, but Primefaces makes it hard to customize CSS. What if I removed Primefaces and styled JSF components myself directly? ChatGPT would help me greatly.
2. But JSF components sit in .xhtml files, which can't be previewed in ChatGPT's canvas. The back and forth of copy pasting between NetBeans and ChatGPT's canvas, all while adapting xhtml to html and vice and versa: what a drag! (I actually spent some time doing that).
3. Do I really need these JSF components after all or [could I just go with native html with htmx to ease the interaction with JakartaEE](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)? Yes, probably so! Let's go htmx + alpine for the front.
4. But if I don't use JSF for the front, do I still need JakartaEE? Maybe that [Jakarta MVC](https://jakarta.ee/specifications/mvc/) would suffice? Let's go for this slimmer version.
5. But wait: why do I keep Jakarta MVC? If that's because it manages user sessions, does it justify keeping an entire framework for that? I could try to learn with ChatGPT how to handle user sessions with Javalin. CSRF and all that.
6. I ended up removing JakartaEE entirely and using Javalin all the way for my backend.

# November 2025: the tipping point
At this point I did not rely on JSF nor JakartaEE - a break from 15 years of coding practice. To manage without, I relied now extensively on copy pasting code to ChatGPT or Gemini for advice on how to do this or that, and for entire rewrites from a JakartaEE logic to a Javalin one.
It became so impractical and silly. I had to zip entire folders of relevant source code to upload the zip as a context for the conversational interface to reason correctly about this or that coding problem. It worked! But the alternative was obvious: what if I could ask an AI interface to edit my source files directly on my laptop, leaving it to explore the context as needed. Instead of me copy pasting my code in a browser - so silly.

Of course I had heard of Cursor. But the 20$/month made me hesitate because my coding project is a side project with zero revenue, and I was already at:

- 20$ / month for Gemini
- 20$ / month for ChatGPT
- 50$ / month for server costs for nocodefunctions (yes that's a big server)

I had tried free equivalents to Cursor, namely [aider](https://aider.chat/) and [Zed](https://zed.dev/ai), which turned out to be disappointing. Eventually I caved in to Cursor and coughed up 20$ extra / month for a Cursor subscription.

And... woooosh. Cursor is in a different category. You ask, it codes. Correctly, and across the code base. It just works. I was so glad that my recent rearchitecturing contributed to that: htmx + Javalin is so simple that it helps the models reason effectively on the code. My coding practice changed radically in a few weeks:

- providing instructions to Cursor
- leaving NetBeans opened, verifying any compiler error. Stopping Javalin microservices, rebuilding and relaunching them to see if the code changes were correct
- copy pasting the error traces to Cursor, asking to "fix it" 

Yes, essentially vibe coding. Did I miss the manual coding input? Not at all. I love being now in charge of designing architecture principles and getting time to thing instead of implementing minute details.

But after a few weeks, I got nagged by something else. Why should I be slowed down by the manual copy pasting of error traces, and why the manual stop / rebuild / restart if Cursor has access to my machine?

# December 2025: the second tipping point
Yes, two tipping points in 2 months. That's how it felt:

Just like Cursor, I had seen some very positive comments on Claude Code. I posted a [question on hacker news](https://news.ycombinator.com/item?id=46185230). The few users who commented were very positive on Claude Code in a direct comparison to Cursor. Quite suggestive.

So during the Christmas break, I spent an extra 20$ / month on Claude Code 😭, and ... before all, it obliged me to change practices I had for the last 15 years:

- moving from Windows to Linux for development. Because I couldn't get Claude Code to work on Windows (my fault I guess. And I can't install WSL on my Windows machine), I had to install Claude Code on my Debian server and basically ended up moving my code base to my Linux server. This step was psychologically difficult because I am not a computer / IT student by training so "developing on Windows, just deploying on Linux with Putty" was the geekiest I thought I would be comfortable with*. Going full Linux felt I don't know, difficult and risky. But it went well in the end.
- not coding on Windows, NetBeans is now of no direct use. Feels weird not to open an IDE that you've used for the last 15 years. What I do instead is using [Cursor to SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) to my distant server. Cursor can show me the files and act as a text editor for them, but I rarely do. 

And Claude holds its promise: after spending some time setting up the proper guidelines, Claude Code can now stop, rebuild, restart the microservices that compose the backend of my web app. It can read their logs and include this info as context for the pursuit of the actions I set. It can easily navigate the directories or grep / ls / sed / push, as needed. Frictions have almost all disappeared. I can give instructions and they get executed perfectly.

# January 2026: the third tipping point
(sorry to exagerate but it felt like it).

A few days ago I remembered that I had installed an Android app on my phone, to SSH to my server and actually never used it. Could I use to "vibe code" on the go? Well yes, easily. I do that now, for real. The setup was very easy. I can test the results on my phone on the [dev version of nocodefunctions.com](https://dev.nocodefunctions.com/) (wrong certicates atm, don't worry and add an exception). When the feature doesn't work, I report it to Claude and ask for a fix. And continue to walk to my destination.

# Next steps
As I wrote just before, change for a better tooling (even an AI shiny one) is a [productivity drain in the first stages](https://nocodefunctions.com/blog/ai-coding-tool-productivity-paradox/). And in my case especially since this summer, I have been living a constant change of tooling, eating up the few hours I have per week on this side project. So I just hope that antigravity by Google will be a flop and won't justify a change from Claude Code :-) So that I can eventually develop a better UI, better UX and new and interesting functions for nocodefunctions.com


* thanks at the time to [Miguel Biraud](https://bsky.app/profile/mgilbir.bsky.social) for introducing me to Putty and Linux - your help was transformative!
--- 
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
