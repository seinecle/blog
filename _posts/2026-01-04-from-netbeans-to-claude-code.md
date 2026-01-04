---
layout: post
title: "From NetBeans to Claude Cursor"
permalink: /from-netbeans-to-claude-cursor/
published: false
date_readable: January 04, 2026
last_modified_at_readable: January 04, 2026
categories: [ai,productivity,coding,development,netbeans,vibe coding,cursor,claude,devops,ide]
---

This blog post to document the rapid evolution of tooling for my web app, developped in Java. I'll keep it short but will highlight how "tooling" co-evolved with the tech stack and the wider environment for developing.

# 2010-2025: NetBeans all the way
- **Code editor, refactoring, Git interface, debugger, maven builds and executions**: all from inside NetBeans
- **front end**: JSF + Primefaces
- **back end**: JakartaEE
- **microservices**: Javalin
- **OS for dev**: Windows
- **OS for prod**: Debian
- **AI assisted coding**: copy-pasting to ChatGPT and Gemini
- **tests**: none

# Summer and Fall 2025: removal of Primefaces, JSF and JakartaEE. htmx + Javalin all the way
It happened in these logical steps:

1. I want to improve the UI of my app, but Primefaces makes it hard to customize CSS. What if I removed Primefaces and styled JSF components myself directly? ChatGPT enables me to do so now.
2. But JSF components sit in .xhtml files, which can't be previewed in ChatGPT's canvas. The back and forth of copy pasting between NetBeans and ChatGPT's canvas, all while adapting xhtml to html and vice and versa: what a drag! (I actually spent some time doing that).
3. Do I really need these JSF components after all or [could I just go with native html with htmx to ease the interaction with JakartaEE](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/)? Yes, probably so! Let's go htmx + alpine for the front.
4. But if I don't use JSF for the front, do I still need JakartaEE? Maybe that [Jakarta MVC](https://jakarta.ee/specifications/mvc/) would suffice? Let's go for this slimmer version.
5. But wait: is it *that hard* to manage user sessions, to the point of necessitating an entire framework mainly for that? I could try to learn with ChatGPT how to handle user sessions with Javalin. CSRF and all that.
6. I ended up removing JakartaEE entirely and using Javalin all the way for my backend.

# November 2025: the tipping point
At this point my coding practice relied extensively on copy pasting code to ChatGPT or Gemini for advice on how to do this or that, and for entire rewrites from a JakartaEE logic to a Javalin one.
It become so impractical and silly. I had to zip entire folders of relevant source code to attach it as a context for the conversational interface to reason correctly about my problem. It worked! But the alternative was obvious: what if an AI tool could edit my source files directly on my laptop, exploring the context as needed. Instead of me copy pasting my code in a browser - so silly.

Of course I had heard of Cursor. But the 20$/month made me hesitate because my coding project is a side project with zero revenue, and I was already at:

- 20$ / month for Gemini
- 20$ / month for ChatGPT
- 50$ / month for server costs for nocodefunctions (yes that's a big server)

I had tried free equivalents to Cursor, namely [aider](https://aider.chat/) and [Zed](https://zed.dev/ai), which turned out to be disappointing. Eventually I caved in to Cursor and coughed up 20$ extra / month for a Cursor subscription.

And... woooosh. Cursor is in a different category. You ask, it codes. Correctly, and across the code base. It just works. I was so glad that my recent rearchitecturing contributed to that: htmx + Javalin is so simple that it helps the models reason effectively on the code.

In my latest blog post I noted that one problem is solved, we get nagged by another one. With excellent coding, I become  


--- 
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
