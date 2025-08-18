---
layout: post
title: "More thougts on the impact of gen AI on software applications"
permalink: /more-thoughts-on-impacts-of-genAI-on-software-applications/
published: false
date_readable: 17 August 2025
last_modified_at_readable: 17 August 2025
categories: [AI, generative AI, software application, destructive creation]
---

These are personal notes on how gen AI impacts existing software applications. Follow up to [this post](/three-impacts-of-genAI-on-software-applications/).

# What gen AI *can* do as of August 2025

## 1. Take multimodal files as input
Until last year, most gen AI apps were limited in the kind of files they could read. Gemini couldn't even read pdfs if I recall correctly.
This barrier has fallen.

Most apps now accept txt, csv, pdf, docx, xlsx, pptx, any xml or json files. More importantly, all major gen ai apps are now multimodal: they accept text but also pictures as input and can make very detailed content analysis of them. I just tried with Chat by Mistral (free version), Gemini, Claude (free version) and ChatGPT: all of them could describe a screenshot of my laptop in great and accurate detail.

Sound analysis has landed, too. We can make a very detailed analysis of a .wav file, for example (as of Aug 2025, only ChatGPT has this capability).

And video? As of now, only ChatGPT can process videos: on the video I tested, it extracts a sample of frames and then tries to infer a meaning from them.  

## 2. Perform advanced analytics, on the fly
ChatGPT can now launch a mini IT environment to treat your queries on the fly: it will be able to run any Python code that is freely available as a packaged library on the web.

## 3. Reasoning
This one is there from the start: LLMs' stunning impact is that they (seem to) reason like any human would do.
I let you appreciate whether this human is like "an intern", "an undergrad" or "PhD level", but still quite close to what a human could do.

Reasoning has taken a new turn since Autumn 2024 ([Open AI](https://openai.com/fr-FR/index/introducing-openai-o1-preview/?utm_source=chatgpt.com)) / February 2025 ([Claude](https://www.anthropic.com/news/claude-3-7-sonnet?utm_source=chatgpt.com)) /  March 2025 ([Gemini](https://blog.google/technology/google-deepmind/gemini-model-thinking-updates-march-2025/#gemini-2-5-thinking)) with the ability for a gen ai app to iterate: it can now feed itself the results it has produced, which allows for re-examinations, modifications and improvements before the final version of the results are delivered to the user.

### Generate interactive, multimodal content
All major providers are now capable of generating pics and interactive web applications.

# What gen AI *can't* do as of August 2025

## ~~1. Connect to "live" data sources~~
Analyzing Bluesky or Reddit or LinkedIn data on the fly?
That is probably already possible: after all, I imagine you can provide your API account credentials for any of these services in a prompt and that would enable the gen AI app to fetch the data on your behalf.
*But that is not practical nor straightforward*. What about speed, memory limits, fine controls, error handling, and persistence of the data that is fetched?

I was about to conclude this paragraph this way but... Claude by Anthropic is contradicting this argument: since [May 2025](https://www.anthropic.com/news/integrations) and with frequent enrichments since then, it offers 2 kinds of data connectors:

- connectors to your desktop apps (your browser, your file explorer...),
- connectors to web data sources and services (Canva, Gmail, Notion, etc.).

These connectors mean that you can use Claude to reason and create about whatever content you produce from your laptop.

## 2. Fine handling of information
A conversational generative AI can now single-handedly cover the entire chain of data processing:

- you can provide a variety of inputs: files, images, prompts (but "live" data sources remain an issue, see just above) 
- these inputs can trigger the launch of a variety of actions to complete your query: web search, creation of a mini-IT environement to perform analytics, a reasoning mode, the creation of visuals, or just a quick written reply if that's all that is necessary.
- you can then save the result: copy the response to the clipboard, or download the results as a file, or download the image.

-> you never leave the app, it is all integrated in one place.

**But in practice and despite all of this, the tasks we perform often quickly require some basic information handling that is not available in the ChatGPT environnment:**

- search, filtering, sorting, renaming, formatting, "undo", ...
These tasks are often perceived to be so elementary that they are situated at the periphery of the value proposition of any given software.
Yet they are the reason we leave a chatgpt conversation and come back to a "regular" desktop application. Because it "is easier and quicker" to conduct these tasks there.

To illustrate : ChatGPT generates text, for sure. Yet we still copy paste the results to Word and take some time formatting and doing some revisions there.
If the final destination of the text is a Powerpoint document, there is even more intense steps of reformatting, as anyone who tried would agree.

## 3. Offer interfaces designed for the task at hand 
Pretty obvious argument: ChatGPT (and Claude and Gemini etc) are generalist apps centered on a conversational interface.
This interface is definitely *not* the most useful in many situations:

- need to manipulate tabular data? An Excel-like interface seem essential
- are you a coder? Then "IDEs" (integrated development enviromnents) are proved solutions for decades now
- are you a UX designer? Then a canvas interface is necessary.
etc.

# 3 directions where these tensions are pushing innovation

## 1. Gen AI chatbots diversifying their interface
[OpenAI launched "Canvas" in 2024](https://openai.com/fr-FR/index/introducing-canvas/), a panel window that opens next to the conversation when the information at hand manifestly needs an other classic form of display. Canvas can take form of a table when needed, or a coding editor, and can render anything that can be represented as a web page: apps, maps, tables, whatever really.

-> [in May 2025](https://blog.google/products/gemini/gemini-collaboration-features/), Gemini by Google launched a similar feature, also named "Canvas". 

In my experience, these are "nice to have" features but not that useful yet: past simple cases, the rendering of html pages is buggy and advanced features are immediately missing (for tabular data for instance).

## 2. Incumbent software integrating AI
This is a priori a smart move: existing software have all the convenience of a very familiar interface to their very large base of users. So you just need to add gen AI capabilities (like: analytics and reasoning) to it. Think Microsoft Copilot added to Excel. But as of this day, in my personal experience the results are very disappointing:

- Copilot in Excel doesn't achieve anything useful: it succeeds at simple tasks, which you could have done yourself quicker, such as adding a column that sums two other columns. And it fails at the more complicated tasks, such as formatting a table or filling values in a column by creating an advanced formula.

- Another (anecdotical) instance is the app I use for grocery shopping. They tried to introduce a "gen ai" feature that would help me pre-fill my basket, based on my previous purchases. Well, that fails miserably and a basic expert system would have been enough ("suggest the most frequently, most recently purchased items"). 

An attempt with a better success is the product category of "integrated development environments" (commonly known as IDEs): these software offer programmers all the necessary assistance to code faster and in a more "comfortable" way (it automates boring tasks etc).
Today, all major IDEs offer AI assisted coding and coders actively use these features, to the point that the absence of these AI assistant features are ressented as hurting productivity. Examples: [JetBrains](https://www.jetbrains.com/help/idea/ai-assistant-in-jetbrains-ides.html) or [VS Code](https://www.infoworld.com/article/3982310/visual-studio-code-beefs-up-ai-coding-features.html?utm_source=chatgpt.com).

## New "AI native software"
This is a very active area of development, so I won't be exhaustive by any stretch here. I'll take two examples:

- [Scenario](https://www.scenario.com/) which generates 3D assets
- Suno that generates music
- 





---
# About Me
I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
