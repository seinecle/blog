---
layout: post
title: Speeding up pairwise comparisons in Java on a regular laptop
permalink: /optimizing-pairwise-comparisons-java/
published: false
date_readable:               May 25, 2023
last_modified_at_readable:   May 25, 2023
---

*Notes on coding strategies to speed up pairwise comparisons for 200,000 journals*

Pairwise comparisons go something like:

```
for each journal in journals
    visit all other journals
      so end up examining each pair
      for each pair, count how many authors have published in the 2 journals of the pair
```      

This exceedinly simple. But if you don't find tricks to speed up things, even at 1,000 pairs examined per second, **it will take 23 days to examine all 2 billion pairs 🥲**.



# Context / goal / hardware

➡ *Context*

This is part of a project to build maps of science, similar to this one:

![Rafols, Porter and Leydesdorff, (2010), "Science overlay maps: a new tool for research policy and library management"](https://github.com/seinecle/MapsOfScience/blob/main/assets/img/rafols-porter-leydesdorff-2010.png)

Th project is live streamed every Wednesday at 3pm (Paris time) [there on Twitch](https://twitch.tv/clementlevallois) and is made [fully open on Github](https://github.com/seinecle/MapsOfScience).


➡ *Goal*

Using OpenAlex data, I retrieve **20 million** journal articles, from which I extracted the journal name and author ids, resulting in a **65Gb json file**.
I transformed this into a list where each entry is a journal with all the authors who published in it. There are **200,000 journals** and with the list of their authors this fills a **0.9Gb file**.

Now the goal is to compute the **similarity between each pair of journals**, "similarity" being measured as the number of authors that jointly published in both.

**This makes 2 billion pairs to evaluate**: 200,000 x 200,000 divided by 2 (because when we compared journal A to B, no need to compare journal B to A again).

**The goal of this part of the project is to go down to hours, not days** to compute these 2B similarities.

➡ *Hardware and stack*

It is a conscious decision not to go for clusters, GPUs and cloud infrastructure where possible, in order to lower the barrier of entry for those who would like to contribute or just fork and run the project by themselves.

In this spirit, so far the project needs:
- a laptop with 8Gb of RAM
- Java installed
- continuous access to the Internet for a period of ~ 24h to retrieve the data from [OpenAlex](https://openalex.org/) (one time operation).

which means:
- no server, no database, no GPU, no framework.


# Tips and results

## Handling Longs, not Strings
Journal ids and authors ids are represented as a String by OpenAlex, but most of the String is just a url, the actual identifier is a Long Integer at the end of the url.

Hence, the first trivial operation consisted in reducing the String ids to Longs.

# Using the [Fastutil library](https://fastutil.di.unimi.it/) to handle Longs in a memory efficient way, as primitive "long"
200,000 journals and their authors sounded like a big dataset. To be on tne safe side, I did not use the Java native Collections and went directly for a library specializing in reducing the memory footprint of large collections of primitive values, also offering performances on speed.

There are several libraries I could have chosen from, please [check this benchmark]([https://github.com/Speiger/Primitive-Collections-Benchmarks/blob/master/BENCHMARKS.md](https://github.com/Speiger/Primitive-Collections-Benchmarks/blob/master/BENCHMARKS-CHARTS.md)) by [Speiger](https://twitter.com/SpeigerCut) which evaluates them.

![Some of the charts by Speiger benchmarking java libraries to handle primitive collections](https://github.com/seinecle/blog/assets/1244100/8708fb31-7a81-4d7f-88ff-e2be8faacf92)


# ParallelStreams and virtual threads
The two loops on the journals are managed with parallelstreams. For each pair of journals, their similarity is measured by a count of their joint authors. This count is performed by a small function which is delegated to a virtual thread.
[I had started by thinking, should I used parallelStreams or virtual threads?, but actually nothing prevents from leveraging them both].

I tried to see if executor.submit() (then retrieving the Future value) would give better results than executor.execute(), but it did not.


# Comparison of sets of authors
This is a trivial part: each journal has a group of authors. How many authors are present in two groups? Just take the intersection of the two sets and get its size.
There are actually several ways to do this:

- use the "retainAll" method provided by the Set collection. [First it did not work](https://stackoverflow.com/questions/76326766/fastutil-operation-on-set-fails-with-long-type), then it worked but performance was not the best.
- loop through the elements of a set, check for each element if it is contained in the other set. This is the approach that gives me the best results. Not using parallel streams as it does not give better results than a classic Iterator.

Also, big gains in speed came from simply looping through the **shortest** Set, not the longest - of course! Just added a check on the size of the two sets of authors at the beginning of the comparison, that's all.

# Making sure there is no unecessary boxing /unboxing 
Java conveniently provides two ways to handle large numbers:

1. a small, memory efficient long primitive.
2. a Long object which takes more memory, but is more capable in terms of methods and integration with the Java Collection framework. 

As said above I went for longs not Longs for the sake of not using much memory given the size of the dataset. But in some parts of the code, Java can implicitly turn a long into a Long to carry an operation you need. Boxing is converting a long into a Long, and unboxing is the reverse. This is trivial but can end up consuming precious nanoseconds, multipled many times. Making sure I did not use long here, Long there in the code helped improve speed.


# Removing the break of having to write the results while looping
When a similarity is computed, this result is stored as a text:
journalA, journalB, count of common authors.

To avoid that writing this result would slow down the loop, it is just given to a queue, which is offloaded in a separate thread. This thread uses a FileChannel to continuously write on disk in a simple way.

Note: I have tried using a StringBuilder to build up a significant portion of text before sending it to the disk - but it was actually slower.


# Removing the break of having to write the results while looping
When a similarity is computed, this result is stored as a text:
journalA, journalB, count of common authors.

To avoid that writing this result would slow down the loop, it is just given to a queue, which is offloaded in a separate thread. This thread uses a FileChannel to continuously write on disk in a simple way.

Note: I have tried using a StringBuilder to build up a significant portion of text before sending it to the disk - but it was actually slower.




# About me

I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
