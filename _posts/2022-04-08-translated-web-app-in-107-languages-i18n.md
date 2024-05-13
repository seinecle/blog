---
layout: post
title: Translating (localizing) my web app in 107 languages - insights
permalink: /translated-web-app-in-107-languages-i18n/
published: true
date_readable:               Apr 08, 2022
last_modified_at_readable:   Apr 09, 2022
categories: [localization, internationalization, java]
---

_The web app is originally developed in English. Now it can be visited in any of the 107 languages offered by Google Translate and DeepL_

# An inspiration: Patrick Chew from Change.org

Early March, I was in San Francisco to guide the 120+ students of the [MSc degree](https://masters.em-lyon.com/en/msc-in-digital-marketing-data-science) I manage at [emlyon business school](https://em-lyon.com/en).

We spent the week listening to inspiring speakers in digital marketing and data science (and that was great! see posts [1](https://www.linkedin.com/posts/levallois_the-msc-in-digital-marketing-and-data-science-activity-6906352818039476224-wLqL?utm_source=linkedin_share&utm_medium=member_desktop_web), [2](https://www.linkedin.com/posts/levallois_learningtrip-day2-sanfrancisco-activity-6906809600755032064-BZnB?utm_source=linkedin_share&utm_medium=member_desktop_web), [3](https://www.linkedin.com/posts/levallois_learningtrip-day3-sanfrancisco-activity-6907355882137509888-SNvs?utm_source=linkedin_share&utm_medium=member_desktop_web), [4](https://www.linkedin.com/posts/levallois_learningtrip-day4-sanfrancisco-activity-6907725996275974144-rBD3?utm_source=linkedin_share&utm_medium=member_desktop_web), [5](https://www.linkedin.com/posts/levallois_learningtrip-day5-sanfrancisco-activity-6907907326733381632-rBoT?utm_source=linkedin_share&utm_medium=member_desktop_web) and [6](https://www.linkedin.com/posts/levallois_learningtrip-lastday-sanfrancisco-activity-6908461012106797056-I2VI?utm_source=linkedin_share&utm_medium=member_desktop_web)).
[Patrick Chew](https://www.linkedin.com/in/patrickchew168/) was one of these speakers and he certainly made an impression on me.
He is Internationalization Manager at [Change.org](https://www.change.org/) and presented us with the opportunities and challenges of developing such an international platform in the last 10 years or so.

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/162472833-fdd35242-d2ab-47a6-b5b2-0d8f5212a6d8.png" alt="Patrick Chew" width="200"/>
</div>

Change.org is internationalized in 20+ languages (if I recall correctly) and Patrick largely contributed to it with a strong kick off in 2012, moving from one language to a dozen in less than a year.
A significant part of the content and traffic at Change.org is now driven by different world regions, obviously.

And that made me think: how cool is that! Could I internationalize my web app?
And as I don't have the same quality constraints as a company website, I  could use automated translation and scale to all available languages!

# A result: a month later, the web app is translated in 107 languages for zero € or $.

You can visit the web app ([Nocodefunctions.com](https://nocodefunctions.com)), it should be localized in the default language of your browser.
You can then switch to any of the languages with a dropdown menu in the header and in the footer of each page:

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/162452618-72b4a2aa-6523-4e48-bce2-33ac55a6fcdd.png" width="400"/>
</div>

# Sharing the process

The process includes nothing extraordinary: just a good deal of patience, relying on a solid tooling, finding the right documentation, and using Google Translation and DeepL free APIs.
Let's start with the tooling.

## The tooling: Jakarta faces and Netbeans (yes!)
[Jakarta Faces](https://start.jakarta.ee/) is the rebranding of Java Server Faces after Oracle offloaded it to the Eclipse foundation.
I suppose 90% of the readers will stop there because it isn't JS or JSF will remind them of JSP and smell like the early 2000s. You'd be wrong.

Basically [Jakarta Faces is alive and kicking](https://nocodefunctions.com/blog/java-frontend-web-app/). [Server-side rendering has come back in favor lately](https://nocodefunctions.com/blog/java-frontend-web-app/#but-java-is-slow-and-heavy), and this is where Java thrives.
It is handy for everyday web development, but especially when you start a project of internationalization, as I realized.

The language is one thing, but then internationalizing a web app is also a lot about refactoring: replacing every bit of String with a placeholder property key, that will be replaced by a value in the selected language at run time.

[Netbeans](https://netbeans.apache.org/) assisted a lot in it with:

* auto-completion of property keys
* error signaling when a property key did not exist in the property file
* and most importantly: embedded property editor designed for internationalization. Create one property for one language, and this key gets replicated in all the language property files you created.

### An aside: where and how are the localized texts stored, in all these languages?

Simply in Java properties files! No database involved, and no markdown or json. Plain text. I was afraid of escaping issues and other horrors, but nothing bad happened. Occasionnally, it made sense to leave a bit of html in the localized value. Simple tags like `<strong>` or `<a href>` links. I just left them there. The translation APIs (see below) are smart enough to identify them and leave them as is. Nice!

The entirety of the languages added about 5Mb to my packaged app (which is about 120Mb in total). Totally acceptable.

## The documentation
  
I relied quasi exclusively on Bauke Scholtz (of [@BalusC](https://stackoverflow.com/users/157882/balusc)'s fame) and Arjan Tims' book, who have a 30-page chapter on Internationalization in their reference book on Java EE 8 and JSF.
I absolutely recommend it, and they just published [an updated version for Java EE 10](https://www.amazon.com/Definitive-Guide-Jakarta-Faces-Applications-dp-1484273095/dp/1484273095/).
I'll buy this new version as it describes how to conveniently localize visuals in a web app, which I didn't do yet.

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/162455448-e3ab7e66-bc31-449e-95c7-1578c3e7f62e.png" width="300"/>
</div>

## The sweat
I ended up:

* substituting ~ 700 pieces of text (originally in English) with a property key.
* this represents about 50,000 characters.
* across 43 html pages and ~ 20 files ("classes" in Java) in the backend

It took me a a dozen evenings for a month.

A lesson I draw from it is that:

* internationalizing a web app _when it is small and young_ feels premature and wrong (develop features and market it instead!), so nobody does it.
* internationalizing a web app _when it has grown_ quickly becomes a huge project, I suppose it is a difficult project even for well-structured companies.

So in the end, the window of opportunity is pretty narrow, and nobody does it. Have you visited a non-GAFAM website localized in 10 languages, let alone 107, lately?

The sweet spot is to do it when the technology is pretty stabilized, and when the size of the web app means that it can still be handled in a couple of months max.
_A benefit is that the effort is done just once, after the initial push all text added to the app will follow the key-value pattern and the internationalization can continue incrementally at low effort and budget._

## The Translation APIs
DeepL is all the rage at the moment so that's the first API I checked. Also because I still have nightmares from the doc for the Google APIs for Java.
As it turns out, DeepL provides "only" 27 target languages (including their regional variations), while Google provides more than 100 target languages:

* DeepL: [https://www.deepl.com/docs-api/translating-text/](https://www.deepl.com/docs-api/translating-text/)
* Google Translate: [https://cloud.google.com/translate/docs/languages?hl=en](https://cloud.google.com/translate/docs/languages?hl=en)

I have written [some spaghetti code to query these APIs](https://github.com/seinecle/TranslateJavaProperties). The process for authorization for Google is less horrible than the usual.

In the end, I use Google for all languages, except for the regional versions of Portuguese (Brazil and Portugal), which DeepL alone offers. The [code is on Github](https://www.amazon.com/Definitive-Guide-Jakarta-Faces-Applications-dp-1484273095/dp/1484273095/), do have a look to see how easy it is.

The irony is that you spend literally dozen of hours refactoring small pieces of text in the web app, making zero visible progress. And suddenly when launching the calls to the APIs, the app ingests one language per minute! In less than 2 hours, all was ready.

### The money

As described above, the source language of my app is English, and it covers about 50,000 chars for the whole app (front and back end). Google Translate and DeepL both have a free tiers of 500,000 chars to translate per month. So you could translate up to 20 languages in a month, for free.

I could go quicker because I had some free credit on my Google Account, that I activated for this occasion.
Looking at the spending on this credit, it looks like I consumed the equivalent of 120€ (130$) for these translations:

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/162468427-c9dae69c-c0e6-404f-8dba-717e514c7005.png" width="400"/>
</div>

# The next steps

That was a one-time effort. I have now taken the habit, when developing new features on my app, to write it in classic code (using classic html etc) but once finished I immediately localize it:

* replacing strings with handlebars and property keys
* running the script above that fetches automatically the 107 versions of the original English text
* as these incremental developments represent a small volume of text, I'll never run past the free tiers of DeepL or Google Translate so I expect it to remain at zero cost.

I have also placed a feedback button (itself localized as well!) opening a sidebar form where users can report imperfect translations:

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/162472330-a0079c84-9d7a-41fc-9774-c5c7263ae3d8.png" width="400"/>
</div>


# Your feedback

Speaking of feedback: try the app and let me know of what you think of it! -> https://nocodefunctions.com/


