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

# Java for the front-end - I thought the whole issue was a dead end?

Java and web browsers are often thought of as incompatible: [Java Applets](https://en.wikipedia.org/wiki/Java_applet) and [Java Webstart](https://en.wikipedia.org/wiki/Java_Web_Start) enabled java apps to be launched from the browser, and they are [now ancient history](https://www.slideshare.net/HendrikEbbers/java-webstart-is-dead-what-should-we-do-now) 💀.

Another flavor of Java in the browser are JSP or "Java Server Pages", which many computer science students learned at school.
Even if JSP is still discussed in some books on Java for the web (eg [1](https://www.amazon.com/Java-Jakarta-Recipes-Problem-Solution-Enterprise-ebook/dp/B0B6Z9JTNH), [2](https://www.amazon.com/Beginning-Jakarta-Web-Development-Applications/dp/1484258657)), it is outdated [since the 2010s](https://odoepner.wordpress.com/2015/03/11/is-jsp-an-unsupported-deprecated-part-of-jee/).

Last, there are frameworks that enable Java developers to "transpile" their code into Javascript thanks to the Google Web Toolkit (GWT, [not super fresh](https://groups.google.com/g/google-web-toolkit/c/FeEI0Rl7cyw/m/OU0HHvxtBQAJ?pli=1)) or the up-and-coming [J2Cl project](https://github.com/google/j2cl) (also by Google, very active).
GWT and J2Cl however are not meant as a beginner-friendly frameworks, they are more of enterprise toolings developed by Google, to be used by big projects in companies.

# The unsung hero of Java for the front-end: Jakarta Server Faces (JSF)!

JSF is around at least since the early 2010s, which is when I started learning coding in Java. I am always surprised it is not more famous, as it allows developing web apps in a fast, secure and robust way.

Here is how you create a web page showing some dynamic content:

- create an html page
- replace the `<head>` and `<body>` tags with `<h:head>` and `<h:body>` tags.
- display some dynamic content by calling some property in the backend, just place it after a hashtag and between handle bars: `#{backendscript.myText}`

See also [this example](https://eclipse-ee4j.github.io/jakartaee-tutorial/#a-web-module-that-uses-jakarta-faces-technology-the-hello1-example) from the official doc, which shows an input field in a form.

JSF is really super simple. It is well documented thanks to [tons of Stackoverflow questions](https://stackoverflow.com/questions/tagged/jsf), many books (I like the ones by [David Hellfinger](https://www.amazon.fr/Java-Application-Development-Enterprise-applications-ebook/dp/B072MFGRVF)) and of course [Youtube tutorials](https://www.youtube.com/watch?v=-Jbuy8aaLVA).

# Primefaces: huge list of free components and themes for JSF

JSF comes with a long list of components that create the classic parts of an html page, so that you don't have to do it yourself.
For example, use the [`<h:dataTable>`](https://www.javatpoint.com/jsf-datatable) tag to create a table that displays some data that is loaded from your backend.

This is already super useful, but there is better: a company called Prime, which is around for a very long time, develops a suite of components that are drop-in replacements for the regular JSF components - and they come with additional features and benefits.

Instead of the `<h:dataTable>`, just use the `<p:dataTable>` tag. It gives you a [basic data table](https://www.primefaces.org/showcase/ui/data/datatable/basic.xhtml), but you can easily add a [column toggler](https://www.primefaces.org/showcase/ui/data/datatable/columnToggler.xhtml), or [dynamic colums](https://www.primefaces.org/showcase/ui/data/datatable/columns.xhtml), or [edit functions](https://www.primefaces.org/showcase/ui/data/datatable/edit.xhtml) on the table... !! **And all this is responsive of course**.


# Your feedback
I build nocode functions for you. Try it and give some feedback, I would appreciate it!

* [nocode functions](https://nocodefunctions.com) 🔎
* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
