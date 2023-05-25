---
layout: post
title: Speeding up pairwise comparisons to 2.8 million/sec in Java on a regular laptop
permalink: /optimizing-pairwise-comparisons-java/
published: true
date_readable:               May 25, 2023
last_modified_at_readable:   May 25, 2023
---

*Notes on coding strategies to speed up pairwise comparisons for 200,000 journals*

Pairwise comparisons go something like:

```
for each journal in journals
    visit all other journals
      so we end up examining each pair of journals
      for each pair, count how many authors have published in the 2 journals of the pair
```      

This is exceedinly simple. But if you don't find tricks to speed up things, even at 1,000 pairs examined per second, **it will take 23 days to examine all 2 billion pairs 🥲**.



# Context / goal / hardware

➡ *Context*

This is part of a project to build maps of science, similar to this one:



![Rafols, Porter and Leydesdorff, (2010), "Science overlay maps: a new tool for research policy and library management"](https://github.com/seinecle/blog/assets/1244100/1510333c-e1f4-424c-a410-65b11cb2dd81)


Th project is live streamed every Wednesday at 3pm (Paris time) [there on Twitch](https://twitch.tv/clementlevallois) and is made [fully open on Github](https://github.com/seinecle/MapsOfScience).


➡ *Goal*

Using [OpenAlex data](https://openalex.org/), I retrieved **20 million** journal articles, resulting in a **65Gb json file**.
Extracting the journal name and author ids for each article, this resulted in a list where each entry is a journal with all the authors who published in it. There are **200,000 journals** and with the list of their authors this fills a **0.9Gb file**.

Now the goal is to compute the **similarity between each pair of journals**, "similarity" being measured as the number of authors that jointly published in both.

**This makes 2 billion pairs to evaluate**: 200,000 x 200,000 divided by 2 (because when we compared journal A to B, no need to compare journal B to A again).

**The goal of this part of the project is to reduce the computation time as much as we can** on these 2B similarities.

➡ *Hardware and stack*

It is a conscious decision not to go for clusters, GPUs and cloud infrastructure if possible, in order to lower the barrier of entry for those who would like to contribute or just fork and run the project by themselves.

In this spirit, so far the project needs:

- a laptop with 8Gb of RAM
- continuous access to the Internet for a period of ~ 24h to retrieve the data from [OpenAlex](https://openalex.org/) (one time operation).

which means:
- no server, no database, no GPU, no framework.

Are we going to get stuck at the step of pair-wise comparisons, if we don't use any fancy tooling? Below is a list of tips that helped speed up computations **by a factor of 20**, the baseline being a double loop using parallel streams. It seems we  can continue working on a laptop! 😛

Do check [the resulting code](https://github.com/seinecle/MapsOfScience/blob/c9b979c05e6472fd8f53f9e6b1ef11afa9e620f8/src/main/java/net/clementlevallois/functions/mapsofscience/JournalSimilaritiesComputer.java), which is actually short.

# Tips

**--- first tips to get to the baseline ---**

## Vectors and matrices?
This was my first impulse as this is the approach I follow in [Cowo](https://github.com/seinecle/cowo-function). But that seemed like an overkill as the similarity measure being used here is a simple count on Sets, so it does not require operations on vectors.

## Handle Longs, not Strings
Journal ids and authors ids are represented [as a String by OpenAlex](https://docs.openalex.org/how-to-use-the-api/get-single-entities), but most of the String is just a url, the actual identifier is a Long Integer at the end of the url.

Hence, the first trivial operation consisted in reducing the String ids to Longs.

## Use a library to handle Longs in a memory efficient way, as primitive "long"
200,000 journals and their authors sounded like a big dataset. To be on the safe side, I did not use the Java native Collections and went directly for a library specializing in reducing the memory footprint of large collections of primitive values, also offering performances on speed.

I am using [Fastutil library](https://fastutil.di.unimi.it/), and there were several libraries I could have chosen from. Please [check this benchmark](https://github.com/Speiger/Primitive-Collections-Benchmarks/blob/master/BENCHMARKS-CHARTS.md) by [Speiger](https://twitter.com/SpeigerCut) which evaluates them.

![Some of the charts by Speiger benchmarking java libraries to handle primitive collections](https://github.com/seinecle/blog/assets/1244100/8708fb31-7a81-4d7f-88ff-e2be8faacf92)

## Don't get bothered by write operations while looping
When a similarity is computed, this result is stored as a text:

> journalA, journalB, count of common authors.

To avoid that writing this result would slow down the loop, it is just given to a queue, which is offloaded in a separate thread. This thread uses a `FileChannel` to continuously write on disk in an efficient way.

Note: I have tried using a `StringBuilder` to accumulate a significant portion of text before sending it to the disk - but it was actually slower.


**--- 💥the following tips are those which improved the baseline x 20💥 ---**

## Parallel streams or virtual threads? Both!
The two loops on the journals are managed with parallel streams.
For each pair of journals, their similarity is simply the count of their joint authors. This count is performed by a small function which is delegated to a virtual thread. Virtual threads and parallel streams work well together - and again, [check the code](https://github.com/seinecle/MapsOfScience/blob/c9b979c05e6472fd8f53f9e6b1ef11afa9e620f8/src/main/java/net/clementlevallois/functions/mapsofscience/JournalSimilaritiesComputer.java) and you'll see that it is managed in one line of code for each.

I tried to see if executor.submit() (then retrieving the `Future` value) would give better results than executor.execute(), but it did not.

## Comparison of sets of authors: not that obvious
This is a trivial part: each of the 2 journals has a group of authors. How many authors are present in the two groups? Just take the intersection of the two sets and get its size!
There are actually several ways to do this:

- use the "retainAll" method provided by the Set collection. [First it did not work](https://stackoverflow.com/questions/76326766/fastutil-operation-on-set-fails-with-long-type), then it worked but performance turned out to be disappointing.
- loop through the elements of a set, check for each element if it is contained in the other set. This is the approach that gives me the best results. Not using parallel streams as it does not give better results than a classic `Iterator`. `SplitIterator` didn't bring a performance boost either. 

Also, big gains in speed at this step came from simply looping through the **shortest** Set, not the longest - of course! Just added a check on the size of the two sets of authors at the beginning of the comparison, that's all.

## Make sure there is no unecessary boxing /unboxing 
Java conveniently provides two ways to handle large numbers:

1. a small, memory efficient `long` primitive.
2. a `Long` object which takes more memory, but is more capable in terms of methods and integration with the Java Collection framework. 

As said above I went for longs not Longs for the sake of not using much memory given the size of the dataset. But in some parts of the code, Java can implicitly turn a `long` into a `Long` to carry an operation you asked for. Boxing is converting a `long` into a `Long`, and unboxing is the reverse. This is trivial but can end up consuming precious nanoseconds, multipled many times. Making sure I consistently relied on `long` variables, not `Long`, helped improve speed.


## Tracking pairs is slow? Remove this step
In my first approach, I was checking for each pair of journals (A,B) whether I didn't not already examine (B,A). It was a necessity not to get each pair twice in the results, and also to half computations from 4 billion pairs to 2 billion!

To do that, I stored in a `Set` a number representing the pairs already examined. Then, for each new pair of journals, I checked whether it was in the `Set` or not before proceeding to the computation of their similarity. It implied:

- computing a hash for each pair, to be stored in a `Set`
- the `Set` had to be synchronized as it was accessed by parallel streams
- each new pair had to be tested with a "is it contained in the Set" before continuing.

This part seemed necessary but also an obvious drag on performance. **A simpler way consists in removing all this logic**, which will involve looping in a different way. If I have 3 journals A, B, C:

- Loop through A, B, C
- For each journal in the loop, loop through all the others **but take the next journal as a starting point - skip the ones before**. So: for A, start looping at B. For B, start looping at C. etc.

As my collections of journals are unordered sets, this approach doesn't work straightforwardly: A, B and C are not necessarily in this order in the inner loop. So it requires some fiddling to introduce a logic of indices but the result is really worth it with a large performance gain.

# Results
These different ways to gain in speed were discussed first during a [Twitch session](https://twitch.tv/clementlevallois), then with [short conversations](https://twitter.com/seinecle/status/1661467087523422208) on Twitter and [StackOverflow](https://stackoverflow.com/questions/76326766/fastutil-operation-on-set-fails-with-long-type), lots of web browsing and questions to ChatGPT.

While I did not keep track rigorously of all the changes, I kept a table of my different attempts and the results they brought.

![Informal table to keep track of my attempts on samples of 4,000 or 5,000 journals](https://github.com/seinecle/blog/assets/1244100/3430e590-1835-49fa-a490-91495c1209ac)

It started with 140,000 pairs examined per second, which would run the entire operation in less than 4 hours.

And the end result is at **2.8 million pairs examined per second, which would be equivalent to 12 minutes on a 200,000 set of journals**. Of course some degradation of performance will occur but it all should stay below the hour I guess.

# Feedback!
If you know about Java and love optimization of performance, I'd love to have your feedback! (see just below).

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [admin@clementlevallois.net](mailto:admin@clementlevallois.net) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
