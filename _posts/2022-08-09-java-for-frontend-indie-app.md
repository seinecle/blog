---
layout: post
title: Using java for the front-end in an indie app in 2022
permalink: /java-for-frontend-indie-app/
published: false
date_readable:               Aug 09, 2022
last_modified_at_readable:   Aug 09, 2022
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

JSF is really super simple. It is well documented thanks to [tons of Stackoverflow questions](https://stackoverflow.com/questions/tagged/jsf), a [clear official doc](https://eclipse-ee4j.github.io/jakartaee-tutorial/), many books ([this reference](https://link.springer.com/book/10.1007/978-1-4842-7310-4), and I also like the ones by [David Hellfinger](https://www.amazon.fr/Java-Application-Development-Enterprise-applications-ebook/dp/B072MFGRVF)) and of course [Youtube tutorials](https://www.youtube.com/watch?v=-Jbuy8aaLVA).

# Is JSF hard? what are the benefits?

JSF is not hard at all:

* It is well integrated with the classic IDEs for Java ([NetBeans](https://netbeans.apache.org/), [IntelliJ](https://www.jetbrains.com/idea/) and [Eclipse](https://www.eclipse.org/ide/)). Each IDE provide:
** template projects that fill in the boilerplate for the Maven config (which is dead simple, by the way).
** debbuging tools (with hot reload, for NetBeans I least)
** the usual super efficient auto-complete, refactoring, navigation and error highlighting tools of the Java ecosystem. The IDE can provide useful info on any class that you mention in an html page (like the `#{backendscript.myText}` mentioned above). Html pages are truly integrated with the rest of your codebase!**

* it handles advanced cases of actions on html pages, super easily:**
(https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/webapp/import_your_structured_data_two_columns.xhtml#L68).
** updating parts of the the page when a button is clicked? Just add [an `update` property](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/webapp/index.xhtml#L215) to your button, followed by the id of the component to be refreshed
** have a user upload a file, or multiple files, with conditions on the types of size of files, [in one line with clear parameters]
** powering your website with multiple languages? Add a [`<f:view>`](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/webapp/who.xhtml#L8) tag in your html, and retrieve the user language [with a single line in the backend](https://github.com/seinecle/nocodefunctions/blob/0fb9a250f4e33559b5e835d241e0974de7047068/src/main/java/net/clementlevallois/nocodeapp/web/front/backingbeans/ActiveLocale.java#L40)





# Primefaces: huge list of free components and themes for JSF

JSF comes with a long list of ready-to-use components that create the classic parts of an html page, so that you don't have to do it yourself.
For example, use the [`<h:dataTable>`](https://www.javatpoint.com/jsf-datatable) tag to create a table that displays some data that is loaded from your backend - no need to recreate it from scratch.

This is already super useful, but there is better: a company called [Prime Tek](https://www.primefaces.org/), which is around for a very long time, develops a suite of components called Primefaces: drop-in replacements for the regular JSF components - and they come with additional features and benefits.

Instead of the `<h:dataTable>`, just use the `<p:dataTable>` tag. It gives you a [basic data table](https://www.primefaces.org/showcase/ui/data/datatable/basic.xhtml), but you can easily add a [column toggler](https://www.primefaces.org/showcase/ui/data/datatable/columnToggler.xhtml), or [dynamic colums](https://www.primefaces.org/showcase/ui/data/datatable/columns.xhtml), or [edit functions](https://www.primefaces.org/showcase/ui/data/datatable/edit.xhtml) on the table... !! **And all this is responsive of course**.

# Alternatives

Every programming language has solid frameworks to develop the front and back end of an app, either in server side rendering or a single page applications. Python has Django, Flask and others, Javascript has Nodejs + Vue, React or Angular, ... There is a solution for every need. I just find that there is a big opportunity for Java developers, and CS students who are taught Java, to go and try JSF without looking at JS or Python as soon as it comes to the front end.






# Your feedback
I build nocode functions for you. Try it and give some feedback, I would appreciate it!

* [nocode functions](https://nocodefunctions.com) 🔎
* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
