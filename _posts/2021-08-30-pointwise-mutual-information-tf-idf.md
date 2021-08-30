---
layout: post
title: Pointwise mutual information and tf-idf: when to use them
permalink: /pmi-tf-idf/
published: false
date_readable:               August 30, 2021
last_modified_at_readable:   August 30, 2021
---

### The problem with co-occurrences: lots of noise

When creating a network from a text or a corpus of texts, the logic is to keep only the most frequent terms, the links betwee any two terms representing how many times they "co-occur" in the text (that is, two terms which appear in the same sentences or paragraphs will have a strong connection between them).

The problem is, most frequent terms in these texts will be connected *even if these connections* don't make a lot of sense.

For example, we can expect words such as "the", "and", "but"... to be frequently used in any text in English. Just because they are so frequent, they will appear frequently together as well.

As a result, when building a network of co-occurring terms, these very common words will be strongly connected. We would have preferred something else:

- terms that co-occur should be connected, yes
- but meaningful connections are those between *unfrequent terms that co-occur*.

Example :

- **we don't care** that "but", "the", "or"... appear frequently in the same sentence, because that is to be expected, given that they are so common throughout the text.
- **but we do care** that in a text about world capitals for instance, "Paris" and "France", though they appear **unfrequently** in the text, keep occurring **frequently** in the same sentences.

How to automagically build a network that takes this nuance into account? Simple: for a pair of terms ("Paris", "France"), divide the number of time they co-occur by the total number of time each term appears in the text. This is one variant of "Pointwise Mutual Information" and it is explained very simply below:

### Pointwise mutual information: the solution to discount edges with low information

Let's imagine a very long text discussing all the world capitals:

- in **12** sentences, "Paris" and "France" are both mentioned,
- "Paris" appears **15** times in the entire text,
- "France" appears **14** times in the entire text,

-> it means that Paris and France appear almost always in the same sentences (they "co-occur"), and very rarely in different sentences! The weight of the edge between them is 12, but with the reasoning above it can be corrected to:

> **12** ÷ (**15** + **14**) = 0.41

Meanwhile, in the same text about world capitals, let's imagine that the words "but" and "if" appear in the same sentences 72 times. Not because these terms are so important in a text of world capitals, but simply because they are so common in the English language. Without a correction, we would find a big edge (weight = 72!) linking the two, bigger than the connection between Paris and France! (weight = 12).

Now let's correct:

"but" and "if" co-occur **72** times in the text (there are 72 sentences that include both "but" and "if"),

- "but" appears **350** times in the text,
- "if" appears **170** times in the text,

-> it means that though "if and "but" appear frequently together in the text, they also appear many more times *separately* in the text as well. The weight of the edge between them is 72, but with the reasoning above it can be corrected to:

> **72** ÷ (**350** + **170**) = 0.13

-> with the correction, the pair "Paris, France" (strength: 0.41) is now stronger than "but, if" (strength: 0.13). Applied to all pairs of the network, this correction will lead to a much more informative result.

What we did here is using a variant of the method called **Pointwise Mutual Information**. The [Wikipedia entry for PMI](https://en.wikipedia.org/wiki/Pointwise_mutual_information) is pretty complex but explains the same principles I presented here.

### An example
I used a variant of PMI in a study of the scientific articles in the field of neuroethics. We first categorized each article according to one or several broad subject categories they were discussing (legal studies, neuroimaging, philosophy of mind, etc.). Then, we wondered: which subject categories "co-occur", meaning: which which subject categories tend to be often discussed together (by the same papers). If I din not apply the PMI correction, then the most freqent subject categories would have been associated, and the less frequent ones would have had weak associations *simply because of this frequency effect, hiding the fact that subject categories rarely discussed in articles actually tend to be discussed in the ***same papers***.
Any how, this is the network we ended with:

![A network of co-occurring subject categories corrected with a PMI method][network]

[network]: https://www.ncbi.nlm.nih.gov/pmc/articles/instance/4929847/bin/fnhum-10-00336-g0004.jpg "A network of co-occurring subject categories corrected with a PMI method"

### Want to use Pointwise mutual information to improve your networks?
[Nocode functions](https://nocodefunctions.com) offers a function which [turns texts into networks](https://nocodefunctions.com/cowo/semantic_networks_tool.html). It includes a PMI correction which is slightly more agressive than the one presented above. It does:

> Corrected weight = weight of cooccurrence (A,B) ÷ (count of A x count of B).

(so the only thing we did as compared to the example above is to use a multiplication instead of an addition).

Questions? [Ping me on Twitter!](https://twitter.com/seinecle)
