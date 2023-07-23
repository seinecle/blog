---
layout: post
title: Speeding up pairwise comparisons from 2.8 to 80 million per sec on a regular laptop
permalink: /to-80-million-pairwise-comparisons-java/
published: true
date_readable:               Jun 12, 2023
last_modified_at_readable:   Jun 12, 2023
---

*How the advice of a user on Reddit helped increase speed by almost x 30*

Pairwise comparisons of journals go something like:

```
for each journal in journals
    visit all other journals
      so we end up examining each pair of journals
      for each pair, count how many authors have published in the 2 journals of the pair
```      


# Context / goal / hardware

-> [see previous blog post](https://nocodefunctions.com/blog/optimizing-pairwise-comparisons-java/)

# How things improved since last time: using int []

The method suggested by user [Ivory2Much](https://www.reddit.com/r/java/comments/13rlb26/speeding_up_pairwise_comparisons_to_28_millionsec/jlm0me1/) consists in not using objects nor the data structures surrounding them, in favor of working with integers in one very long array.

To recall, we want to compare pairs of journals, where the similarity of the 2 journals is measured by how many authors they have in common.

The first initialization step consists in mapping all journal ids and authors ids to ints.

Then, these journal and author ids, now represented as integers, can be stored in a single array in a way that preserves the information about which author relates to which journal:

```
[journal 1 id, number of authors for journal 1, id of 1st author of this journal, id of 2nd author, id of 3rd author, journal 2 id, number of authors for this journal, id of 1st author of this journal, etc.] 
```

(this data structure is better expressed with a simple example [in the original comment](https://www.reddit.com/r/java/comments/13rlb26/speeding_up_pairwise_comparisons_to_28_millionsec/jlm0me1/) by Ivory2Much. As the example was laid out in consecutive lines, it got me confused in thinking the array was multidimensional. But no, it is just to make it easier to read).

What's left to do is relatively trivial:

- looping through journal ids by advancing in the array, using parallelism as a bonus because the data structure doesn't get in the way.
- counting how many authors 2 journals have in common - but here again, the user suggested a simple and clever way to examine ints in the array in an economical way. 

# Results
We were at 2.8 million pairs examined per second. With this approach, we get to 80 million pairs examined per second!

In practice, for a dataset made of:

- 98,230 journals
- related to 19,343,954 authors

There are 98,230 x 98,229 pairs to be examined, divided by 2 as we examine pair A-B and not B-A again. This amounts to 9,649,034,670 (close to 10 billion) pairs to examine.
The improved algorithm takes 60 seconds to run on this dataset on a [relatively recent processor with 4 cores](https://www.intel.com/content/www/us/en/products/sku/208662/intel-core-i71165g7-processor-12m-cache-up-to-4-70-ghz/specifications.html), which amounts to 80,408,622 pairs compared per second.

The previous version run at 2.8 million pairs per second: almost 30 x slower and that was my best shot!

# Lessons learned
Personally, I found this way of doing computations quite illuminating and at odds with the discussions about GPUs, vectors and advanced algorithms as the way to get crazy speeds.
It seems that there is much, much to gain by not moving data around and by avoiding abstractions at all costs. I'd love to learn more on this - are there textbooks discussing this approach?

Also for those interested, I tried a version with virtual threads and another with a fixed thread pool and this made no discernable change.

The limits seem two-fold:

- the size of arrays: they seem limited in Java to ~ 2B elements, which is huge but this limit could be hit for larger datasets. It is probably possible to find remedies (multiple arrays?), but things would become less easy and elegant.
- the amount of RAM that is available. The computations on the example above necessitated ~ 8 Gb or RAM. That's not much actually but pairwise comparisons grow rapidly with the size of input data, so RAM might fast become an issue.

# Use it!
I am in the process of making this very fast solution available on https://nocodefunctions.com, as a free and click-and-point solution.

[The code is already available on Github](https://github.com/seinecle/similarity-function) with a permissive license. Have a look at the [test file](https://github.com/seinecle/similarity-function/blob/main/src/test/java/net/clementlevallois/functions/similarity/tests/SimilarityTest.java), which gives a how to.


# Feedback - can we improve on it?
If you know about Java and love optimization of performance, I'd love to have your feedback! (see just below).


# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I also  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
