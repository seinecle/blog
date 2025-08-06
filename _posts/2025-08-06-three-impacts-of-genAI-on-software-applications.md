---
layout: post
title: "Three impacts of gen AI on software applications"
permalink: /three-impacts-of-genAI-on-software-applications/
published: true
date_readable: 6 August 2025
last_modified_at_readable: 6 August 2025
categories: [AI, generative AI, software application, destructive creation]
---

These are very short notes to categorize and clarify how gen AI impacts existing software applications.

# Positive change

## *Easier software development*
Gen AI acts as an augmented suit: developpers become better developers. They can code more complex tasks, quicker. A team of developers has an extended potential.
Or the the same potential can be achieved with a reduced team. Or even: a reduced team still has an extended potential.

# Negative change
(negative or disruptive or risky: your pick)

## *Entire classes of text-handling software are made obsolete by a ChatGPT-like interface*
Early August 2025, I have seen a fellow academic announcing the coming launch of his new web app: a service for students to revise, comment and predict the grade of the Master thesis they are working on.

-> this is obsolete by design. Just uploading the draft of the thesis to ChatGPT provides the student with all the feedback they need. With less friction.

Take away: Grammarly, Deepl, and a large numbers of software applications manipulating textual documents are replacable by prompting ChatGPT for the exact service, for free.

## *Software helping finding needles in a haystack are at risk of getting bypassed*
I remember these two contrasting posts:

**a.** on the reddit channel for OSINT , [a post in July 2025 asking whether genAI was useful to fellow OSINT researchers](https://www.reddit.com/r/OSINT/comments/1lrjcv0/osint_and_ai/).
The best voted answer starts with:

> "Personally as AI researcher I have zero trust in anything LLM spews out. "

**b.** In May 2025, Ethan Mollick (whom I absolutely advise to follow) had posted this:

<blockquote class="bluesky-embed" data-bluesky-uri="at://did:plc:flxq4uyjfotciovpw3x3fxnu/app.bsky.feed.post/3lokji4dwpc2z" data-bluesky-cid="bafyreibsly4scel4t5fxshjbhv3kkos3nricg5a43jypklrj6m5xjirshq" data-bluesky-embed-color-mode="system"><p lang="en">Pretty awesome result from the new version of Gemini 2.5.

I changed one line of War and Peace, inserting a sentence into Book 14, Chapter 10 (halfway through), where Princess Mary &quot;spoke to Crab Man the superhero.&quot;

Gemini 2.5 consistently found this reference among 860,00 tokens.<br><br><a href="https://bsky.app/profile/did:plc:flxq4uyjfotciovpw3x3fxnu/post/3lokji4dwpc2z?ref_src=embed">[image or embed]</a></p>&mdash; Ethan Mollick (<a href="https://bsky.app/profile/did:plc:flxq4uyjfotciovpw3x3fxnu?ref_src=embed">@emollick.bsky.social</a>) <a href="https://bsky.app/profile/did:plc:flxq4uyjfotciovpw3x3fxnu/post/3lokji4dwpc2z?ref_src=embed">7 mai 2025 à 06:06</a></blockquote>

-> OSINT researchers could be a bit more curious about gen AI capabilities for their trade.

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

Then it can interface whatever this IT environment produced with its dialog and reasoning capabilies (part b.) - a domain or skillset that software companies do not possess or master.




### A propos
Je suis Clément Levallois, universitaire et développeur indépendant de [nocode functions](https://nocodefunctions.com) 🔎, une application d'analyse de texte et de réseaux. Cette app est [open source](https://github.com/seinecle/nocodefunctions).

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Plus d'articles](https://nocodefunctions.com/blog) 👓.
