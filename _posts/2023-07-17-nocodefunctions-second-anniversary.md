---
layout: post
title: Nocode functions is two years old!
permalink: /nocodefunctions-second-anniversary/
published: false
date_readable:               Jul 17, 2023
last_modified_at_readable:   Jul 17, 2023
---
*[Nocode functions](https://nocodefunctions.com/) is a free, no-registration web app for click-and-point data analysis*

In this post, I celebrate the second anniversary of [nocode functions](https://nocodefunctions.com/)!

# Key facts over the past year

According to the Wayback machine, I have launched nocodefunctions [around May 2021](http://web.archive.org/web/20210503153337/https://nocodefunctions.com/).
Last year, I celebrated its [first anniversary with a blog post](https://nocodefunctions.com/blog/nocodefunctions-is-one-year-old/) - go have a look!

Read along or jump to the category that interests you the most:

1. Overall feeling
2. Overall quality, user friendliness
3. Traffic
4. Functions: what's new? what disappeared and why?
5. Long term maintainability
6. Academic returns
7. Outreach
8. What's next



# Overall feeling
![](https://i.pinimg.com/originals/4e/c1/55/4ec1557e1b7e0e996b08d9ccbf8bbaff.gif)


# Next steps

The next steps consist in going slowly and surely. The goal will remain to provide a free, no-registration, click-and-point experience to execute data analysis functions of the best quality.

I will improve the documentation, starting with submissions to academic journals that specialize in relevant topics. The doc on Github will also get some love, so that this open source project can become easily re-usable.

The Twitter import will get improved, so that we can go beyond 100 tweets (🤦) and also with a complete user-friendly access to all the subtelties of the query parameters available in the v2 of the Twitter API ([there are a lot](https://developer.twitter.com/en/docs/twitter-api/tweets/search/integrate/build-a-query)).

The code of the app will be refactored, with robustness and elegance in view. At the moment, the code of the app includes the web pages and some back-end code to make it work. The functions themselves are located in separate repos. Good, but this modular principle should be pushed a bit further, so that the codebase for nocodefunctions ends up including just the web interface, really. In particular, the logic to import files, and to export the results, should go in separate modules.

Following user reports, I will improve the UX, which remains less than perfect. The goal is to have a user complete an analysis in just a minute - the time to upload a dataset and to click on a "compute" button.

That's all I can think of for now.

# Acknowledgements

![](https://media.giphy.com/media/ZfK4cXKJTTay1Ava29/giphy.gif)

This app is truly built on the shoulders of giants. Fully developed in [Java](https://www.youtube.com/watch?v=RRubcjpTkks) using [Netbeans](https://netbeans.apache.org/) as a coding tool, I thank the community for developing such a versatile, robust, easy-to-use programming language and tooling. Thanks also to all the maintainers of the libraries that provide specific features. And thanks to all the users who provided feedback, big or not, anonymously or not. Find the [detailed list of acknowledgements here](https://nocodefunctions.com/acknowledgements.html).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

