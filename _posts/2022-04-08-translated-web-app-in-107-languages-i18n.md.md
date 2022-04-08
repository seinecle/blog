---
layout: post
title: Translating (localizing) my web app in 107 languages - insights
permalink: /translated-web-app-in-107-languages-i18n/
published: false
date_readable:               Apr 08, 2022
last_modified_at_readable:   Apr 08, 2022
---

_The web app is originally developed in English. Now it can be visited in any of the 107 languages offered by Google Translate and DeepL_

# An inspiration: Patrich Chew from Change.org

Early March, I was in San Francisco to guide the 120+ students of the MSc degree I manage at emlyon business school.
We spent the week listening to inspiring speakers in digital marketing and data science.
Patrick Chew was one of these speakers and he certainly made an impression on me.
Patrick is Internationalization Manager at Change.org and presented us with the opportunities and challenges of developing such an international platform in the last 10 years or so.

Change.org is internationalized in 20+ languages (if I recall correctly) and Patrick largely contributed to it with a strong kick off in 2012, moving from one language to a dozen in less than a year.
A significant part of the content and traffic at Change.org is now driven by different world regions, obviously.

And that made me thought: how cool is that! I could internationalize my website, too!
And as I don't have the same quality constraints as a company website, I  could use automated translation and scale to all available languages!

# A result: a month later, the web app is translated in 107 languages for zero € or $.

You can visit the web app, it will be localized in the defaut language of your browser.
You can then switch to any of the languages with a dropdown menu in the header and in the footer of each page:

![image](https://user-images.githubusercontent.com/1244100/162452618-72b4a2aa-6523-4e48-bce2-33ac55a6fcdd.png)

# Sharing the process

The process includes nothing extraordinary: just a good deal of patience, relying on a solid tooling, finding the right documentation, and using Google Translation and DeepL free APIs.
Let's start with the tooling.

## The tooling: Jakarta faces and Netbeans (yes!)
Jakarta Faces is the rebranding of Java Server Faces after Oracle offloaded it to the Eclipse foundation.
I suppose 90% of the readers will stop there because it isn't JS or JSF will remind them of JSP and smell like the early 2000s. You'd be wrong.

Basically Jakarta Faces is alive and kicking. Server-side rendering has come back in favor lately, and this is where Java thrives.
It is handy for everyday web development, but especially when you start a project of internationalization, as I realized.

The language is one thing, but then internationalizing a web app is also a lot about refactoring: replacing every bit of String with a placeholder property key, that will be replaced by a value in the selected language a run time.

Netbeans assisted a lot in it with:

* auto-completion of property keys
* error signaling when a property key did not exist in the propery file
* and most importantly: embedded property editor designed for internationalization. Create one property for one language, and this key gets replicated in all the language property files you created.

## The documentation
I relied quasi exclusively on Bauke Scholtz (of @BalusC's fame) and Arjan Tims' book, who have a 30-page chapter on Inernationalization in their reference book on Java EE 8 and JSF.
I absolutely recommend it, and they just publised an updated version for Java EE 10.
I'll buy it as it describes how to conveniently localize visuals in a web app, which I did,'t do yet.

![image](https://user-images.githubusercontent.com/1244100/162455448-e3ab7e66-bc31-449e-95c7-1578c3e7f62e.png)

## The sweat
I ended up:

* substituting ~ 700 pieces of text (originally in English) with a property key.
* this represents about 50,000 characters.
* across 43 html pages and ~ 20 files ("classes" in Java) in the backend

It too me a a dozen evenings for a month.

A lesson I draw from it is that:

* internationalizing a web app _when it is small and young_ feels premature and wrong (develop features and market it instead!), so nobody does it.
* internationalizing a web app _when it has grown_ quickly becomes a huge project, I suppose it is a difficult project even for well-structured companies.

So in the end, nobody does it. Have you visited a website localized in 10 languages, let alone 107, lately? (apart by the Gafams?)

The sweet spot is to do it when the technology is pretty stabilized, and when the size of the web app means that it can still be handled in a couple of months max.
__A benefit is that the effort is done just once, after the initial push all text added to the app will follow the key-value pattern and the internationalization can continue incrementally. __

## The Translation APIs
DeepL is all the rage at the moment so that's the first API I checked. Also because I still have nightmares from the doc for the Google APIs for Java.
As it turns out, DeepL provides "only" 27 target languages (including their regional variations), while Google provides more than 100 target languages:

* DeepL: https://www.deepl.com/docs-api/translating-text/
* Google Translate: https://cloud.google.com/translate/docs/languages?hl=en

### Conclusion and thanks
I will progressively refactor all the functions on [nocodefunctions.com](https://nocodefunctions.com) to adopt this design. At the moment (Feb 19, 2022), only [sentiment analysis](https://test.nocodefunctions.com/umigon/sentiment_analysis_tool.html) on the _test_ version of the site has been implemented. As a result, analyzing 6,000 tweets take just 10 seconds now (600 tweets per second!), versus ~ one minute before.

I arrived at this solution after reading many blog posts by professional Java developers and StackOverflow Q&As. I thank all these contributors, and I hope this new blog post will be of help to the next person researching these topics.
