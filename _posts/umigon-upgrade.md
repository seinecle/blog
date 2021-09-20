---
layout: post
title: Sentiment analysis with Umigon 2.0
permalink: /umigon-upgrade/
published: false
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



### Umigon: a new heuristics engine
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

> "I would like this word to be a positive marker of sentiment IF it is preceded by this term AND NOT followed by this term. ELSE, consider neutral except IF etc..."

First I thought I had to develop such a thing myself, but actually a Java project already provides it out of the box.
It is called [MVEL](https://github.com/mvel/mvel), check it out!

As a bonus, the conditions are expressed in a language which is very natural, so that I can re-read myself easily.
One of the most complex heuristics looks like:

> if(A && B && C){12} else if (C == false) {11}

Where A, B and C are checks on the context of a term, and "11" and "12" are the codes for "positive marker" and "negative" marker.

The changes have been integrated and you should see a great improvement in the results (by the way, if you conduct benchmarks on solutions for sentiment analysis, I would love to hear about it!)

