---
layout: post
title: A simple cache warmer
permalink: /cache-warmer/
published: true
date_readable:               Sept 25, 2023
last_modified_at_readable:   Sept 25, 2023
categories: [cache warmer,cache warming,command line interface]
---
I just created a cache warmer, hoping that it is useful to website administrators.

# Cache warming: what is it?
Cache warming consists in "obliging" a website to put its web pages and other resources (images...) in cache, with the aim to speed up the page loading for the visitors of the website.

![freezing](https://github.com/seinecle/blog/assets/1244100/5377e135-77fe-4fd8-8889-d49025248a18)

# Cache warming: should we do it?
Probably not, if you are not ready to invest significant time.
As [this answer on StackOverflow discusses](https://webmasters.stackexchange.com/a/143224/121497), managing the cache(s) of a web application is a complex thing.

Yet, this is a frequent requirement ("get the agency that manages the website to put in place a cache warmer").
I created a simple cache warmer to help someone who had this requirement.
The solution is not sophisticated but it answers the requirement.

# What does it do in practice?

1. It takes a list of urls from the `sitemap.xml` of your website
2. It visits each urls, twice: using the user-agent of a mobile device, and the user-agent of a desktop computer. **The visit explicitly requests a cache refresh**.
3. When all urls have been visited, it pauses for a time (that you define). Then it starts again.

# How to use it

1. you need an access to a Linux server
2. Java 17 should be installed
3. Download this [CacheWarmer-1.0.jar](https://github.com/seinecle/jcachewarmer/tree/main/target) file and place it in a directory
4. Place the files [cache-warmer.properties](https://github.com/seinecle/jcachewarmer/blob/main/cache-warmer.properties) and [site-map-urls.txt](https://github.com/seinecle/jcachewarmer/blob/main/site-map-urls.txt) in the same directory. Modify the values in these 2 files as you prefer. 
5. On the command line in the directory, do: `nohup java --module-path . --module jcachewarmer/net.clementlevallois.cachewarmer.controller.Controller &`

The cache warmer is now running continuously.

# I am not a technical person, but I do have access to a Linux server. Can I run the cache warmer?

I could release a version of the cache warmer that does not need the installation of Java.
It would be a zip file that you would unzip on your server, and a `run.bat` file to execute, that's all.

Get in touch with me (analys at exploreyourdata . com) if that would be interesting to you and you would be ready to invest a bit of time to test the solution.

# Is it free, open source and licensed to allow commercial use?
[Yes it is](https://github.com/seinecle/jcachewarmer/blob/main/LICENCE.md).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
