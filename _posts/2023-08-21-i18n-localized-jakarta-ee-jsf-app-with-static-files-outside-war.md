---
layout: post
title: Make your localized JSF app more slim by placing your localized Strings outside as static files
permalink: /i18n-localized-jakarta-ee-jsf-app-with-static-files-outside-war/
published: true
date_readable:               Aug 21, 2023
last_modified_at_readable:   Aug 21, 2023
categories: [nocodefunctions,java, jsf, internatioanlization]
---
An app localized in 107 different languages gets big because of all the translated text.
I reduce the size by 30% by placing these translations outside the app - here is how.
This is a somewhat technical post on how I proceeded, and the gains it brought.

# Why externalizing the translations outside the app?
Java makes it very easy to create a localized web app, see my previous blog post on [how I translated nocodefunctions in 107 languages quickly and at not cost](https://nocodefunctions.com/blog/translated-web-app-in-107-languages-i18n/).

One of my key objectives for nocodefunctions is to make it painless to maintain and easy to extend with new features.
This broad objective is served by a several tactical goals:

- reducing the number of dependencies
- relying on well maintained, lean dependencies (aka: not Guava)
- adding tests
- decoupling strictly the view from the business logic ([the first attempt](https://nocodefunctions.com/blog/java-concurrency-with-http-client-asynch/) and now [the app is entirely decoupled](https://nocodefunctions.com/blog/nocodefunctions-second-anniversary/#cleaner-organization-))
- relying as much as I can on static files rather than on a database. So far nocodefunctions doesn't rely on a db.

Applying these principles, the frontend of the app is now a single, smallish 13Mb war file (all deps included!), which is a 10 x reduction in size compared to last year.

In such a slim app, I realized the text files containing the translations make up for 30% of it: 16 Mb uncompressed, 3Mb when compressed in the app. 
It is a bit a waste of time to include them at each compile and deployment cycle, given that it is purely static content.
What if I could put them on a separate folder, outside the app? The app would read the files at deployment time, and whenever the users would start a session.

Turns out, it is a bit harder than I thought.

# Steps to make it work
When the translations are **in** the app, the principle is pretty simple:

1. you get the language (the `Locale`) that the user wants, either as the default language of their browser or from a drop down menu.
2. you retrieve the text corresponding to this langage, using this idiom:

```java
ResourceBundle textsInOneLanguage = ResourceBundle.getBundle(<path to the folder containing all translation files in your app >, <language chosen by the user >);
```

That's it, then you can just do:

```java
textsInOneLanguage.getString("title of home page")
```

and it will return the title of the home page in the language that the user had chosen.

## Getting translated files outside the app: a different story.

JSF (the Java framework for front end dev) that I am using is placing two difficulties in the way:

- using the `ResourceBundle` as above, you can not specifiy a path to resources placed outside the app
- you would usually use a `PropertyResourceBundle` for this, but JSF doesn't accept it.

So... ? To solve the issue, my goto resource is Bauke Scholtz and Arjan Tijms's ["Definitive Guide to Jakarta Faces (the new name of JSF) in Jakarta EE 10"](https://doi.org/10.1007/978-1-4842-7310-4):

![The Definitive Guide to Jakarta Faces in Jakarta EE 10](https://github.com/seinecle/blog/assets/1244100/46c70888-e797-4c32-a76a-941b056babab)

Their solution is about loading translations from a database, not static files in a folder, but hey.
The code is pretty complicated and I didn't understand everything of it.
In the end and thanks to this head start, I could get it to work, cutting almost all the code to [one tiny file](https://github.com/seinecle/nocodefunctions-web-app/blob/master/src/main/java/net/clementlevallois/nocodeapp/web/front/i18n/I18nStaticFilesResourceBundle.java):

```java
*
 * Copyright Clement Levallois 2021-2023. License Attribution 4.0 Intertnational (CC BY 4.0)
 */
package net.clementlevallois.nocodeapp.web.front.i18n;

import jakarta.faces.context.FacesContext;
import java.io.File;
import java.net.MalformedURLException;
import java.net.URL;
import java.net.URLClassLoader;
import java.util.Enumeration;
import java.util.Locale;
import java.util.ResourceBundle;
import java.util.logging.Level;
import java.util.logging.Logger;
import net.clementlevallois.nocodeapp.web.front.backingbeans.SingletonBean;

/**
 *
 * @author LEVALLOIS
 */
public class I18nStaticFilesResourceBundle extends ResourceBundle {

    ResourceBundle rb;
    Locale current;

    @Override
    public Object handleGetObject(String key) {
        return getCurrentInstance().getObject(key);

    }

    @Override
    public Enumeration<String> getKeys() {
        return getCurrentInstance().getKeys();
    }

    public ResourceBundle getCurrentInstance() {
        Locale locale = FacesContext.getCurrentInstance().getViewRoot().getLocale();
        if (rb == null || !locale.equals(current)) {
            rb = simpleMethodToGetResourceBundle(locale);
            current = locale;
        }
        return rb;
    }

    public ResourceBundle simpleMethodToGetResourceBundle(Locale locale) {
        try {
            File i8nFolderAsFile = new File(SingletonBean.getExternalFolderForInternationalizationFiles());
            URL[] urls = {i8nFolderAsFile.toURI().toURL()};
            ClassLoader loader = new URLClassLoader(urls);
            rb = ResourceBundle.getBundle("text", locale, loader);
            return rb;
        } catch (MalformedURLException ex) {
            Logger.getLogger(I18nStaticFilesResourceBundle.class.getName()).log(Level.SEVERE, null, ex);
        }
        return null;

    }
}
```

Just a couple of notes:

 - `SingletonBean.getExternalFolderForInternationalizationFiles()` returns the path to the folder containing the .properties files, as a String 
 - the String `text` is the convention I used to name my properties file: `text_en.properties`, `text_fr.properties`, etc.

So when a user visits the app, a [SessionScoped bean is initiated](https://github.com/seinecle/nocodefunctions-web-app/blob/master/src/main/java/net/clementlevallois/nocodeapp/web/front/backingbeans/SessionBean.java
) and it triggers:

```java
        Locale locale = FacesContext.getCurrentInstance().getViewRoot().getLocale();
        I18nStaticFilesResourceBundle dbb = new I18nStaticFilesResourceBundle();
        ResourceBundle localeBundle = dbb.simpleMethodToGetResourceBundle(locale);
```

(also check the class [ActiveLocale](https://github.com/seinecle/nocodefunctions-web-app/blob/master/src/main/java/net/clementlevallois/nocodeapp/web/front/backingbeans/ActiveLocale.java), which provides the logic to change the language through a dropdown menu and through a url param).

As usual for localization in a JSF app, the `faces-bean.xml` config file must include the list of supported languages.
With translation files situated outside the app: instead of pointing to the package of the app where the properties files are located, the `<resource-bundle><base-name>` property must now point to the class extending `ResourceBundle` that you have just created (see above):

```xml
        <resource-bundle>
            <base-name>net.clementlevallois.nocodeapp.web.front.i18n.I18nStaticFilesResourceBundle</base-name>
            <var>text</var>
        </resource-bundle>
```

And... that's it.
The live version is visible at [https://nocodefunctions.com](https://nocodefunctions.com).
The [source code is on Github](https://github.com/seinecle/nocodefunctions-web-app).

# Benefits
First, I now know better how to load static property files from outside a Java web app, which is surely going to serve me again. Then:

- the app shrunk from 13.4 Mb to 10.3Mb, which is 23% smaller.
- as a result: compiling my app now takes ~ 11 seconds, as compared to ~ 17 seconds before. The fight against long builds continues! ✊
- I can now fix translations without taking the app down. Just editing the txt files, they will be taken into account next time a visitor browses the app. Great! 🌈

# Next steps
I couldn't find a documentation on this quite mainstream use case. Writing this blog post, I hope it will server future users. 

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

