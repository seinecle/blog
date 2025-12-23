---
layout: post
title: "The AI productivity race in coding"
permalink: /ai-productivity-race/
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

Productivity for AI assisted tasks would be increasing steadily, driven by this endless cycle. We benefit from a race to the bottom of [costs](https://epoch.ai/data-insights/llm-inference-price-trends) and [hallucination rates](https://github.com/vectara/hallucination-leaderboard), with constantly new heights for [task completion duration](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) and [overall performance](https://www.linkedin.com/posts/emollick_no-signs-of-an-end-to-rapid-gains-in-ai-ability-activity-7407157959958351873-9Y1h).

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

# Exploration and adoption of AI tools: a long process

My own journey is illustrative of the tortuous, time consuming process of exploration and learning costs associated with the adoption of new tools:

* 2010-2022: [NetBeans](https://netbeans.apache.org/front/main/index.html) only. Very happy with it.
* 2023: NetBeans + copy pasting of code snippets in Claude and ChatGPT.
* 2024: same as 2023. Weak attempts at exploring [Jeddict](https://plugins.netbeans.apache.org/catalogue/?id=103), a plugin for LLM assistance in NetBeans. I did not adopt it because copy pasting to Claude, Gemini and ChatGPT is faster, easier.
* 2025
   1. (Spring): still copy pasting code in Gemini, Claude and ChatGPT. Using the new canvas features of Gemini and ChatGPT to render / edit frontend files.
   2. (Summer): bored by the copy pasting. I heard of Cursor of course but the 20$ monthly subscription makes me hesitate, as I already spend 20$ for OpenAI and 20$ for Gemini. SO I try  [Aider](https://aider.chat/), a free and open source solution to finally have in-place AI assisted editing of my files. Far from good enough, I stop it.
   3. (Fall): tried [Zed](https://zed.dev/ai). Freee just like Aider, the results are disappointing: slow and imprecise.
   4. (Fall): tried [Cursor](https://en.wikipedia.org/wiki/Cursor_(code_editor)). Fantastic results. I virtually stop coding in NetBeans and use it only for its debugger.
   5. (Winter): will try Claude Code. The reason is that Cursor has troubles interacting with the services I launch: it can't properly read their error logs and integrate them back in the conversation to iterate further. I've read that Claude Code does it very well.

As can be seen from the above, I have changed from a 13-year period of complete stability in tool use to a period of exploration and trial and error.
This is me as a solo developer, I can't imagine what the process looks like at the scale of an organization. My guess is that:

- in large organizations, teams will stick with their traditional IDE and just wait for it to evolve or for useful plugins for AI assistance to appear. Switching costs are just too high.
- in medium / agile organizations, teams will switch to Cursor (many already have). Switching *again* to Claude Code is a bridge too far, and in any case Claude Code is too strong a vendor lock-in. They'll wait a couple of months for Cursor to catch up to Claude Code.
- and companies that have a strong connivence with Anthropic, or the solo devs like myself who have very low switching costs, will try Claude Code.





---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
