---
layout: post
title: "Productivity and AI: it's the tool, not the model"
permalink: /ai-coding-tool-productivity-paradox/
published: true
date_readable: December 23, 2025
last_modified_at_readable: December 23, 2025
categories: [ai,productivity,cursor,claude,llm,tools, tooling,antigravity,netbeans,ide]
---

Every week, a new "SOTA" (State of the Art) model is announced, promising higher reasoning capabilities and (often) lower costs. We could be led to think that we are entering an era of infinite, frictionless productivity. But the reality is messier. While the models are getting smarter, the gap between "intelligence on tap" and "completing a task" is managed by our tools and right now, that tooling interface is becoming a major source of friction.

As we will see, this isn’t just a developer’s dilemma in the context of new AI assisted coding interfaces. It is a preview of the "retooling tax" that every professional domain must soon learn to navigate.

The paradox is simple: as models improve, productivity bottlenecks increasingly shift away from intelligence itself and toward the tools that mediate access to it.

## The race for better models
This is the popular meme reflecting the merry-go-round of weekly improvements of AI models:

<img alt="The endless cycle of improvement of AI models" src="https://github.com/user-attachments/assets/b67de1e8-941e-4bd1-a8b4-8d0510fd7e0c" style="max-width: 100%; width: 460px; height: auto;"/>

