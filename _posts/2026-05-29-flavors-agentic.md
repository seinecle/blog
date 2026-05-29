---
layout: post
title: "Three flavors of agentic AI"
permalink: /three-flavors-agentic/
published: true
date_readable: May 29, 2026
last_modified_at_readable: May 29, 2026
categories: [ai,productivity,coding,development,agentic,agents]
---

A reasonable definition of an "AI agent" or "agentic coding" can be:

- a software process endowed with the capabilities of an LLM
- launched with instructions given at the start to accomplish a task
- which runs autonomously (no interactive session with a human), for a significant period of time
- with a non-deterministic behavior: the agent will adapt to the circumstances, hopefully without deviating from the instructions it received

These software processes (agents) can be launched in parallel to achieve faster results or to accomplish a larger number of tasks:  same process launched in multiple copies, or a variety of processes launched at once.

Not a necessity but logical next step: to accomplish a task, a process can be led to launch other processes, subprocesses, etc. This evokes images of cascades, armies, or swarms of agents coordinating in a decentralized manner (no human in the loop) to accomplish a task. 

Yet, in practice, "agents" is often used with no relation to the definition above. Possibly to sound up-to-date and sophisticated, "agents" might in reality designate a ChatGPT conversation where the user prompted "you are acting like a professional tax **agent** and in the following, I want you to help me fill in my tax declaration" 🤷‍♂️.

Pieter Levels, who tends to speak frankly about coding and AI matters, shared this feeling in summer 2025:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">If I hear people talk about &quot;AI agents&quot; these days it&#39;s generally a red flag and I know they&#39;re non-technical ppl reading AI news but not actually shipping anything<br><br>Not cause I don&#39;t believe in AI agents but it&#39;s such a marketing term with no real meaning at this point</p>&mdash; @levelsio (@levelsio) <a href="https://x.com/levelsio/status/1953125500492128766?ref_src=twsrc%5Etfw">August 6, 2025</a></blockquote>

**We are now approaching summer 2026, have things changed much?**

In my coding practice, I explored several ways to do agentic coding that would live up to the definition proposed above, and not masquerade for it.

Here are 3 flavors I tried:

# Flavor 1: launching multiple command line interfaces
I did that for a while:

