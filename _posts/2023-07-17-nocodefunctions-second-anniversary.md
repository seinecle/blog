---
layout: post
title: Nocode functions is two years old!
permalink: /nocodefunctions-second-anniversary/
published: true
date_readable:               Jul 17, 2023
last_modified_at_readable:   Jul 17, 2023
---
*[Nocode functions](https://nocodefunctions.com/) is a free, no-registration web app for click-and-point data analysis*

In this post, I make a list of the improvements brought to [nocode functions](https://nocodefunctions.com/) from August 2022 to today (July 2023).

# Key facts over the past year

According to the Wayback machine, I have launched nocodefunctions [around May 2021](http://web.archive.org/web/20210503153337/https://nocodefunctions.com/).
Last year, I celebrated its [first anniversary with a blog post](https://nocodefunctions.com/blog/nocodefunctions-is-one-year-old/) - go have a look!

# Overall feeling
![](https://i.pinimg.com/originals/4e/c1/55/4ec1557e1b7e0e996b08d9ccbf8bbaff.gif)

# Quality, user friendliness 🤗
- The promise has not changed. Nocode functions remains open source (CC BY 4.0), free, fully translated in 107 languages, requires no registration, and is respectful of your data. Just click and analyze your data!
- The app experienced no significant downtime. Users could rely on it 24/24, 365 days a year. How? Simply: when I feel that I will introduce a change that can break the app, I first try the change on a test copy of nocodefunctions, which is: [https://**test**.nocodefunctions.com](https://test.nocodefunctions.com). When everything is stabilized, I deploy the changes on the normal address of nocodefunctions: https://nocodefunctions.com.
- The app remained super fast to load, functions were fast or faster to run, and more error messages were introduced when unexpected errors occurred.
- The overall design and usage flow remained the same: choose a function, upload your data, select optional parameters, run the function, see the results, download the results.
- An ugly error in the design of the web pages has been finally, permanently [fixed in July 2022](https://twitter.com/seinecle/status/1678039323130712064). This error made some functions unusable because the buttons on the pages couldn't be clicked. It was very hard to diagnose as it disappeared and came back randomly without leaving clear errors. I could finally fix it (two [CSS files](https://webplatform.github.io/docs/tutorials/learning_what_css_is/) were colliding), thanks to the detailed reports by [Veronica Espinoza](https://twitter.com/Verukita1).

# Traffic
When I celebrated the first anniversary of Nocodefunctions.com, the app almost always had **less than 300 users** per week. For this second anniversary, the app almost always experiences **more than 300 users** per week.

![image](https://github.com/seinecle/blog/assets/1244100/8ebb73a8-1288-4fb3-84ed-652ce52d6839)

Visit the [public, live version of nocodefunctions users count](https://public.nocodefunctions.com/).

Note: in [November 2022](https://github.com/seinecle/nocodefunctions-web-app/commit/8f2983e96e74b7ee933752ca8dc1ddeb1b90282a), I have changed how users are counted. Before, the count was triggered in a technical and imprecise way: each time a function's [managed bean](https://www.java4coding.com/contents/jsf/jsf-managed-beans) is instantiated. Now, the count of users is incremented each time the button launching a function is clicked (actually launching, not merely choosing a function then leaving the app).

# Functions: what's new? what disappeared and why?

🎈 Gone:

- ["Best Worst Scaling"](https://en.wikipedia.org/wiki/Best%E2%80%93worst_scaling) was removed around Spring 2023. It was the most complicated function, hard to maintain, and yet I never had any report of a user for it. If anyone reads this and has a serious interest in it, get in touch. Read this short blog post on [why it is a potentially great function to survey tastes and preferences](https://nocodefunctions.com/blog/best-worst-scaling-bws-in-progress/). Check also [this study in sentiment analysis to see BWS in action](https://aclanthology.org/P17-2074/).
- Tweets importer. [Twitter has shutdown its free API in February 2023](https://twitter.com/TwitterDev/status/1621026986784337922). Get in touch if a Twitter importer for nocodefunctions would remain important to you.

🪄 New:

- [Spatialize gexf](https://nocodefunctions.com/spatialize/spatialize_network.html): a gexf file is a classic file format for networks. With this function, you can apply a layout to your network in a quicker way than if you would use [Gephi](https://gephi.org/) instead. The function is not amazingly fast to be honest, but still better than doing the layout directly in Gephi.
- [Detect promoted content](https://nocodefunctions.com/organic/organic_listening_voice_of_customer_tool.html). Still embryonic, this function should be widely used in my opinion! Basically, it categories texts in "natural / organic / genuine voice" vs "promoted / corporate speak". That is essential if you do sentiment analysis on brands or products, as you'd want to first filter out posts or tweets that are paid content sponsoring or promoting this product!
- [Sentiment analysis in Spanish](https://nocodefunctions.com/umigon/sentiment_analysis_tool.html). This feature was developped by [Emma Léger](https://www.linkedin.com/in/emmaleger/) whom I thank here. This new feature now needs to be further tested and improved, don't hesitate reporting issues, directly from the app!

📈 Much improved:

- [Semantic network generator](https://nocodefunctions.com/cowo/semantic_networks_tool.html), [topic detection](https://nocodefunctions.com/topics/topic_extraction_tool.html), [sentiment analysis](https://nocodefunctions.com/umigon/sentiment_analysis_tool.html). These three functions now benefit from excellent (unique, I'd dare say) methods for the first essential steps of treatment of the text that you provide as input. Basically, these functions work on the words in the text, so the first step consisting in cutting the text in all its words is of great importance. This is harder than it seems. Punctuation signs, accentuations, lower and upper case, and multi-words ("European Union") need to be taken into account if we want the next steps to achieve a high accuracy. A keystone to these operations is the [tokenizer](https://github.com/seinecle/umigon-tokenizer), which I released in March 2023. More on this in the "Long term maintainability" section below.

- [pdf matcher](https://nocodefunctions.com/pdfmatcher/pdf_matcher_tool.html). I really like the development of this function, which shows several benefits of the app:
    - on April 2 2022, [Runa Sandvik](https://twitter.com/runasand) who is a security specialist I follow on Twitter, asked for a simple solution to mine pdfs.
    - on April 9, 2022, I could release a new function doing that - called [pdf matcher](https://nocodefunctions.com/pdfmatcher/pdf_matcher_tool.html) as described in [this blog post](https://nocodefunctions.com/blog/pdf-matcher-tool-for-journalists/).
    - in August 2022, [Veronica Espinoza](https://twitter.com/Verukita1) reports that words cut at the end of a line are missed out (ignored), when uploading pdfs for semantic networks. I improve the pdf reader to take this into account, and this benefits all functions using pdfs for inputs - including the pdf matcher function of course.
    - on July 4 2023, so one year later, I improved this function a lot because I'll need it for an academic project. It now features [boolean searches](https://nocodefunctions.com/blog/enhanced-pdf-search/). Doing this, I realized it was bugged in different ways.

Created in answer to the need of a member of the community, released super quickly, improved thanks to a user report, and then developed further for my own needs: 4 things that illustrate why I feel fullfilled developping the app.

# Long term maintainability
The app grew and grew as a single big project containing more and more files, to the point where working on it was slowed down in many ways, even if once deployed it was still very fast and the users didn't really notice anything.
To make my experience as a developer still enjoyable, the app required to be "refactored", re-architectured in a leaner way.

I hesitated doing it for a long time because once you start it, there is no turning back. You break everything and must push forward to get to the new version that you hope will be better.
That requires a lot of work, the app is basically "in the air" for weeks (available and running online, but the code to produce it is turned into something else).
And without bringing anything really new in terms of features or visible upgrade to the users - at least in the short term. Anyway, I jumped!

**Over Oct-Nov 2022, I cut the app in 3 different parts: a front-end, a back-end running the functions, and a back-end managing file uploads and downloads (I/O)**. Before the operation, the app had become a monolith of about 120 Mb in size. With this transformation, it became a front-end of 13Mb in size, a back-end of 97 Mb (functions) and 30 Mb (I/O). Let's explain the pain points it solved:

## Quicker devops 💨
- BEFORE: slow to compile ( > 1 min), upload (1 min) and deploy (1:30 in my IDE, 20 seconds on the server). It was becoming horrible to wait 1 to 2 minutes to see the results of a tiny change I made in the code, and really frustrating since I knew that all this time was lost compiling the entire app, when the change was affecting 1% of it!
- AFTER: 20 seconds max to compile and same to upload. Deployment takes 15 seconds for the front-end (also locally! compared to > 1 minute before!), and one second for the back-end. I can do changes and see the results super quickly! Pyschologically, the frustration of suffering this waiting time is gone, so I enjoy coding.

## Less downtime ⏳
- BEFORE: The app being a monolith, I had to stop it entirely to redeploy it even if the change I had made to the app was super small and affecting a tiny backend function. The web app was down just for 20 seconds or so to deploy this tiny change, which was bad for the users and also really unsatisfying / frustrating on my side.
- AFTER: I can start and stop each part of nocode functions independently. That means that a user will not see a 404 error when visiting the site when I am simply restarting the functions or the I/O machinery.

## Cleaner organization 🧹
- BEFORE: the app mixed the code for the web pages with the code performing the functions. Very bad practice, and a pain to maintain ("where did I put this part of the function again? In the code of the button where the user clicked... 🤦"). 
- AFTER: The code for each function is in a separate project. The front-end sends data to these projects, and receives the results from them, through a web service.

Graphically, this looks like:

![](https://docs.google.com/drawings/d/e/2PACX-1vTc-zHHvrXo9DynfUhRuD0B3TyVL7LOaW1cvKNlhPGyNJoncjjbrOuWZGRSFe0tP1x5qQ8p0ZyVJFgx/pub?w=720&h=540)

## Bonus: greater modularity allows for the release of packages 💎
The app is fully open source, which is good for auditability and accountability.
However, this doesn't mean anyone can just download the code, click on a button and run the app on their own machine. Surely doable, but not trivial. Fully open source isn't equal to fully reusable.

To make progress on this, I have started taking the most fundamental building blocks of the functions and packaging them in the standard, industry-grade way that is expected by the community of developers to re-use them.
Every programming language has their packages and their paltform to distribute them.
[RubyGems](https://www.ruby-lang.org/en/libraries/) for Ruby, [npm](https://www.npmjs.com/) for Javascript, the [CRAN](https://cran.r-project.org/) for R,  ... and [Maven Central](https://central.sonatype.com/) for Java.

It is just the beginning, and documentation is severly lacking, but it is now possible for any developer to rely on the following packages that were developed for nocodefunctions:

- [umigon-tokenizer](https://central.sonatype.com/artifact/net.clementlevallois.functions/umigon-tokenizer), to tokenize a text.
- [umigon-ngram-ops](https://central.sonatype.com/artifact/net.clementlevallois.functions/umigon-ngram-ops), to add ngrams to the words of a text.
- [umigon-model](https://central.sonatype.com/artifact/net.clementlevallois.functions/umigon-model), which contains the data structures to describe a text and analyze it further.
- [umigon-lemmatizer-lightweight](https://central.sonatype.com/artifact/net.clementlevallois.functions/umigon-lemmatizer-lightweight), which is a fast and light lemmatizer for English, Spanish and French.
- [umigon-stopwords](https://central.sonatype.com/artifact/net.clementlevallois.functions/umigon-stopwords) which provides lists of stopwords in a dozen of languages **and methods to evaluate whether an ngram containing a stopword is itself a stopword**. Also contains lists of stopwords for academic types of discourses, both in English and French.
- [utils-core](https://central.sonatype.com/artifact/net.clementlevallois.utils/utils-core), a set of helper methods. Two I keep using: an implementation of a [Multiset](https://github.com/seinecle/Utils/blob/main/src/main/java/net/clementlevallois/utils/Multiset.java) (no need of Guava for that...), and a [Clock](https://github.com/seinecle/Utils/blob/main/src/main/java/net/clementlevallois/utils/Clock.java) to compute elapsed time in a convenient way.

Nocodefunctions now relies on these packages and I keep evolving them as the application grows. I would like to thank [Maciej Walkowiak](https://twitter.com/maciejwalkowiak) whose [tutorial on how to publish a package on Maven Central](https://maciejwalkowiak.com/blog/guide-java-publish-to-maven-central/) allowed me to do it - and making it very painless. Also thanks to [JReleaser](https://jreleaser.org/) which is the tool doing the actual lifting. 

# Academic returns 🎓
One important aspect of the web application is to make it aligned with one of my professional objectives as an academic: publishing.
As stated in [the manifesto for nocode functions](https://nocodefunctions.com/blog/long-game/), my hope is that the web app will be a testbed for new data analytics projects, that will turn into publications.
After two years of development:

- one project of a book on Nocodefunctions co-authored with Veronica Espinoza - but I haven't contributed a single line yet :/
- one paper under review on text mining for marketing. This paper was directly inspired by the sentiment analysis function.
- one paper written, rejected and soon re-submitted on the lexicon-based approach of the sentiment analysis function
- one discussion with a colleague about the "organic posts detection" function, which led to me publishing this function (after a period when it was broken and dormant). Might lead to a common project?
- one project on the evolution of open source projects in management journals. I'll need the pdf matching function for it, and that's why I've improved this function recently.
  
I still need to write a paper on nocodefunctions itself - duh! - but this always seems postponed for later. If an editor reads this line and wants to send me an invitation to submit a paper, please !! :-)

And teaching? I have advertised nocodefunctions to the students I teach in various undergraduate and graduate programs at [my school](https://em-lyon.com/en). I mention it in my [methodology class for MSc theses](https://seinecle.github.io/methodology/). Not sure this is effective though, as I got no follow up email or contact on this subject. It is a shame as students conducting data analysis for their theses was an obvious use case in my view.

# Outreach 📢
[I don't monetize nocodefunctions](https://nocodefunctions.com/why.html), so my strategy to grow the traffic and usage on nocode functions is not as intense as it would be otherwise. I don't have investors breathing in my neck and I don't expect to pay the rent with it.

That said, it is only human to long for a form of recognition, and seeing traffic to the app is one of my satisfactions. These are the first things I check in the morning with my coffee and a play on Wordle! :-)

For this reason, I had already performed the essentials of SEO in the first year of the app:

- filling in the meta tags in the <header> of all the web pages of the app,
- creating intra-app links and paying attention to the text of these links

 This blog is another effort I made: created in July 2021, I published 12 posts the first year. In 2022-23, I published 11 posts (counting this one), which tend to be a bit denser. Would you guess which one is the most popular, by very far? This one on "[using java for the front-end of a web app in 2022](https://nocodefunctions.com/blog/java-frontend-web-app/)". Who would have guessed? 😁.

# Plans for next year 🔮
The app works and is very stable. My plan is to continue on growing it slowly, adding new functions suggested by users and which seem useful to the broadest numbers. Adding no function would also be fine, I would then spend my time adding more documentation to the code base and publishing libraries encapsulating the essentials of the existing functions, to make them easy to re-use by other developers. No rush! 


# Acknowledgements 🙏

![](https://media.giphy.com/media/ZfK4cXKJTTay1Ava29/giphy.gif)

This app is truly built on the shoulders of giants. Fully developed in [Java](https://www.youtube.com/watch?v=RRubcjpTkks) using [Netbeans](https://netbeans.apache.org/) as a coding tool, I thank the community for developing such a versatile, robust, easy-to-use programming language and tooling. Thanks also to all the maintainers of the libraries that provide specific features. And thanks to all the users who provided feedback, big or not, anonymously or not. Find the [detailed list of acknowledgements here](https://nocodefunctions.com/acknowledgements.html). I would like to extend a special thank to [Veronica Espinoza](https://twitter.com/Verukita1), who provided especially constructive feedbacks and suggestions, countless times. The quality of the nocode functions is in no small part the result of her help.

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