*([source](https://www.reddit.com/r/singularity/comments/1ks0jrb/the_cycle_never_ends/). other versions of this meme do include Anthropic's Claude, if you wonder)*

LLMs become more capable, cheaper, and available on tap, to the point that the new best performing model can be indistinguishable from the previous one, simply because models are now so smart that the tasks we perform are not complex enough to clearly differentiate between "a great model" and an "even greater model": both perform equally well on the tests.

This is the experience of [Simon Willison](https://simonwillison.net/2025/Nov/24/claude-opus/) when testing a preview of Claude Opus 4.5 on November 24, 2025:

> It’s clearly an excellent new model, but I did run into a catch. My preview expired at 8pm on Sunday when I still had a few remaining issues in the milestone for the alpha [of his coding project]. I switched back to Claude Sonnet 4.5 and... kept on working at the same pace I’d been achieving with the new model. With hindsight, production coding like this is a less effective way of evaluating the strengths of a new model than I had expected. I’m not saying the new model isn’t an improvement on Sonnet 4.5—but I can’t say with confidence that the challenges I posed it were able to identify a meaningful difference in capabilities between the two.

This experience reflects that for some tasks, we have seemingly reached a plateau: models are already "clever enough". Model providers continue the race the bottom for [costs](https://epoch.ai/data-insights/llm-inference-price-trends) and [hallucination rates](https://github.com/vectara/hallucination-leaderboard), while constantly reaching new heights for [task completion duration](https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/) and [overall performance](https://www.linkedin.com/posts/emollick_no-signs-of-an-end-to-rapid-gains-in-ai-ability-activity-7407157959958351873-9Y1h).

From the user’s perspective, however, the experience still falls short of the promise of effortless productivity: intelligence may be abundant, but friction remains pervasive. I will illustrate this with the case of coding tasks, before returning to the broader picture.

## The tooling paradox
Making use of generative AI in a coding task is actually not as straightforward as just asking "solve this problem / respond to this difficult question" and then just collecting the answer.
Here are some essential milestones in the short history of tools that have been evolved to ease this process.

| # | Name | Owning company | First public release | Interface type | Key features (1 line) | Cost model |
|---|------|----------------|----------------------|----------------|-----------------------|------------|
| 1 | [GitHub Copilot](https://en.wikipedia.org/wiki/GitHub_Copilot) | GitHub (Microsoft) | 2021 | IDE extension (VS Code, JetBrains…) | Inline code completion and chat powered by LLMs | Subscription (individual / business) |
| 2 | [Cursor](https://en.wikipedia.org/wiki/Cursor_(code_editor)) | Anysphere | 2022 | Stand-alone IDE | AI-native IDE with conversational editing across the codebase | Freemium + subscription |
| 3 | [Aider](https://aider.chat/) | Open source (community) | 2023 | CLI | Git-aware conversational code editing from the terminal | Free (API usage paid separately) |
| 4 | [Zed](https://zed.dev/ai) | Zed Industries | 2024 | Stand-alone IDE | High-performance collaborative editor with built-in AI agents | Freemium + paid AI features |
| 5 | [ChatGPT Canvas](https://openai.com/fr-FR/index/introducing-canvas) | OpenAI | 2024 | Web UI (chat interface) | Editable documents and live frontend rendering inside chat | Freemium + ChatGPT Plus / Team |
| 6 | [Gemini Canvas](https://blog.google/products/gemini/gemini-collaboration-features) | Google | 2025 | Web UI (chat interface) | Collaborative canvas with live code and document rendering | Included in Gemini Advanced plans | 
| 7 | [Claude Code](https://claude.com/product/claude-code) | Anthropic | 2025 | CLI | Agent-based CLI introducing the notion of skills (Claude only) | Paid (Anthropic API) |
| 8 | [Codex (CLI)](https://openai.com/fr-FR/codex/) | OpenAI | 2025 | CLI | Autonomous coding agents for repo-level tasks (OpenAI only) | Paid (usage-based) |
| 9 | [Antigravity](https://antigravity.google/) | Google | 2025 (November)| Stand-alone IDE | AI-native IDE with conversational editing across the codebase. Direct competitor to Cursor. | Free for a limited period. Likely subscription (enterprise-oriented) |

Each of these tools come with various features, pricing models, degrees of vendor lock-in, and maturity. They all try to reduce the friction in AI assisted coding.

For the developer, the cognitive overhead of evaluating, adopting, and eventually abandoning these tools creates a 'productivity tax' that can temporarily outweigh the gains of the AI itself.

## Exploration and adoption of AI tools: a cost inducing process

My own journey using AI for coding is illustrative of the tortuous, time consuming process of exploration and learning costs associated with the adoption of new tools:

* 2010-2022: [NetBeans](https://netbeans.apache.org/front/main/index.html) only. Very happy with it.
* 2023: NetBeans + copy pasting of code snippets in Barde (now Gemini), Claude and ChatGPT. Feels weird and broken to resort to Ctrl+C and Ctrl +V but this is still very useful.
* 2024: same as 2023. Weak attempts at exploring [Jeddict](https://plugins.netbeans.apache.org/catalogue/?id=103), a plugin for LLM assistance integrated in NetBeans. I did not adopt it because copy pasting to Claude, Gemini or ChatGPT is more flexible.
* 2025
   1. (Spring): still copy pasting code in Gemini, Claude and ChatGPT. Using the new canvas features of Gemini and ChatGPT to render / edit frontend files. This causes friction with my tech stack because it makes use of xhtml files, not html files. That obliges me to do some manual and AI assisted file edits between the two formats.  
   2. (Summer): bored by the back and forth between .xhtml and .html formats, and by the copy pasting. I heard of Cursor of course but the 20\$ monthly subscription makes me hesitate, as I already spend 20\$ for OpenAI and 20$ for Gemini (plus my server costs etc). So I try  [Aider](https://aider.chat/), a free and open source solution to finally have in-place AI assisted editing of my files. Far from good enough, I don't adopt it.
   3. (Fall): I try [Zed](https://zed.dev/ai), a kind of free and open source Cursor. The results are disappointing: slow and imprecise.
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
3. **it is not just a story about coding. The same is happening in visual creation, for example. Look at this list of [100+ tools for AI assisted visual creation](https://nocodefunctions.com/blog/list-of-ai-apps-for-visual-creation/) I maintain: it would be foolish to think that the potential of these tools is simply measurable in terms of "is the result better or worse, is productivity higher or lower?" Workflows, aesthetics, domains of expression, cost models, team work, skillsets, pace of production, ... in a word, the entire domain and industry is turned upside down.**

## What to make of it?
This is a pretty long blog post to arrive at this simple conclusion: the endless competition between AI models providers can give the false impression that as professionals, we can rest in our armchairs and just wait and benefit from this continuous stream of improvements. We are moving from an era of **tool mastery** (learning one category of desktop app for a decade) to an era of **tool fluidity**. The competitive advantage is no longer just knowing how to code, but how quickly one can integrate a new AI-native workflow without breaking momentum.

From the perspective of a professional in higher education, this means that the often repeated:

> "we don't train our students for a particular tool, we train them in fundamental skills"

... has a renewed sense of relevance and urgency. Because in practice, we do tend to rely on the obvious workhorses of the trade. Just pick an IDE for coding, learn the Adobe Creative Cloud for visual creation, and choose Blender or Maya for 3D modelling - obviously, right? Well, it might be time for a rethink and train students in the art and craft of resetting their fundamental tooling suite on a regular basis.

In a world where tools now have a half-life measured in months, not decades, learning to retool quickly is no longer a support skill — it is the core of professional competence.

--- 
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