- open an SSH session to my server
- launch [Codex CLI](https://developers.openai.com/codex/cli) in it
- ask GPT to accomplish a task just by writing a prompt describing the task
- open a second SSH session to my server
- launch [Codex CLI](https://developers.openai.com/codex/cli) in it
- ask GPT to accomplish another task just by writing a prompt describing the task
- rinse and repeat...

Honestly, that works pretty well. It is extremely low-tech as you can see. It also means you can launch [Claude Code](https://claude.com/fr/product/claude-code) in one session, Codex CLI in another, [Gemini CLI](https://geminicli.com/) in a third one... and hence spread your token consumption on several AI providers in parallel, which makes the token budget limit slower to hit for a given provider.

# Flavor 2: launching AI CLIs in headless mode
I used this second approach to write crawlers for 200+ different webpages. Obviously with 200 crawlers to create, that would have been too boring to do with the Flavor 1 described just above. ChatGPT guided me throughout on how to implement this new approach. The basic logic is:

- one json file containing the parameters for the 200 websites (urls and a few more details).
- one bash script (call it "A") that can launch one LLM in command line interface, in headless mode. Headless means that the LLM, once launched with the prompt you have given it, will execute until it has completed the task, without interrupting to ask you for permission or ask for feedback or a follow-up. For that I use the [`exec` flag on Codex CLI that triggers the headless mode](https://developers.openai.com/codex/noninteractive). Script A also contains the prompt that will be given to the LLM when it launches. The prompt is a piece of text with placeholders at key places, that will be replaced by the actual information related to a specific website to be crawled. The prompt basically asks the LLM to write a crawler for this website.
- another script (script "B") that picks 20 websites from the json file and executes script A for each of them. The placeholders of script A are replaced by the info of the website to be crawled, meaning that the crawler created by the LLM will be specific to this website.
- I launch script B, check that it works fine, then relaunch it with 20 other websites, etc. until I got 200 websites treated that way. 

Let me show you script A (script written by ChatGPT) to illustrate how this approach Flavor 2 involves more complexity than Flavor 1:

<details>
<summary><strong>Long script A — click to expand</strong></summary>

    #!/usr/bin/env bash
    set -euo pipefail
    
    ROOT="/home/xxx/backend"
    
    PACKAGE="${1:?missing package}"
    SOURCE_ID="${2:?missing source_id}"
    PLATFORM="${3:?missing platform}"
    URL="${4:?missing url}"
    LOCAL_GUARDRAIL="${CODEX_LOCAL_GUARDRAIL:-1}"
    
    PROMPT="$ROOT/ops/codex/prompts/${PACKAGE}-agent.txt"
    LOG_MD="$ROOT/reports/codex/logs/${PACKAGE}-agent.md"
    STDOUT_LOG="$ROOT/reports/codex/logs/${PACKAGE}-stdout.log"
    STDERR_LOG="$ROOT/reports/codex/logs/${PACKAGE}-stderr.log"
    
    echo "[$(date -Is)] preparing ${PACKAGE}"
    
    cat > "$PROMPT" <<EOF
    You are source_crawler_creator.
    
    Create or repair exactly one isolated direct-site crawler package.
    
    SOURCE_ID: ${SOURCE_ID}
    URL: ${URL}
    PLATFORM: ${PLATFORM}
    PACKAGE_NAME: ${PACKAGE}
    PACKAGE_PATH: src/main/java/com/xxx/directsite/crawling/sources/${PACKAGE}
    
    Writable paths:
    - src/main/java/com/xxx/directsite/crawling/sources/${PACKAGE}/**
    - src/test/java/com/xxx/directsite/crawling/sources/${PACKAGE}/**
    - src/test/resources/directsite/${PACKAGE}/**
    - reports/codex/source-results/${PACKAGE}.json
    - reports/codex/shared-change-requests/${PACKAGE}.md
    
    Read-only reference paths:
    - src/main/java/com/xxx/directsite/crawling/sources/estia/**
    - src/main/java/com/xxx/directsite/crawling/sources/groupeesa/**
    - src/main/java/com/xxx/directsite/crawling/sources/generic/**
    - src/main/java/com/xxx/directsite/crawling/sources/ats/**
    - src/main/java/com/xxx/directsite/crawling/sources/talentsoft/**
    - src/main/java/com/xxx/directsite/crawling/rules/**
    - src/main/java/com/xxx/directsite/crawling/CrawlerRegistry.java
    - src/main/java/com/xxx/directsite/crawling/DirectSiteCrawler.java
    - src/main/java/com/xxx/directsite/crawling/DirectSiteCrawlerSupport.java
    - src/main/java/com/xxx/directsite/crawling/sources/AGENTS.md
    - AGENTS.md
    - pom.xml
    
    Hard constraints:
    - Modify only the writable paths listed above.
    - Do not edit CrawlerRegistry.java.
    - Do not edit shared crawler classes, including ats and talentsoft reference packages.
    - Do not edit shared pipeline, shared DTOs, pom.xml, or AGENTS.md.
    - Do not touch any other source package.
    - If registration is required in shared code, do not make that shared change. Report it.
    - Keep crawl, parse, reconcile, and LLM enrichment concerns separate.
    - For platform-specific sources, inspect the existing platform package as a read-only reference and create only source-specific wrappers/specs if useful.
    
    Testing rules:
    - JUnit tests must not perform live network calls.
    - Use local fixtures under src/test/resources/directsite/${PACKAGE}/ for listing/detail HTML whenever practical.
    - Inline HTML/JSON is acceptable only for very small snippets.
    - Prefer behavior assertions over brittle exact cardinality unless the fixture is intentionally constructed for that cardinality.
    - Do not assert overly specific live data fields unless they are necessary to lock parser behavior.
    - If asserting URLs/titles from fixtures, treat them as fixture examples, not as proof that the live page still exists.
    
    Task:
    1. Inspect existing crawler patterns.
    2. Investigate the URL and determine xxx.
    3. Create or repair the dedicated ${PACKAGE} crawler package.
    4. Implement only source-specific crawling/parsing details in this package.
    5. Reuse shared rules/classes when applicable.
    6. Add narrow tests if practical.
    7. Run the narrowest useful Maven compile/test command.
    8. Write reports/codex/source-results/${PACKAGE}.json with:
    {
      "source_id": "${SOURCE_ID}",
      "package": "${PACKAGE}",
      "status": "created|repaired|blocked|needs_shared_change",
      "files_changed": [],
      "tests_run": [],
      "shared_change_requested": false,
      "notes": "..."
    }
    
    Final answer:
    - concise summary
    - files changed
    - tests run
    - whether shared change is needed
    EOF
    
    echo "[$(date -Is)] starting ${PACKAGE}"
    
    if [ "$LOCAL_GUARDRAIL" = "1" ]; then
      BEFORE_STATUS="$(mktemp)"
      AFTER_STATUS="$(mktemp)"
      git status --short --untracked-files=all > "$BEFORE_STATUS"
    fi
    
    codex exec \
      --cd "$ROOT" \
      --sandbox workspace-write \
      --model gpt-5.4 \
      --output-last-message "$LOG_MD" \
      - < "$PROMPT" \
      > "$STDOUT_LOG" \
      2> "$STDERR_LOG"
    
    if [ "$LOCAL_GUARDRAIL" = "1" ]; then
      git status --short --untracked-files=all > "$AFTER_STATUS"
    
      FORBIDDEN="$(
        comm -13 <(sort "$BEFORE_STATUS") <(sort "$AFTER_STATUS") \
          | cut -c4- \
          | grep -vE "^(\.codex/|ops/codex/|reports/codex/|src/main/java/com/xxx/directsite/crawling/sources/${PACKAGE}/|src/test/java/com/xxx/directsite/crawling/sources/${PACKAGE}/|src/test/resources/directsite/${PACKAGE}/)" || true
    )"
        if [ -n "$FORBIDDEN" ]; then
          echo "[$(date -Is)] FORBIDDEN FILE CHANGES for ${PACKAGE}:" >&2
          echo "$FORBIDDEN" >&2
          exit 42
        fi
    fi
    echo "[$(date -Is)] finished ${PACKAGE}"
</details>

This approach works well. It is not as easy as "launch script A, get 200 crawlers written in an hour" but almost that. If you are patient to read a bit the script above, you'll see that the LLM is tasked to write unit tests for each crawler it creates! As is normal, these tests don't always pass so that slow downs things a bit, but that's for the good cause since doing extra work to get passing tests means that the crawls will be more reliable.

With this approach, I expect to have my 200 hundred crawlers up and ready in the next few days, and with an easy path to grow to hundreds more.

# Flavor 3: having one LLM create and manage these subagents itself
Flavor 2 was really bash and unix heavy: this makes my processes harder to maintain. Why not have an LLM just spin off agents by itself, following my instructions? That's what every solution is advertising these days:

- Cursor invites you to ["delegate implementation to focus on higher-level direction"](https://web.archive.org/web/20260528201253/https://cursor.com/product)
- Codex has ["sub agents"](https://web.archive.org/web/20260524042439/https://developers.openai.com/codex/subagents) you can ochestrate
- Google's Antigravity offers to ["orchestrate multiple autonomous agents working in parallel across independent projects."](https://perma.cc/4S83-LRM3)
- Claude Code can create ["custom sub agents"](https://web.archive.org/web/20260528082943/https://code.claude.com/docs/en/sub-agents) for you.

 My opinion: probably, but not today. Asking one agent to delegate to sub-agents mean that you are 2 steps removed from the sub-agents. Inconsistencies, poor choices, flat errors... will be harder to catch. Interruption and resuming of work for a given sub agent is not straightforward. And you get solution dependent: my AI of choice these days is GPT 5.5, and that would be off limit if I choose a solution with agents that is not developed by its company, OpenAI.

> For these reasons and until proven otherwise, I'll stick with Flavor number 2 (and even number 1 in simple cases) described above.

# Do we even need agents?

Most of the time, *no*. Here is [Ethan Mollick](https://www.linkedin.com/in/emollick/) creating a complete, live web application with just one prompt and 4 follow-ups, for a total of less than 20 lines:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">How lucky are you to have been born when and where you are?<br><br>Had Opus 4.8 in Claude Code whip up a new visualization of all humans who ever lived. In addition to being neat, it is an interesting test of combining research, code, design and stats for an AI. <a href="https://t.co/ayNEdhSLy3">https://t.co/ayNEdhSLy3</a> <a href="https://t.co/Ny2NmICZsK">pic.twitter.com/Ny2NmICZsK</a></p>&mdash; Ethan Mollick (@emollick) <a href="https://x.com/emollick/status/2060165879908749490?ref_src=twsrc%5Etfw">May 29, 2026</a></blockquote>

Another example is the website developed by my daughter: a [fullfledged e-commerce platform](https://www.daebias.com/). Developed with zero fancy technology or agentic scaffolding. Just prompts (and a lot of work).

You probably also noticed that in chats with LLMs when we search for information, these LLMS can choose to launch searches on different websites: each search performed with its own  agent. This helps speed up their research and cover more ground in response to your request.

So I'd say that in most cases, we don't need agents even for complex tasks because LLMs  work just fine without, and if agents are useful then LLM launch their own agents and manage them under the hood.

# And the difficulty of agents bumping onto each other
The topic is just unglamorous and the blog post is already too long so I'll be super brief: multiple agents writing simultaneously in your code base will step on each other's feet. If they make changes to the same file, there is a very good chance the resulting file will be a mess.

The remedy is to have each agent working on different [git branches](https://www.w3schools.com/GIT/git_branch.asp), then proceeding to the merge of the branches into the main branch when all agents are done. This is also a mess: what if the merge fails? (and oh, it will). I tried this approach and it is tedious, hair rising and makes you quit the multi agent game quickly.

So how did I do in Flavor 2 to create dozens of crawlers without having agents crashing on the work of the others?

I first conducted plenty of preparatory work on just one crawler, making sure it worked in perfect isolation of the others. Not an easy task when you still want to follow the DRY (don't repeat yourself) principle in coding. Only at this condition that each crawler is perfectly isolated can you have dozens of agents work on source files simultaneously without creating a mess.

If you scroll up and check the bash script I've shared, you'll see I was also advised on the matter by ChatGPT, which added some hard blocks in the prompt, so that each agent is explicitly forbidden from touching files not in the scope of its work.

# Next steps
Getting from dozens of crawlers written with Flavor 2 to hundreds of crawlers. Then executing them. Becoming sufficiently proficient at this "home made" multi agent set up that I can reproduce it when and if needed in other places.

# And you?
What multi agent setup works for you? Or do you stick with no agent at all?

--- 
# About Me

I'm an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com), a point-and-click tool for exploring texts and networks. Try it out and let me know what you think. I'd love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) on app development and data exploration.
