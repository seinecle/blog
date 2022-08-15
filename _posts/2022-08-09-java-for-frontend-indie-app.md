---
layout: post
title: Using java for the front-end of a web app in 2022
permalink: /java-frontend-web-app/
published: true
date_readable:               Aug 14, 2022
last_modified_at_readable:   Aug 15, 2022
---

*This is a technical article about my positive experience as an academic developing an indie app, using Java for the front-end.
Please excuse the at-times sloppy vocabulary.*

# Java for the front-end - I thought it was a dead end?

Using Java for front-end development is often thought to be just impossible: Java is for heavy backend stuff, right?

Yes, a long time ago, [Java Applets](https://en.wikipedia.org/wiki/Java_applet) and [Java Webstart](https://en.wikipedia.org/wiki/Java_Web_Start) enabled java apps to be launched from the browser. But this is [ancient history](https://www.slideshare.net/HendrikEbbers/java-webstart-is-dead-what-should-we-do-now), as old as the Flash plugin 💀.

Even without applets, there is still a way to use Java for the front end: this is JSP or "Java Server Pages", which many computer science students learned at school.
Even if JSP is still discussed in some books on Java for the web (eg [1](https://www.amazon.com/Java-Jakarta-Recipes-Problem-Solution-Enterprise-ebook/dp/B0B6Z9JTNH), [2](https://www.amazon.com/Beginning-Jakarta-Web-Development-Applications/dp/1484258657)), it is outdated [since the 2010s](https://odoepner.wordpress.com/2015/03/11/is-jsp-an-unsupported-deprecated-part-of-jee/). Another dead end 💀 😔. 

Last, there are frameworks that enable Java developers to "transpile" (convert in a complicated way) their code into Javascript thanks to the Google Web Toolkit (GWT, [not super fresh](https://groups.google.com/g/google-web-toolkit/c/FeEI0Rl7cyw/m/OU0HHvxtBQAJ?pli=1)) or the up-and-coming [J2Cl project](https://github.com/google/j2cl) (also by Google, very active).
GWT and J2Cl however are not meant as a beginner-friendly frameworks, they are more of enterprise toolings developed by Google, to be used by big projects in companies.

# The unsung hero 🌈 of Java for the front-end: Jakarta Faces (JSF)!

Java Server Faces (JSF), **now known as "Jakarta Faces"**, is around at least since the early 2010s. I am always surprised it is not more famous and rarely mentioned, as it allows developing web apps easily in a fast, secure and robust way.

The thing works, is easy to learn, benefits from all the goodness of the Java ecosystem... yet, have you ever heard about it?

Here is how you create a web page showing some dynamic content:

- create an html page (with an extension ".xhtml")
- replace the `<head>` and `<body>` html tags with `<h:head>` and `<h:body>` tags.
- now, in order to display some dynamic content by calling some property in the backend, just place it after a hashtag and between handle bars like so:

  `#{backendscript.myText}`
  
Create a file `Backendscript.java` in your backend, add a variable called `String myText = "hi! welcome to my page!"`. It will be displayed on the web page.

JSF is really super simple.
It is well documented thanks to [tons of Stackoverflow questions](https://stackoverflow.com/questions/tagged/jsf), a [clear official doc](https://eclipse-ee4j.github.io/jakartaee-tutorial/), many books ([this reference](https://link.springer.com/book/10.1007/978-1-4842-7310-4), and I also like the ones by [David Heffelfinger](https://www.amazon.fr/Java-Application-Development-Enterprise-applications-ebook/dp/B072MFGRVF)) and of course [Youtube tutorials](https://www.youtube.com/watch?v=-Jbuy8aaLVA).

# Is JSF hard? what are the benefits?

JSF is not hard at all:

**1. It is well integrated with the classic IDEs for Java** ([NetBeans](https://netbeans.apache.org/), [IntelliJ](https://www.jetbrains.com/idea/) and [Eclipse](https://www.eclipse.org/ide/)). Each IDE provide:

  * template projects that fill in the boilerplate for the Maven config (which is dead simple, by the way).
  * debugging tools (with hot reload, for NetBeans at least)
  * the usual super efficient auto-complete, refactoring, navigation and error highlighting tools of the Java ecosystem. The IDE can provide useful info on any class that you mention in an html page (like the `#{backendscript.myText}` mentioned above). **Html pages are truly integrated with the rest of your codebase!**

**2. It handles advanced cases of actions on html pages, super easily**
  * updating parts of the the page when a button is clicked? Just add [an `update` property](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/webapp/index.xhtml#L215) to your button, followed by the id of the component to be refreshed
  * still on this question of updating / dynamic content: I just love the simplicity with JSF to have the frontend update the backend, the frontend updating itself, or the backend updating the frontend, which are basic requirements of a web app. 
  * have a user upload a file, or multiple files, with conditions on the types of size of files, [in one line with clear parameters](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/webapp/import_your_structured_data_two_columns.xhtml#L68).
  * powering your website with multiple languages? Add a [`<f:view>`](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/webapp/who.xhtml#L8) tag in your html, and retrieve the user language [with a single line in the backend](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/java/net/clementlevallois/nocodeapp/web/front/backingbeans/ActiveLocale.java#L40)
  * etc, etc.

**3. You can add and mix html tags, JS scripts, and css, and it is SEO friendly**

You have full control on the html produced by JSF and can always add vanilla html and js. This makes for an easy way to collaborate with designers and front-end developers who don't know nor care about JSF. I have tried it myself: as I suck in CSS, I got some help by a designer who could work on the html pages I had developed with JSF, without any difficulty finding their way and making the modifications they needed.

JSF generates html which you can then see and read in your browser. That helps a lot for debugging with the usual dev tools, and check that your SEO actions are well implemented.


# Primefaces: huge list of free components and themes for JSF

JSF comes with a long list of ready-to-use components that create the classic parts of an html page, so that you don't have to do it yourself.
For example, use the [`<h:dataTable>`](https://www.javatpoint.com/jsf-datatable) tag to create a table that displays some data that is loaded from your backend - no need to recreate it from scratch.

This is already super useful, but there is better: a company called [Prime Tek](https://www.primefaces.org/), which is around for a very long time, develops a suite of open source components called Primefaces: drop-in replacements for the regular JSF components - and they come with additional features and benefits.

![primefaces](https://user-images.githubusercontent.com/1244100/184534013-231ca860-a753-4556-931e-b601616cb7dc.png)


Instead of the `<h:dataTable>`, just use the Primefaces's `<p:dataTable>` tag. It gives you a [basic data table](https://www.primefaces.org/showcase/ui/data/datatable/basic.xhtml), but you can easily add a [column toggler](https://www.primefaces.org/showcase/ui/data/datatable/columnToggler.xhtml), or [dynamic colums](https://www.primefaces.org/showcase/ui/data/datatable/columns.xhtml), or [edit functions](https://www.primefaces.org/showcase/ui/data/datatable/edit.xhtml) on the table... !! **And all this is responsive of course**.

# But Java is slow and heavy?

**1. Slow**

No. The funny thing is that JS frameworks such as React, Angular and Vue emerged with the promise to be quicker and smarter than JSF by Java, because they were sending all the logic of the app at once to the browser of the vistor of the website ("the client"), in just one go, hence their names of a "single page application" (SPA) that do "client side rendering" (CSR). No need to fetch pages from the backend after this single, first step, so that's blazzing fast in theory 🏎️ (all happening in the browser, no back and forth with a distant server).

JSF works differently: when a user calls a page (such as https://nocodefunctions.com), the app in the backend generates the html for this page only and sends it back. That is called "server side rendering" (SSR).
Same happens for any page that the user will visit on the website.
Seems slow 🚜.

In practice for Single Page Applications, the time can be very long for the user to receive and load the javascript files that make the whole app.
This can lead to a bad user experience (having to wait for the 1st page to load, we have all had this experience!), and penalties in terms of SEO.
As a result, Java style Server Side Rendering gained back a new popularity as it is judged superior in terms of speed / performance than Client Side Rendering.
New [SSR frameworks emerge](https://blog.logrocket.com/improve-app-performance-react-server-side-rendering/#why-move-to-react-server-side-rendering), obliging developers used to Client Side Rendering to handle and mix these two different logics. A real pain in my opinion. Java and JSF provide SSR for ~ 15 years now - the thing is just solid, use it! 

**2. Heavy**

No. What you need to deploy a JSF app is:

- the app itself. A naked "hello world" JSF app is probably 10kb or less.
- optional: add Primefaces (discussed above) if you want more high quality components. [This represents an extra 4.5Mb](https://mvnrepository.com/artifact/org.primefaces/primefaces/12.0.0-RC2).
- that's it.

Now, run it on a server. For that, you need to:

- have a server, in the cloud or else. For the test version of Nocodefunctions ([https://test.nocodefunctions.com](https://test.nocodefunctions.com), I use Hetzner where I rent [a bare-metal server with 2Gb of RAM for € 4.15 / mo](https://www.hetzner.com/cloud). I could use less RAM but my app provides some data-intensive services and it needs to fit in memory. The real (non test) version of nocodefunctions runs on a bigger server (also with Hetzner) to the data intensive jobs of more users in parallel - at less than 50€ / mo. 
- have Java installed. That is a single download of a [less than 200Mb](https://adoptium.net/) file for Mac, Win or Linux, is [completely free even for commercial use](https://adoptium.net/docs/faq) (no "but Oracle can..." worry to have) and is a one liner / one click to install.
- have a Java web server to run. There are many. I personally use [Payara Micro (Community Edition)](https://www.payara.fish/downloads/payara-platform-community-edition/), which is free and is a single file download of 77Mb.
- launch your app. That is a one liner.

# Conclusion: consider Java!

Some programmers, I feel, think that Python, Ruby, php, nodejs + React... are the only choices when you start a small web app. I hope they will consider Java + JSF for their next project. **Especially if they learned java at school**: you will get such a head start, take advantage of it!


# Demo

I build [nocode functions](https://nocodefunctions.com) 🔎 entirely in Java. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
