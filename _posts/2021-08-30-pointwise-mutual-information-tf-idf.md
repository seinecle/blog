---
layout: post
title: Pointwise mutual information and tf-idf: when to use them
permalink: /pmi-tf-idf/
published: false
date_readable:               August 30, 2021
last_modified_at_readable:   August 30, 2021
---

When creating a co-occurrence network from a text or a corpus of texts, the most frequent terms will be connected *even if these connections* don't make a lot of sense.
For example, we would expect words such as "the", " and", "but"... to appear frequently, and they will co-occur frequently (often appear in the same sentences or paragraphs).

As a result, we will end up with a network where these words will be strongly connected. We would have preferred something else:

- terms that co-occur should be connected, yes
- but meaningful connections are those between *unfrequent terms that co-occur*.

Example :
• **we don't care** that "but", "the", "or"... appear frequently in the same sentence, because that is to be expected, given that they are so common throughout the text.
• **but we do care** that in a text about world capitals for instance, "Paris" and "France", though they appear unfrequently in the text, keep occurring in the same sentences.

How to automagically build a network that takes this nuance into account?

**Simple: for a pair of terms ("Paris", "France"), divide the number of time they co-occur by the total number of time each term appears in the text.**

So if:
• "Paris" and "France" co-occur 12 times in the text,
• "Paris" appears 15 times in the text,
• "France" appears 14 times in the text,

-> it means that Paris and France appear almost always together in the text! The weight of the edge between them is 12, but with the reasoning above it can be corrected to:
12 ÷ (15 + 14) = 0.41

Meanwhile, in the same text about world capitals, let's imagine that the words "but" and "if" appear in the same sentence 72 times. Not because these terms are so important in a text of world capitals, but simply because they are so common in the English language. Without a correction, we would find a big edge (weight = 72!) linking the two, bigger than the connection between Paris and France! (weight = 12).

Now let's correct:

"but" and "if" co-occur 72 times in the text,
• "but" appears 350 times in the text,
• "if" appears 170 times in the text,

-> it means that though "if and "but" appear frequently together in the text, they also appear many more times *separately* in the text as well. The weight of the edge between them is 72, but with the reasoning above it can be corrected to:

72 ÷ (350 + 170) = 0.13

-> with the correction, the pair "Paris, France" is now stronger than "but, if". Applied to all pairs of the network, this correction will lead to a much more informative result.
