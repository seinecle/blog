---
layout: post
title: Sentiment analysis with Umigon 2.0
permalink: /umigon-upgrade/
published: true
date_readable:               Sept 20, 2021
last_modified_at_readable:   Sept 20, 2021
---

Umigon is the name of the function performing __sentiment analysis__, which I initially developed in 2012.

Umigon just got an upgrade that I will develop in this blog post, but let's first describe quickly what it does:

- sentiment analysis with three "classes" of sentiments: positive, neutral, negative
- works on texts in English or French
- focus on *sentiment*, not *negative factuals*, which is important
- for social media: short texts such as tweets, instagram comments, facebook posts. Handles hashtags, emojis and emoticons, slang and mispellings: natural language in all its forms.
- created for non coders: click and point, just send a text and it returns the result
-  free without restrictions, and available here: https://nocodefunctions.com/umigon/sentiment_analysis_tool.html
- evaluated as best in class, compared to 23 other solutions (commercial or not): https://epjdatascience.springeropen.com/articles/10.1140/epjds/s13688-016-0085-1


### Umigon: a new heuristics engine with MVEL
As described [in this paper](https://aclanthology.org/S13-2068/), Umigon's performance is based on using lists of terms which are markers of sentiment.
Obviously though, terms alone would not suffice, as in this example:

> I __like__ this brand [positive sentiment]

> Reading a book is really __like__ travelling but without taking a trip [neutral sentiment]

> I really don't __like__ this taste of ice cream [negative sentiment]

How can we distinguish between each case?

The solution consists in taking the context into account. How is "__like__" used in the sentence? For each word, Umigon can query and take into account whether:

- the preceding words in the sentence are negative, positive, or some specific words
- the following words in the sentence are negative, positive, or some specific words
- the word itself is written in caps, or appears at the beginning or end of the sentence
- etc.

These rules can of course be combined, which leads to some very precise handling of the semantics of a text.

Until now, expressing the combination of these rules was done with a simple syntax I had developed (see pages 3 and 4 of [this paper](https://aclanthology.org/S13-2068.pdf)).

However, it was crude in the sense that it could not accomodate cases where the logic was a bit involved, such as:

> "I would like this word to be a positive marker of sentiment IF it is preceded by this term AND NOT followed by this term. ELSE, consider it neutral except IF etc..."

First I thought I had to develop such a thing myself, but actually a Java project already provides it out of the box.
It is called [MVEL](https://github.com/mvel/mvel), check it out!

MVEL can handle all the boolean logic I need and as a bonus, the conditions are expressed in a language which is very natural, so that I can re-read myself easily.
One of the most complex heuristics for a term looks like:

> if(A && B && C){12} else if (C == false) {11}

Where A, B and C are true / false values that result from checks on the context of the term, and "11" and "12" are the codes for "positive marker" and "negative" marker.

### Bug fixes: minor but big impact
Umigon has been put back online in the Spring of 2021, on a web app which makes it easy for users to test their texts and report any misclassifications with just one click. I have received about 40 of such reports, which were as many tests on edge cases which I had missed. Thanks to them, I could spot and fix these issues:

- negations were not taken into account if they were one word apart from the term under examination. <code>I don't really like</code> was considered neutral because <code>don't</code> was not immediately before <code>like</code>. FIXED
- emojis following each other 🥰⛷️ were considered as one big emoji, so they escaped detection. FIXED
- the list of terms that I call "amplifiers" (<code>seriously</code>, <code>ultra</code>, <code>ridiculously</code>, <code>freaking</code>, etc.) did not load properly so it was never put in action in the heuristics where it played a role 🤦‍♂️. FIXED 
- apostrophs were breaking term detection, which is annoying given that they appear in contexts that carry rich semantics (<code>can't</code>, <code>I'm</code> ... and same in French!). FIXED
- exagerations like <code>looooove</code> were not properly handled, hence if the term was carrying a mark of sentiment (<code>love</code>) it was ignored. FIXED

### Addition of new terms
Language is constantly evolving, especially the type of oral expressions and slang which finds a written expression on social media. Umigon will never capture all of it, but it covers a pretty large scope (try it!). With new user reports, no new addition for slang but "classic" terms which were not included yet in the "negative" category - always the richest 😀:

- grotesque
- infuriating
- heart breaking
- mortifying
- on what planet
- how can

The changes have been integrated and you should see a great improvement in the results (by the way, if you conduct benchmarks on sentiment analysis, I would love to hear about it!)

------
Try Umigon here: https://nocodefunctions.com/umigon/sentiment_analysis_tool.html

And discover all the other functions: https://nocodefunctions.com/
