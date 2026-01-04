---
layout: post
title: "From NetBeans to Claude Cursor"
permalink: /from-netbeans-to-claude-cursor/
published: false
date_readable: January 04, 2026
last_modified_at_readable: January 04, 2026
categories: [ai,productivity,coding,development,netbeans,vibe coding,cursor,claude,devops,ide]
---

I document the rapid evolution of tooling for my web app, with a focus on Java. I highlight how changes in “tooling” co-occurred with an evolution of my tech stack and the wider development environment.

That's the opening scene: my coding environment as a solo Java web developer over the last 15 years (look Ma, no JetBrains!).

# 2010–2025: NetBeans all the way
- **Code editor, refactoring, Git interface, debugger, Maven builds and executions**: all from inside NetBeans
- **Frontend**: JSF + PrimeFaces
- **Backend**: Jakarta EE
- **Microservices**: none at first, then Javalin since 2022
- **OS for dev**: Windows
- **OS for prod**: Debian
- **DevOps**: PuTTY, [WinSCP](https://winscp.net/eng/download.php) (and pushing to Git from NetBeans)
- **AI-assisted coding**: since 2023, copy-pasting code into ChatGPT and Gemini
- **Tests**: none

# Summer and Fall 2025: removing PrimeFaces, JSF, and Jakarta EE — htmx + Javalin all the way
This happened through a series of logical steps (the first ones are retraced in a [previous post](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)):

1. I wanted to improve the UI of my app, but PrimeFaces makes CSS customization painful. What if I removed PrimeFaces and styled JSF components directly? ChatGPT would help a lot.
2. But JSF components live in `.xhtml` files, which can't be previewed in ChatGPT's canvas. The constant back-and-forth-copy-pasting between NetBeans and ChatGPT, adapting XHTML to HTML and vice versa was a drag (and I did spend time doing it).
3. Do I really need JSF components at all, or [could I just use native HTML with htmx to interact with Jakarta EE](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)? Probably yes. Let's go htmx + Alpine on the frontend.
4. But if I don't use JSF, do I still need Jakarta EE? Maybe [Jakarta MVC](https://jakarta.ee/specifications/mvc/) would suffice? Let's try the slimmer option.
5. But wait: why keep Jakarta MVC at all? If it's mainly for session management, does that justify an entire framework? I could learn via ChatGPT how to manage sessions directly in Javalin (CSRF and all).
6. I ended up removing Jakarta EE entirely and using Javalin end-to-end for the backend.

# November 2025: the tipping point
At this stage, I was no longer relying on JSF or Jakarta EE: a break from 15 years of habits! I now depended heavily on copy-pasting code into ChatGPT or Gemini for advice, and for full rewrites from Jakarta EE logic to Javalin.

It became so impractical. I was zipping entire source folders just to give enough context to a conversational interface. **It worked**, but it was silly.

The obvious alternative: what if an AI could edit my source files directly on my machine, exploring the context as needed, without browser copy-paste gymnastics?

I had heard of Cursor, but the $20/month made me hesitate. This is a side project with zero revenue, and I was already paying:
- $20/month for Gemini
- $20/month for ChatGPT
- $50/month for server costs (yes, that's a big server)

I tried free alternatives: [aider](https://aider.chat/) and [Zed](https://zed.dev/ai), and found them disappointing. Eventually, I caved and added another $20/month for Cursor.

And… whoosh. Cursor is in a different category. You ask, it codes correctly, across the codebase. It just works. My recent re-architecture helped: htmx + Javalin is simple enough that models reason effectively over it.

My workflow changed radically in a few weeks:
- giving instructions to Cursor
- keeping NetBeans open to check compiler errors, stop microservices, rebuild and relaunch
- copy-pasting error traces into Cursor and asking it to “fix it”
- virtually no hand coding 😮

Yes, vibe coding. Did I miss manual coding? Not at all. I enjoy focusing on architecture and design decisions instead of minute implementation details.

But after a few weeks, another friction appeared: why manually copy error traces, or stop/restart services, if Cursor already has access to my machine?

# December 2025: the second tipping point
Yes, two tipping points in two months.

Just like for Cursor, I had seen very positive feedback about Claude Code. So I posted a [question on Hacker News](https://news.ycombinator.com/item?id=46185230), asking whether Claude Code was meaningfully different or better than Cursor. The replies were few but very positive, even with this direct comparison with Cursor.

So during the Christmas break, I spent another $20/month on Claude Code 😭. After the change I had lived with Cursor and that I thought were huge already, it forced me to change 15 years of habits:

- **From Windows to Linux for development.** I couldn't get Claude Code working on Windows (my fault probably, and I can't install WSL on my machine), so I installed it on my Debian server and effectively moved my codebase there. Psychologically difficult: I'm not an IT-trained developer, and "Windows for dev, Linux via PuTTY for prod" already felt geeky enough*. Going full Linux felt risky. But it worked out.
- **NetBeans became irrelevant.** I now use [Cursor over SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) to connect to Claude on the server. Cursor can show and edit files, but I rarely do manual edits.

Claude Code delivers: with proper guidelines it can stop, rebuild, and restart my microservices; read logs and use them as context; navigate directories; grep, sed, push: whatever is needed. Contrary to Cursor it takes full advantage of having access to the file system and the command line. Friction is almost gone. I give instructions; they get executed. It writes tests (so does Cursor to be fair), which was a sore point in my practice.

# January 2026: the third tipping point
(Sorry for the exaggeration but it really felt like it.)

A few days ago, I remembered an Android SSH app I had installed years ago and never used. Could I "vibe code" on the go?

Yes. Easily.

I now do it for real. The setup was trivial. I test results directly on my phone browser on the [dev version of nocodefunctions.com](https://dev.nocodefunctions.com/) (certificate warnings for now, add an exception). When something breaks, I report it to Claude, ask for a fix, and keep walking.

# Money, money, money
Spending $80/month on AI-assisted coding is not sustainable for me:
- I downgraded ChatGPT from Plus ($20) to Go ($4), since I no longer use it for coding.
- I cancelled Cursor.

# Next steps
As I wrote earlier, switching tooling (even shiny AI tooling) is initially a [productivity drain](https://nocodefunctions.com/blog/ai-coding-tool-productivity-paradox/). Since this summer, I've been in near-constant tooling transition, eating up the few weekly hours I have for this project.

So I hope Google's *antigravity* will flop and won't justify another switch away from Claude Code :-) That way, I can finally focus on better UI, better UX, and new features for nocodefunctions.com.

\* Thanks to [Miguel Biraud](https://bsky.app/profile/mgilbir.bsky.social) for introducing me to PuTTY and Linux back then. Your help was transformative.

--- 
# About Me

I'm an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a point-and-click tool for exploring texts and networks. Try it out and let me know what you think. I'd love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
