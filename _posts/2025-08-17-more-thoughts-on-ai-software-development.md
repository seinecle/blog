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

## 1. Take files as input
Until last year, most gen AI apps were limited in the kind of files they could read. Gemini couldn't even read pdfs if I recall correctly.
This tends to quickly disappear.
Most apps now accept txt, csv, pdf, docx, xlsx, pptx, any xml or json files.

## 2. Can perform advanced analytics, on the fly
ChatGPT can now launch a mini IT environment to treat your queries on the fly: it will be able to run any Python code that is freely available as a packaged library on the web.

## 3. Reasoning
This one is there from the start: LLMs' stunning impact is that they (seem to) reason like any human would do.
I let you appreciate whether this human is like "an intern", "an undergrad" or "PhD level", but still quite close to what a human could do.

# What gen AI *can't* do as of August 2025

## 1. Connect to "live" data sources
Analyzing Bluesky or Reddit or LinkedIn data on the fly?
That is probably already possible: after all, I imagine you can provide your API account credentials for any of these services in a prompt and that would enable the gen AI app to fetch the data on your behalf.
*But that is not practical nor straightforward*. What about speed, memory limits, fine controls, error handling, and persistence of the data that is fetched?

## 2. Fine handling of information
A conversational generative AI can now single handly cover the entire chain of data processing:

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

## 1. Gen AI chatbots enriching their interface
[OpenAI launched "Canvas" in 2024](https://openai.com/fr-FR/index/introducing-canvas/), a panel window that opens next to the conversation when the information at hand manifestly needs an other classic form of display. Canvas can take form of a table when needed, or a coding editor, and can render anything that can be represented as a web page: apps, maps, tables, whatever really.

-> Gemini by Google launched a similar feature, also named "Canvas", in Spring 2025. 

In my experience, these are not really helpful yet: past simple cases, the rendering of html pages is buggy and advanced features are immediately missing (for tabular data).

## 2. Incumbent software integrating AI
This is a priori a smart move: existing software have all the convenience of a very familiar interface to their very large base of users. So you just need to add gen AI capabilities (like: analytics and reasoning) to it. Think Microsoft Copilot added to Excel. But as of this day the results are very disappointing.

Another (anecdotical) instance is the supermarket chain where I do my grocery shopping, and that delivers it. All from a mobile app. So they tried to add a "gen ai" feature that would help me pre-fill my basket, based on my previous purchases. Well, that fails miserably and a basic expert system would have been enough ("suggest the most frequently, most recently purchased items"). 

Attempts with a better success are:

- [Photoshop](https://helpx.adobe.com/photoshop/using/generative-expand.html) integrating AI-based functions (a move that dates before generative AI).
- [JetBrains](https://www.jetbrains.com/help/idea/ai-assistant-in-jetbrains-ides.html) adding AI assistant capabilities to its IDEs. Same for [VS Code](https://www.infoworld.com/article/3982310/visual-studio-code-beefs-up-ai-coding-features.html?utm_source=chatgpt.com)

## New "AI native software"






---
# About Me
I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
