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

- **architecture**: MVC but very loose. The "controller" of each function is a big spaghetti code in one large JakartaEE backend.
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

Of course I had heard of Cursor but for a side project with zero revenue I was alreay at:

- 20$ / month for Gemini
- 20$ / month for ChatGPT
- 50$ / month for server costs for nocodefunctions (yes that's a big server)

But I caved in and coughed up 20$ extra / month for a Cursor subscription.

And... woooosh. 

   1. (Spring): still copy pasting code in Gemini, Claude and ChatGPT. Using the new canvas features of Gemini and ChatGPT to render / edit frontend files. This causes friction with my tech stack because it makes use of xhtml files, not html files. That obliges me to do some manual and AI assisted file edits between the two formats.  
   2. (Summer): bored by the back and forth between .xhtml and .html formats, and by the copy pasting. I heard of Cursor of course but the 20\$ monthly subscription makes me hesitate, as I already spend 20\$ for OpenAI and 20$ for Gemini (plus my server costs etc). So I try  , a free and open source solution to finally have in-place AI assisted editing of my files. Far from good enough, I don't adopt it.
   3. (Fall): I try , a kind of free and open source Cursor. The results are disappointing: slow and imprecise.
   4. (Fall): fed up with the broken process of previewing my xhtml files as html files in the canvases. [I change my tech stack](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/) largely because of that. The copy pasting continues.
   5. (Fall): I finally have a try at [Cursor](https://en.wikipedia.org/wiki/Cursor_(code_editor)). Fantastic results. I virtually stop coding in NetBeans and use it only to launch services and test them in debugging mode. Big positive impact on my stack: I can remove a large framework (that I used for the last 10 years!) and I come back to a simpler code base.
* 2026: will try [Claude Code](https://claude.com/product/claude-code). Late 2025 I pushed Cursor to its limits by trying to make it interact with the services I launch: it can't properly read their error logs and integrate them back in the conversation to iterate further. I've read that Claude Code does it very well. [Claude's notion of 'skills' is also very promising](https://quesma.com/blog/claude-skills-not-antigravity/). The only issue is that Claude Code is not Windows friendly yet, so I must switch to a Linux based development environment to adopt it (<i><small>this switch to Linux is overdue of course but that's a different story</small></i>). 

As can be seen from the above, I have changed from a 13-year period of complete stability in tool use to a year exploration and trial and error. The opportunity cost is real: because I spent 2025 chasing the 'perfect' workflow, feature development on my primary app (nocodefunctions.com) essentially froze. I traded immediate output for a total architectural and workflow refactor. A new version of the app is [slowly emerging](https://next.nocodefunction.com), derived from a completely renewed code base.

This is me as a solo developer, I can't imagine what the process looks like at the scale of an organization which simply can't pause, stop or refactor things in such a way. My guess is that:

- in large organizations, teams will stick with their traditional IDE and just wait for it to evolve or for useful plugins for AI assistance to appear. Switching costs are just too high.
- in medium sized oganizations / startups, teams will switch to Cursor (many already have). Switching *again* to Claude Code is a bridge too far, and in any case Claude Code is too strong a vendor lock-in. They'll wait a couple of months for Cursor to catch up to Claude Code.
- and companies that have a strong connivence with Anthropic, or the solo devs like myself who have very low switching costs, will try Claude Code.

So the profusion of AI assisting tools gives this picture:

<img alt="The endless cycle of improvement of AI tools for coding" src="https://github.com/user-attachments/assets/eec559d6-27a6-4d8c-ba97-54b8882b9793" style="max-width: 100%; width: 460px; height: auto;"/>

*(source: generated by the author with Gemini)*

What looks like a tooling problem in software development is, in fact, an early signal of a much broader phenomenon.

## Not just coding: the broader lesson about reskilling
The story above shows that:

1. paradoxically, progress in AI can cause a temporary decrease in productivity because of the retooling it invites to do. Switching costs of all sorts are incurred and production has to slow or stop to make time for the exploration of these new tools. Discovery process, learning of the UI, evaluation...
2. retooling has strong bandwagon effects. New tools are not just about a "better or lower performance": they open new opportunities and have specific limits which invite to rethink the material that is worked on by the tool, and even aspects of the general environment where we are operating.
3. **it is not just a story about coding. The same is happening in visual creation, for example. Look at this list of [100+ tools for AI assisted visual creation](https://nocodefunctions.com/blog/list-of-ai-apps-for-visual-creation/) I maintain: it would be foolish to think that the potential of these tools is simply measurable in terms of "is the result better or worse, is productivity higher or lower?" Workflows, aesthetics, domains of expression, cost models, team work, methodologies, skillsets, pace of production, ... in a word, the entire domain and industry is turned upside down.**

## What to make of it?
This is a pretty long blog post to arrive at this simple conclusion: the endless competition between AI models providers can give the false impression that as professionals, we can rest in our armchairs and just wait and benefit from this continuous stream of improvements. This is a very false sense of comfort.

We are moving from an era of **tool mastery** (learning one type of instrument: an investment to be repaid over decades) to an era of **tool fluidity** (accepting to unlearn and reinvest in fundamentally new instruments, regularly). The competitive advantage is no longer just knowing how to master a set of professional skills, but how quickly one can integrate these skills in new AI-native workflows without breaking momentum.

From the perspective of a professional in higher education, this means that the often repeated:

> "we don't train our students for a particular tool, we train them in fundamental skills"

... has a renewed sense of relevance and urgency. Because in practice, we do tend to rely on the obvious workhorses of the trade. Just pick an IDE for coding, learn the Adobe Creative Cloud for visual creation, and choose Blender or Maya for 3D modelling - obviously, right? Well, it might be time for a rethink and train students in the art and craft of resetting their fundamental tooling suite on a regular basis.

In a world where tools now have a half-life measured in years, not decades, learning to retool quickly is no longer a support skill — it is a core professional competence.

--- 
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
