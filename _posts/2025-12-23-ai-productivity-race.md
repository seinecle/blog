---
layout: post
title: "Coding productivity and AI: it's the tool, not the model"
permalink: /ai-coding-productivity-race/
published: false
date_readable: December 23, 2025
last_modified_at_readable: December 23, 2025
categories: [ai,productivity,cursor,claude,llm,antigravity,netbeans,ide]
---

# Since LLMs are more clever, cheaper by the day and available on tap...
... we would be swimming in virtually infinite intelligence to assist in any of our projects.
Creativity and time, not our coding skills, would become the limit to what we can accomplish.

This is the popular meme reflecting the merry-go-round of weekly improvements of AI models:

<img width="640" height="614" alt="image" src="https://github.com/user-attachments/assets/b67de1e8-941e-4bd1-a8b4-8d0510fd7e0c" />

(other versions of this meme do include Anthropic's Claude, if you wonder)

Productivity for AI assisted coding would be increasing steadily, driven by this endless cycle. We benefit from a race to the bottom of [costs](https://epoch.ai/data-insights/llm-inference-price-trends) and [hallucination rates](https://github.com/vectara/hallucination-leaderboard), with constantly new heights for [task completion duration](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) and [overall performance](https://www.linkedin.com/posts/emollick_no-signs-of-an-end-to-rapid-gains-in-ai-ability-activity-7407157959958351873-9Y1h).

In practice though, tooling comes in the way.

# Tooling: an essential layer

Making use of generative AI in a coding task is actually not straightforward. Here are some essential milestones in the short history of tools that have been evolved to ease this process.

| # | Name | Owning company | First public release | Interface type | Key features (1 line) | Cost model |
|---|------|----------------|----------------------|----------------|-----------------------|------------|
| 1 | [GitHub Copilot](https://en.wikipedia.org/wiki/GitHub_Copilot) | GitHub (Microsoft) | 2021 | IDE extension (VS Code, JetBrains…) | Inline code completion and chat powered by LLMs | Subscription (individual / business) |
| 2 | [Cursor](https://en.wikipedia.org/wiki/Cursor_(code_editor)) | Anysphere | 2022 | Stand-alone IDE | AI-native IDE with conversational editing across the codebase | Freemium + subscription |
| 3 | [Aider](https://aider.chat/) | Open source (community) | 2023 | CLI | Git-aware conversational code editing from the terminal | Free (API usage paid separately) |
| 4 | [Zed](https://zed.dev/ai) | Zed Industries | 2024 | Stand-alone IDE | High-performance collaborative editor with built-in AI agents | Freemium + paid AI features |
| 5 | [ChatGPT Canvas](https://openai.com/fr-FR/index/introducing-canvas) | OpenAI | 2024 | Web UI (chat interface) | Editable documents and live frontend rendering inside chat | Freemium + ChatGPT Plus / Team |
| 6 | [Gemini Canvas](https://blog.google/products/gemini/gemini-collaboration-features) | Google | 2025 | Web UI (chat interface) | Collaborative canvas with live code and document rendering | Included in Gemini Advanced plans | 
| 7 | [Claude Code](https://claude.com/product/claude-code) | Anthropic | 2025 | CLI | Agent-based CLI for large-scale code refactoring (Claude only) | Paid (Anthropic API) |
| 8 | [Codex (CLI)](https://openai.com/fr-FR/codex/) | OpenAI | 2025 | CLI | Autonomous coding agents for repo-level tasks (OpenAI only) | Paid (usage-based) |
| 9 | [Antigravity](https://antigravity.google/) | Google | 2025 | Stand-alone IDE | AI-first IDE integrating agents, refactors, and repo-level reasoning | Free for a limited period. Likely subscription (enterprise-oriented) |

Each of these tools come with various features, pricing models, degrees of vendor lock-in, and maturity. They all try to reduce the friction in AI assisted coding.
From the coder's perspective, the paradox is that learning / adopting / rejecting / switching between these tools is a productivity drain. This can actually slow down a project before the productivity gains of using AI assisted coding actually gets visible. So the "infinite cycle of model improvement" shown above is paralleled by a 

# Exploration and adoption of AI tools: a cost inducing process

My own journey is illustrative of the tortuous, time consuming process of exploration and learning costs associated with the adoption of new tools:

* 2010-2022: [NetBeans](https://netbeans.apache.org/front/main/index.html) only. Very happy with it.
* 2023: NetBeans + copy pasting of code snippets in Claude and ChatGPT. Feels weird and broken to resort to Ctrl+C and Ctrl +V
* 2024: same as 2023. Weak attempts at exploring [Jeddict](https://plugins.netbeans.apache.org/catalogue/?id=103), a plugin for LLM assistance integrated in NetBeans. I did not adopt it because copy pasting to Claude, Gemini and ChatGPT is more flexible.
* 2025
   1. (Spring): still copy pasting code in Gemini, Claude and ChatGPT. Using the new canvas features of Gemini and ChatGPT to render / edit frontend files. This causes friction with my tech stack because I code with xhtml files, not html files. That obliges me to do some manual and AI assisted file edits between the two formats.  
   2. (Summer): bored by the copy pasting. I heard of Cursor of course but the 20$ monthly subscription makes me hesitate, as I already spend 20$ for OpenAI and 20$ for Gemini. So I try  [Aider](https://aider.chat/), a free and open source solution to finally have in-place AI assisted editing of my files. Far from good enough, I stop it.
   3. (Fall): tried [Zed](https://zed.dev/ai). Free just like Aider, the results are disappointing: slow and imprecise.
   4. (Fall): fed up with the broken process of previewing my xhtml files as html files in the canvases. [I change my tech stack](https://nocodefunctions.com/blog/jsf-primefaces-vs-htmx-alpine-tailwind/) largely because of that.
   5. (Fall): tried [Cursor](https://en.wikipedia.org/wiki/Cursor_(code_editor)). Fantastic results. I virtually stop coding in NetBeans and use it only to launch services and test them in debugging mode.
   6. (Winter): Cursor has troubles interacting with the services I launch: it can't properly read their error logs and integrate them back in the conversation to iterate further. I've read that Claude Code does it very well. I'll try it asap. The only issue is that Claude Code is not Windows friendly yet, so I must switch to a Linux based development environment to adopt it (this swith to Linux is overdue of course but that's a different story). 

As can be seen from the above, I have changed from a 13-year period of complete stability in tool use to a period of rapid exploration and trial and error.
This is me as a solo developer, I can't imagine what the process looks like at the scale of an organization. My guess is that:

- in large organizations, teams will stick with their traditional IDE and just wait for it to evolve or for useful plugins for AI assistance to appear. Switching costs are just too high.
- in medium / agile organizations, teams will switch to Cursor (many already have). Switching *again* to Claude Code is a bridge too far, and in any case Claude Code is too strong a vendor lock-in. They'll wait a couple of months for Cursor to catch up to Claude Code.
- and companies that have a strong connivence with Anthropic, or the solo devs like myself who have very low switching costs, will try Claude Code.

So the profusion of AI assisting tools gives this picture:

<img width="2112" height="2016" alt="Gemini_Generated_Image_4uuoi64uuoi64uuo" src="https://github.com/user-attachments/assets/eec559d6-27a6-4d8c-ba97-54b8882b9793" />



---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
