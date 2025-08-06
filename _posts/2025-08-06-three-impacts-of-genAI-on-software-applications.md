---
layout: post
title: "Three impacts of gen AI on software applications"
permalink: /three-impacts-of-genAI-on-software-applications/
published: true
date_readable: 6 August 2025
last_modified_at_readable: 6 August 2025
categories: [AI, generative AI, software application, destructive creation]
---

These are personal notes to categorize and clarify how gen AI impacts existing software applications.

# Positive change
## *Easier software development*
Gen AI acts as an augmented suit: with AI copilots, developpers become better developers. They can code more complex tasks, quicker. A team of developers gains an extended potential.
Or the the same potential can be achieved with a reduced team. Or even: a reduced team still has an extended potential.

# Negative change
(negative or disruptive or risky: your pick)

## *Entire classes of domain-specific analytics are made obsolete by a ChatGPT-like interface*
Early August 2025, I have seen a fellow academic announcing the coming launch of his new web app: a service for students to revise, comment and predict the grade of the Master thesis they are working on.

-> this is obsolete by design. Just uploading the draft of the thesis to ChatGPT provides the student with all the feedback they need. With less friction.

Take away: Grammarly, Deepl, and a large numbers of software applications offering analytics on documents for specific domains are replacable by prompting ChatGPT for the exact service, for free.

## *Software in information retrieval are at risk of getting bypassed*
Contrast these posts a. and b.:

**a.** In July 2025 on the reddit channel for OSINT , [a post asked whether genAI was useful to fellow OSINT researchers](https://www.reddit.com/r/OSINT/comments/1lrjcv0/osint_and_ai/).
The best voted answer starts with:

> "Personally as AI researcher I have zero trust in anything LLM spews out. "

**b.** In May 2025, Ethan Mollick (whom I absolutely advise to follow) posted this on Bluesky:

<blockquote class="bluesky-embed" data-bluesky-uri="at://did:plc:flxq4uyjfotciovpw3x3fxnu/app.bsky.feed.post/3lokji4dwpc2z" data-bluesky-cid="bafyreibsly4scel4t5fxshjbhv3kkos3nricg5a43jypklrj6m5xjirshq" data-bluesky-embed-color-mode="system"><p lang="en">Pretty awesome result from the new version of Gemini 2.5.

I changed one line of War and Peace, inserting a sentence into Book 14, Chapter 10 (halfway through), where Princess Mary &quot;spoke to Crab Man the superhero.&quot;

Gemini 2.5 consistently found this reference among 860,00 tokens.<br><br><a href="https://bsky.app/profile/did:plc:flxq4uyjfotciovpw3x3fxnu/post/3lokji4dwpc2z?ref_src=embed">[image or embed]</a></p>&mdash; Ethan Mollick (<a href="https://bsky.app/profile/did:plc:flxq4uyjfotciovpw3x3fxnu?ref_src=embed">@emollick.bsky.social</a>) <a href="https://bsky.app/profile/did:plc:flxq4uyjfotciovpw3x3fxnu/post/3lokji4dwpc2z?ref_src=embed">7 mai 2025 à 06:06</a></blockquote>

-> in my honest opinion, Ethan Mollick's experiment suggests that for a wide range of "find the needle in the haystak" kind of tasks, LLMs are already unique in the value they can deliver. 

That is of concern to software relying on any domains of information retrieval in some capacity: search engines, natural language processing, database management, data preparation, document processing, data visualization, and more.

And that is an opportunity that OSINT specialists should explore.

## *AI agents will act as "on-the-fly sofware packages"*
On July 17, 2025, OpenAI has released agents in ChatGPT. In practice, this means that your question to ChatGPT can now trigger the launch of a sandboxed Linux instance (in simple terms, a "small computer") able to download, install and run any available software to help answer your question. All done autonomously, at the moment of your request!

I tried it in the following way:

- I have the network of my followers on Twitter, back from 2023. This is stored as a text file formatted in a specialized way: the gexf file format, made to represent entities and their relations.
- I used a specialized desktop software named [Gephi](https://gephi.org/) to create this visual representation of this network:

<img width="400" height="400" alt="seinecle_network_small" src="https://github.com/user-attachments/assets/3a111562-3d6a-4079-a9bb-8b46d45a9b40" />

**Could this be done "just with ChatGPT"?**

Here is the visualization that I could create by uploading the file to ChatGPT and then asking some questions:

<iframe src="/blog/assets/data/network_interactive.html" width="430" height="350"></iframe>

(here is [the entire dialog with ChatGPT](https://chatgpt.com/share/68931976-5dec-8001-8c6a-f7e4c955f712))

This is pretty good for a 10-minute exercise. To achieve this result, ChatGPT followed 2 types of actions, without my intervention:

**a.** for the data analytics part: it could **not** perform it just by following a "token generation logic" because the data is too large to fit its context window reliably. So it spawned a mini Linux instance,  installed the python packages it judged necessary, and used this custom, newly created IT environment to reliably upload, read and analyze the file.

**b.** for the generation of the interactive web visualization, it just relied on its "instantaneous" knowledge of D3, the javascript library it used for it.

**Part a. of the process is the one that is usually crafted, maintained (and sold) by software companies. Now, ChatGPT can assemble these sofware parts when and as needed, for the price of a 20€ / month ChatGPT subscription.**

# Ways out
To avoid being weeded out by genAI, software need to deliver a value not reproducible via existing chat interfaces, nor through the newest agentic capabilities.

> The value delivered needs to rely on the <u>integration</u> of <u>non trivial</u>, <u>custom</u> resources and processes.

*integration*: software need to arrange, combine and interface a series of resources so that the mix they create is hard to reproduce. At the moment, even with multimodal LLMs, assembling a variety of heterogeneous assets is an area that LLMs dont excel at.

*non trivial*: the more specific, niche, specialized the resource: the better. LLM agents rely on tools and processes that they can find on the Internet (think: most starred repo on Github) and they tend to pick the most commonly known items of the category.

*custom*: software can rely on classic processes, but then they should customize them to be truly better than the default that agentic AI will pick. Choosing non obvious parameters, rewritting some key parts of the process.

# Final thoughts: open source - to what extent?
I develop my web app entirely in open source. I am not sure what feeling I would have if I would see an AI agent pick up some of my functions and integrate it in some processes in response to a user request. Why should it matter, since in the end a user has been served, which is one of my key objectives? I still feel that I would kind of loose control to OpenAI on what I have created. I am not sure.

If I wanted to prevent that from happening, I could:

- close the source of my code
- make the build of my code hard to reproduce. Which it already is.
- write my code in another language than Python, because LLMs pick mostly from Python and Javascript at the day of this writing. I write in Java so this is already the case.

---
# About Me
I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
