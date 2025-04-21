---
layout: post
title: Latest improvements to nocodefunctions
permalink: /nocodefunctions-improvements/
published: true
date_readable:               April 21, 2025
last_modified_at_readable:   April 21, 2025
categories: [nocodefunctions, development, architecture, refactoring]
---

This is an update on the latest improvements for nocodefunctions.com, with a short video demo!

# The demo
This video showcases a number of new features detailed below:




Handling first names better

When crawling news sites like lemonde.fr, you can end up with nodes like “Emmanuel” or “Anne” popping up in the resulting network.
Not because two people with those names were making headlines, but because many different people named Emmanuel or Anne were mentioned—completely unrelated.

These standalone first names aren’t very meaningful. Unless they appear frequently with something else—usually a last name—they should be removed.
So:

    “Emmanuel” → removed

    “Emmanuel Macron” → stays

    “Pierre-Emmanuel Barré” → also stays (if mentioned often enough)

🧹 From now on, isolated first names get cleaned up automatically. Enjoy!
Fully responsive

Nocodefunctions.com is meant to be simple:
1️⃣ Upload a file or pick a website
2️⃣ Click "run"
3️⃣ Watch, download, or share the results

It’s something you can totally do from your phone—except, until now, some pages didn’t behave well on mobile.

📲 Good news: all pages now display properly on smartphones. You can analyze and share results on the go—even for entire websites.
Topics are back

The “Topic Detection” feature had been down for a few weeks.
I paused it to take it apart and experiment with building multi-step functions more cleanly.

I learned a lot—especially about how not to let things spiral into spaghetti code.

🚀 Topic detection is back online, and this refactoring should help unlock more powerful features soon.
Semantic networks in multiple languages

I recently tried analyzing the devoxx.fr website—a well-known dev conference series, with the French edition last week.

Results were underwhelming. Why? The site mixes French and English.
Since I had selected "French" as the language, the English pages were misinterpreted—so the stopword filtering failed, and things like “the”, “have”, or “a lot” cluttered the graph.

It turned out to be a relatively small lift to support multiple languages instead of just one.

🎌 You can now select more than one language when your input (file or website) is multilingual.
Check out the cleaned-up graph for devoxx.fr.
Next steps ✨✨✨

I’m now working on chaining functions together—surprise: they’ll rely on generative AI.

The refactoring I did on topic detection is a key building block for this.
More coming soon—stay tuned, and don’t hesitate to reach out!

# About Me
I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think—I’d love your feedback!

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
