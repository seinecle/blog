---
layout: post
title: How to detect humor and sarcasm in texts
permalink: /detecting-humor-and-sarcasm-in-text/
published: true
date_readable:               Dec 17, 2021
last_modified_at_readable:   Dec 17, 2021
---

_On detecting sarcasm / humor: I received an email asking me how I would go about the dectection of sarcasm and humor in texts. A lot of papers on the subject have appeared but I didn't review them. I'd be interested to see what approaches are explored to date. The following is how I would approach the task:_

Sarcasm and humor are, in my opinion, cases that are very difficult to approach by machine learning. Indeed, a sarcastic or humorous connotation is revealed by very subtle clues, which are difficult to put together in an annotated training set.

On the other hand, these very subtle clues are detectable if we examine carefully:

1. the different semantic aspects of the passage (punctuation, vocabulary, grammatical structure ...)
2. the context: what comes before the text under examination, what comes after it, or even the speaker's profile (I expect the Twitter account of the United Nations to be less susceptible to sarcasm than an account coming from entertainment).

On the semantic aspects: I am a priori very confident of the fact that many sarcastic or humorous sentences leave semantic traces of their connotation - it is only very rarely 100% dependent on the context. Indeed, it is the subjective experience I have of it when I read sarcastic tweets. By re-reading them carefully, we can distinguish objectivable characteristics:

- sentence length (strongly positive sentences which are really terse can be a hint of sarcasm.)
- use of punctuation ("..." can be a hint of sarcasm)
- some vocabulary markers ("really" is a reinforcer, but "reaaaally" can be a hint of sarcasm).

So my approach would labor intensive: read a lot of sarcastic-type sentences (difficulty: where to find them easily?), and reflect on each of them. What aspects of the sentence contribute to my subjective opinion that the author is being sarcastic? And then I'd try to codify those semantic traits as I did for [Umigon](https://nocodefunctions.com/umigon/sentiment_analysis_tool.html): creating lexicons and their heuristics + sentence-level heuristics.

I understand that one can be uncertain about the effectiveness of this approach: is it really possible to list semantic markers of something as subtle as sarcasm? My response is to turn the table on this argument. When or if sarcasm is impossible to pinpoint semantically, then a computational approach cannot get a grasp on it... __but neither can humans__. To put it differently: when sarcasm is entirely context dependent (no semantic clue available), then machines and humans alike tend to be unsure about the sarcastic character of the utterance. This shows that the computational approach has not hit a limit, but instead that the person who made the sarcastic comment used to few markers to make its intentions (sarcasm or not?) entirely known.

An excellent example of this is a tweet by Elon Musk, in response to a tweet by the company

Then, we would have to develop a tool for taking into account the context, which would be "specific platform" I think. Typically, a platform that allows reactions in the form of emojis would help a lot, as one could rely on commenter's reactions such as "😆" or "😬" or "🤣" to signal that content may be humorous or sarcastic.

So that would be my starting point!
