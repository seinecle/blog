---
layout: post
title: Gephi code retreat for 2022 - my impressions a week later
permalink: /gephi-code-retreat-2022-impressions/
published: false
date_readable:               Sept 08, 2022
last_modified_at_readable:   Sept 08, 2022
---

*My thoughts on the Gephi Code Retreat - 2022 edition, to which I participated in Paris last week*

# Quick background on Gephi

Two-line summary if you don't know Gephi. Born around 2010, [Gephi](https://gephi.org) is the leading software for the visualization and exploration of networks.
It is open source and free. It is used by analysts, professors, journalists, students. It useful to find patterns and connecting the dots in rich and unstructured datasets, for instance: finding communities, people with key roles in a crowd, identifying connections between items or products, etc.

<div aling="center">
   <img src="https://user-images.githubusercontent.com/1244100/189077290-65d51016-df16-4b8c-a154-0cf64ee01eb9.png" title="A screenshot of Gephi" width="500px/>
</div>                                                                                                                                  

**Gephi has been downloaded [millions of times](https://seinecle.github.io/gephi-tutorials/generated-html/history-en.html#_a_cumulative_downloads) since its creation**, and the original paper describing Gephi has been cited by close to **[10,000 academic publications from a huge variety of scientific fields]([https://scholar.google.fr/scholar?hl=fr&as_sdt=0%2C5&q=gephi&btnG=](https://scholar.google.fr/citations?view_op=view_citation&hl=fr&user=fEDLILQAAAAJ&citation_for_view=fEDLILQAAAAJ:u5HHmVD_uO8C))**.

The Gephi Code retreat is a one-week event organized by the founding members of Gephi to accelerate the development of the software and help the community of Gephi enthusiasts meet and cohere. That is the second year such a retreat is organized, after a first edition in Copenhagen.

# What did I do / deliver?

I worked the full week on creating a plugin for Gephi that will allow a user, directly while using Gephi, to export the network they are working on to the web.
The network will be viewable and explorable from the browser, and shareable with a simple url.

[A short video with a live demo available here](https://www.twitch.tv/videos/1579615061?t=01h28m54s) explains all the details.

It is important and fair to note that the plugin leverages 2 key resources that I did not develop myself - [Alexis Jacomy](https://twitter.com/jacomyal) and [Ouestware](https://www.ouestware.com/en/) developed and designed them:

- the library to visualize the networks on the web, which is called [Retina](https://ouestware.gitlab.io/retina/beta/)
- the roadmap to actually export the network to the web, which involves creating a Gist on Github, and [which is publicly discussed here](https://github.com/gephi/gephi-plugins/issues/262#issuecomment-1231627948).

The plugin is not released yet, as it needs to be reviewed and will probably be released with a bunch of other deliverables produced by other contributors during this week.
You can [check the code here](https://github.com/gephi/gephi-plugins/tree/web-publish-plugin/modules/WebPublishPlugin), and see that I continue to push updates to refine it.

# If you'd like to see the Gephi week or what I'm doing

- Check the [Twitch stream of the Gephi week](https://www.twitch.tv/datalgo) - I'll try to say hi this afternoon (Paris time)
- Get fresh news from the [Gephi Twitter account](https://twitter.com/Gephi) and also from [Datalgo](https://twitter.com/nicolasbchb)
- Here are the [Gephi plugins I have developed over the years](https://gephi.org/plugins/#/browse/search/levallois)

I have written [tutorials for Gephi](https://seinecle.github.io/gephi-tutorials/).
I also build [nocode functions](https://nocodefunctions.com) 🔎 that can also serve the needs of the community of Gephi users. It is [fully open source](https://github.com/seinecle/nocodefunctions).
Try it and give some feedback, I would appreciate it!

* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about my journey as a social scientist and app developer.
