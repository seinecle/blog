---
layout: post
title: Make your localized JSF app more slim by placing your localized Strings outside as static files
permalink: /i18n-localized-jakarta-ee-jsf-app-with-static-files-outside-war/
published: false
date_readable:               Aug 21, 2023
last_modified_at_readable:   Aug 21, 2023
categories: [nocodefunctions,java, jsf, internatioanlization]
---
An app localized in 107 different languages gets big because of all the translated text.
I reduce the size by 30% by placing these translations outside the app - here is how.
This is a somewhat technical post on how I proceeded, and the gains it brought.

# Why externalizing the translations outside the app?
Java makes it very easy to create a localized app, see my previous blog post on [how I translated nocodefunctions in 107 languages quickly and at not cost](https://nocodefunctions.com/blog/translated-web-app-in-107-languages-i18n/).

One of my key objectives for nocodefunctions is to make it painless to maintain and easy to extend with new features.
This broad objective is served by a several tactical goals:

- reducing the number of dependencies
- relying on well maintained, lean dependencies (aka: not Guava)
- adding tests
- decoupling strictly the view from the business logic ([the first attempt](https://nocodefunctions.com/blog/java-concurrency-with-http-client-asynch/) and now [the app is enitrely decoupled](https://nocodefunctions.com/blog/nocodefunctions-second-anniversary/#cleaner-organization-))
- relying as much as I can on static files rather than on a database. So far nocodefunctions doesn't rely on a db.

Applying these principles, the frontend of the app is now a single, smallish 13Mb war file (all deps included!), which is a 10 x reduction in size compared to last year.

In such a slim app, I realized the text files containing the translations make up for 30% of it: 16 Mb uncompressed, 3Mb when compressed in the app. 
It is a bit a waste of time to include them at each compile and deployment cycle, given that it is purely static content.
What if I could put them on a separate folder, outside the app? The app would read the files at deployment time, and whenever the users would start a session.

Turns out, it is a bit harder than I tought.

# Steps to make it work
When the translations are **in** the app, the principle is pretty simple:

1. you get the language (the `Locale`) that the user wants, either as the default language of their browser or from a drop down menu.
2. you retrieve the text corresponding to this langage, using this idiom:

```
ResourceBundle textsInOneLanguage = ResourceBundle.getBundle(<path to the folder containing all translation files in your app >, <language chosen by the user >);
```

That's it, then you can just do:

```
textsInOneLanguage.getString("title of home page")
```

and it will return the title of the home page in the language that the user had chosen.

## Getting translated files outside the app: a different story.

JSF (the Java framework for front end dev) that I am using is placing two difficulties in the way:

- using the `ResourceBundle` as above, you can not specifiy a path to resources placed outside the app
- you would usually use a `PropertyResourceBundle` for this, but JSF doesn't accept it.

So... ? To solve the issue, my goto resource is Bauke Scholtz and Arjan Tijms's ["Definitive Guide to Jakarta Faces (the new name of JSF) in Jakarta EE 10"](https://doi.org/10.1007/978-1-4842-7310-4):

![The Definitive Guide to Jakarta Faces in Jakarta EE 10](https://github.com/seinecle/blog/assets/1244100/46c70888-e797-4c32-a76a-941b056babab)



# Next steps
I developed this function for my research needs, so I don't have precise plans to expand it further.
Unless you provide feedback and requests! 


# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

