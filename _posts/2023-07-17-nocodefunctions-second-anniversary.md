---
layout: post
title: Nocode functions is two years old!
permalink: /nocodefunctions-second-anniversary/
published: false
date_readable:               Jul 17, 2023
last_modified_at_readable:   Jul 17, 2023
---
*[Nocode functions](https://nocodefunctions.com/) is a free, no-registration web app for click-and-point data analysis*

In this post, I make a list of the improvements brought to [nocode functions](https://nocodefunctions.com/) from August 2022 to today (July 2023).

# Key facts over the past year

According to the Wayback machine, I have launched nocodefunctions [around May 2021](http://web.archive.org/web/20210503153337/https://nocodefunctions.com/).
Last year, I celebrated its [first anniversary with a blog post](https://nocodefunctions.com/blog/nocodefunctions-is-one-year-old/) - go have a look!

For Aug 2022 to Jul 2023, read along or jump to the category that interests you the most:

1. Overall feeling
2. Quality, user friendliness
3. Traffic
4. Functions: what's new? what disappeared and why?
5. Long term maintainability
6. Academic returns
7. Outreach
8. What's next

# Overall feeling
![](https://i.pinimg.com/originals/4e/c1/55/4ec1557e1b7e0e996b08d9ccbf8bbaff.gif)

# Quality, user friendliness
- The promise has not changed. Nocode functions remains open source (CC BY 4.0), free, fully translated in 107 languages, requires no registration, and is respectful of your data. Just click and analyze your data!
- The app experienced no significant downtime. Users could rely on it 24/24, 365 days a year. How? Simply: when I feel that I will introduce a change that can break the app, I try the change on a test copy of nocodefunctions, which is: [https://**test**.nocodefunctions.com](https://test.nocodefunctions.com). When everything is stabilized, I deploy the changes on the normal address of nocodefunctions: https://nocodefunctions.com.
- The app remained super fast to load, functions were fast or faster to run, and more error messages were introduced when unexpected errors occurred.
- The overall design and usage flow remained the same: choose a function, upload your data, select optional parameters, run the function, see the results, download the results.
- An ugly error in the design of the web pages has been finally, permanently [fixed in Jumy 2022](https://twitter.com/seinecle/status/1678039323130712064). This error made some functions unusable because the buttons on the pages couldn't be clicked. It was very hard to diagnose as it disappeared and came back randomly without leaving clear errors. I could finally fix it (two [CSS files](https://webplatform.github.io/docs/tutorials/learning_what_css_is/) were colliding), thanks to the detailed reports by [Veronica Espinoza](https://twitter.com/Verukita1).

# Traffic
When I celebrated the first anniversary of Nocodefunctions.com, the app almost always had **less than 300 users** per week. For this second anniversary, the app almost always experiences **more than 300 users** per week.

![image](https://github.com/seinecle/blog/assets/1244100/8ebb73a8-1288-4fb3-84ed-652ce52d6839)

Visit the [public, live version of nocodefunctions users count](https://public.nocodefunctions.com/).

Note: in [November 2022](https://github.com/seinecle/nocodefunctions-web-app/commit/8f2983e96e74b7ee933752ca8dc1ddeb1b90282a), I have changed how users are counted. Before, the count was triggered in a technical and imprecise way: each time a function's [managed bean](https://www.java4coding.com/contents/jsf/jsf-managed-beans) is instantiated. Now, the count of users is incremented each time the button launching a function is clicked (actually launching, not merely choosing a function then leaving the app.

# Functions: what's new? what disappeared and why?

Gone:

- ["Best Worst Scaling"](https://en.wikipedia.org/wiki/Best%E2%80%93worst_scaling) was removed around Spring 2023. It was the most complicated function, hard to maintain, and yet I never had any report of a user for it. If anyone reads this and has a serious interest in it, get in touch. Read this short blog post on [why it is a potentially great function to survey tastes and preferences](https://nocodefunctions.com/blog/best-worst-scaling-bws-in-progress/). Check also [this study in sentiment analysis to see BWS in action](https://aclanthology.org/P17-2074/).
- Tweets importer. [Twitter has shutdown its free API in February 2023](https://twitter.com/TwitterDev/status/1621026986784337922). Get in touch if a Twitter importer for nocodefunctions would remain important to you.

New:

- Spatialize gexf: a gexf file is a classic file format for networks. With this function, you can apply a layout to your network in a quicker way than if you would use [Gephi](https://gephi.org/) instead. The function is not amazingly fast to be honest, but still better than doing the layout directly in Gephi.
- Detect promoted content. Still embryonic, this function should be widely used in my opinion! Basically, it categories texts in "natural / organic / genuine voice" vs "promoted / corporate speak". That is essential if you do sentiment analysis on brands or products, as you'd want to first filter out posts or tweets that are paid content sponsoring or promoting this product!
- Sentiment analysis in Spanish. This feature was developped by [Emma Léger](https://www.linkedin.com/in/emmaleger/) whom I thank here. This new feature now needs to be further tested and improved, don't hesitate reporting issues, directly from the app!

Much improved:

- Semantic network generator, topic detection, sentiment analysis. These three functions now benefit from excellent (unique, I'd dare say) methods for the first essential steps of treatment of the text that you provide as input. Basically, these functions work on the words in the text, so the first step consisting in cutting the text in all its words is of great importance. This is harder than it seems. Punctuation signs, accentuations, lower and upper case, and multi-words ("European Union") need to be taken into account if we want the next steps to achieve a high accuracy. A keystone to these operations is the [tokenizer](https://github.com/seinecle/umigon-tokenizer), which I released in March 2023. More on this in the "Long term maintainability" section below.

- pdf matcher. I really like the development of this function, which shows several benefits of the app:
    - on April 2 2022, [Runa Sandvik](https://twitter.com/runasand) who is a security specialist I follow on Twitter, asked for a simple solution to mine pdfs.
    - on April 9, 2022, I could release a new function doing that - called [pdf matcher](https://nocodefunctions.com/pdfmatcher/pdf_matcher_tool.html) as described in [this blog post](https://nocodefunctions.com/blog/pdf-matcher-tool-for-journalists/).
    - in August 2022, [Veronica Espinoza](https://twitter.com/Verukita1) reports that words cut at the end of a line are missed out (ignored), when uploading pdfs for semantic networks. I improve the pdf reader to take this into account, and this benefits all functions using pdfs for inputs - including the pdf matcher function of course.
    - on July 4 2023, so one year later, I improved this function a lot because I'll need it for an academic project. It now features [boolean searches](https://nocodefunctions.com/blog/enhanced-pdf-search/). Doing this, I realized it was bugged in different ways.

Created in answer to the need of a member of the community, released super quickly, improved thanks to a user report, and then developed further for my own needs: 4 things that illustrate why I feel fullfilled developping the app.

# Long term maintainability
The app required to be refactored. I hesitated doing it for a long time because it required a lot of work, without bringing anything really new or visible to the users - at least in the short term.

**Over Oct-Nov 2022, I cut the app in 3 different parts: a front-end, a back-end running the functions, and a back-end managing file uploads and downloads (I/O)**. Why? The app had become a monolith of about 120 Mb in size. With this transformation, it became a front-end of 13Mb in size, a back-end of 97 Mb (functions) and 30 Mb (I/O). Let's explain the pain points it solved:

## Quicker devops
- BEFORE: slow to compile ( > 1 min), upload (1 min) and deploy (1:30 in my IDE, 20 seconds on the server). It was becoming horrible to wait 1 to 2 minutes to see the results of a tiny change I made in the code, and really frustrating since I knew that all this time was lost compiling the entire app, when the change was affecting 1% of it!
- AFTER: 20 seconds max to compile and same to upload. Deployment takes 15 seconds for the front-end (also locally! compared to > 1 minute before!), and one second for the back-end. I can do changes and see the results super quickly! Pyschologically, the frustration of suffering this waiting time is gone, so I enjoy coding.

## Less downtime
- BEFORE: The app being a monolith, I had to stop it entirely to redeploy it even if the change I had made to the app was super small and affecting a tiny backend function. The web app was down just for 20 seconds or so to deploy this tiny change, which was bad for the users and also really unsatisfying / frustrating on my side.
- AFTER: I can start and stop each part of nocode functions independently. That means that a user will not see a 404 error when visiting the site when I am simply restarting the functions or the I/O machinery.

## Cleaner organization
- BEFORE: the app mixed the code for the web pages with the code performing the functions. Very bad practice, and a pain to maintain ("where did I put this part of the function again? In the code of the button where the user clicked... 🤦"). 
- AFTER: The code for each function is in a separate project. The front-end sends data to these projects, and receives the results from them, through a web service.

Graphically, this looks like:
<div style= "border:1px;">
![](https://docs.google.com/drawings/d/e/2PACX-1vTc-zHHvrXo9DynfUhRuD0B3TyVL7LOaW1cvKNlhPGyNJoncjjbrOuWZGRSFe0tP1x5qQ8p0ZyVJFgx/pub?w=480&h=360)
</div>
      
# Acknowledgements

![](https://media.giphy.com/media/ZfK4cXKJTTay1Ava29/giphy.gif)

This app is truly built on the shoulders of giants. Fully developed in [Java](https://www.youtube.com/watch?v=RRubcjpTkks) using [Netbeans](https://netbeans.apache.org/) as a coding tool, I thank the community for developing such a versatile, robust, easy-to-use programming language and tooling. Thanks also to all the maintainers of the libraries that provide specific features. And thanks to all the users who provided feedback, big or not, anonymously or not. Find the [detailed list of acknowledgements here](https://nocodefunctions.com/acknowledgements.html).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

