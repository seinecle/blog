---
layout: post
title: Six different visions for the future of generative AI
permalink: /visions-generative-ai/
published: true
date_readable:               Oct 12, 2023
last_modified_at_readable:   Oct 12, 2023
categories: [chatgpt,llm,artificial intelligence,artificial general intelligence,prospective]
---
Seizing the nature and consequences of generative AI is an exercise in speculation. But we can speculate with method.

> in the following I use "ChatGPT", "LLM" and "generative AI" interchangeably because ChatGPT and Large Language Models (LLMs) are front examples of generative AI.

# The consequences of generative AI - why do we care?
For the sake of keeping this blog post short, I'll just mention that Geoffrey Hinton, who is a key contributor to generative AI, compared it to the invention of electricity, or [even the invention *of the wheel*](https://youtu.be/qpoRO378qRY?feature=shared&t=2295):

<iframe width="560" height="315" src="https://www.youtube.com/embed/qpoRO378qRY?si=E5QZ42mq7n8m3A4f&amp;start=2295" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen> 
</iframe>

So we should probably pay attention and as the interviewer said, "let's buckle up".

# How to explore the consequences of a radically new fundamental technology? Caveats
I must say I lack the experience that academics and colleagues possess in exactly this topic, with [Philippe Silberzahn on how to face disruptive innovations](https://philippesilberzahneng.com) or [Thomas Gauthier on conducting far reaching prospective studies](https://www.linkedin.com/in/thomas-gauthier-1473b62/).
I will simply list and organize the different influential visions for generative AI that I have read and encountered in the past months.

The goal is very modest: it is to provide a panorama of visions by people whose opinions are usually well informed. I do it to develop [my own thoughts on the consequences of ChatGPT](https://nocodefunctions.com/blog/chatgpt-consequences/), and hopefully you will find it useful too.
Let us not forget that of course, each of them have a stake in the debate, and that their voice is performative: by articulating a vision, they contribute to this vision becoming reality, even modestly.

# The visions (in no particular order)

## 1. Noam Chomsky: generative AI is not true intelligence

### Who?
[Noam Chomsky](https://en.wikipedia.org/wiki/Noam_Chomsky), key contributor to linguistics in the second half of the XXth century and public intellectual.

### Source
Op-ed in the New York Times: ["Noam Chomsky: The False Promise of ChatGPT"](https://www.nytimes.com/2023/03/08/opinion/noam-chomsky-chatgpt-ai.html)

Date: March 8, 2023 ([full version in pdf](https://drive.google.com/file/d/1kuggyRlT5eqlqqZ0ad25CpdAvXvetMbi/view)).

### Argument
ChatGPT is good at mimicking discourse. True intelligence, reasoning, remains qualitatively different from what ChatGPT does. Chomsky elaborates:

> Here’s an example. Suppose you are holding an apple in your hand. Now you let the apple go. You observe the result and say, “The apple falls.” That is a description. A prediction might have been the statement “The apple will fall if I open my hand.” Both are valuable, and both can be correct. But an explanation is something more: It includes not only descriptions and predictions but also counterfactual conjectures like “Any such object would fall,” plus the additional clause “because of the force of gravity” or “because of the curvature of space-time” or whatever. That is a causal explanation: “The apple would not have fallen but for the force of gravity.” That is thinking. 

It seems that ChatGPT (and Bard too, I didn't check) are well able to display such a reasoning. This is [the transcript of my attempt on ChatGPT today](https://chat.openai.com/share/437a046c-e7f2-4bf2-bb21-33d700d8254a):

> Suppose you are holding an apple in your hand. Now you let the apple go. What will happen and why?

> If I were a physical entity capable of holding an apple, and I were to let it go, the apple would fall to the ground due to the force of gravity. Gravity is a fundamental force of nature that pulls objects with mass towards each other. In this case, the Earth's gravity would pull the apple towards its center. When you release the apple, there are no other forces counteracting gravity (assuming we are neglecting air resistance in this scenario). Therefore, the gravitational force will cause the apple to accelerate towards the Earth at a rate of approximately 9.81 meters per second squared (on the surface of the Earth). This acceleration continues until the apple hits the ground or encounters some other obstacle that might affect its motion. [the answer continues with a precise description of the law of universal gravitation, which I skip here for brievety].

### My personal opinion
I tend to flatly disagree with Chomsky here, which is embarrassing because who am I to disagree with such a great mind. I would think that yes, generative AI is not the same kind of intelligence as a human intelligence. But that does not prove generative AI is incapable of reasoning. It can achieve reasoning through different (non biological) means, namely the gigantic number of statistical associations stored in the model that the generative AI is.

## 2. Andrej Karpathy: generative AI as "the kernel process of a new Operating System"

### Who?
[Andrej Karpathy](https://en.wikipedia.org/wiki/Andrej_Karpathy) was a Director of AI at Tesla and as of today, he is working at OреոΑӏ (the company which released ChatGPT).

### Source
A tweet from his personal account

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">With many 🧩 dropping recently, a more complete picture is emerging of LLMs not as a chatbot, but the kernel process of a new Operating System. E.g. today it orchestrates:<br><br>- Input &amp; Output across modalities (text, audio, vision)<br>- Code interpreter, ability to write &amp; run… <a href="https://t.co/2HsyslOG2F">pic.twitter.com/2HsyslOG2F</a></p>&mdash; Andrej Karpathy (@karpathy) <a href="https://twitter.com/karpathy/status/1707437820045062561?ref_src=twsrc%5Etfw">September 28, 2023</a></blockquote>

Date: September 28, 2023

### Argument
GPT-4, which is the generative AI behind ChatGPT, is not merely a "model that produces good chatbots". If we consider that the text it generates is not just passive reading material for humans, but text which can then be fed as "instructions" or "commands" to other computing systems such as apps (including to... itself 🤯), then a better describer for GPT-4 would be that it is an operating system (à la Windows, iOS, Android, Linux), or even best, **the central orchestrator in such an operating system** (technically called a ["kernel"](https://en.wikipedia.org/wiki/Kernel_(operating_system))).

### My personal opinion
The development of plugins and apps for ChatGPT ([since April 2023](https://www.youtube.com/watch?v=mpnh1YTT66w)) and Bard ([since September 2023](https://blog.google/products/bard/google-bard-new-features-update-sept-2023/)) points indeed to this model.
The immense stream of revenues that would be generated from replicating the logic of an App Store to generative AI does provide the incentives for companies to push in this direction.
Karpathy does point that this analogy, by necessity, sticks to known mental models (what is a kernel, what is an app store), and that we should expect unexpected developments beyond these models.
I also agree with this: we don't know what is the magnitude of the changes that such a technology will enable. In my view, the change is comparable to the [the move from analogical to digital systems](https://nocodefunctions.com/blog/chatgpt-consequences/).


## 3. Mustafa Suleyman: containment is needed

### Who?
[Mustafa Suleyman](https://en.wikipedia.org/wiki/Mustafa_Suleyman) was the cofounder of DeepMind which developed AlphaGo, the system that beat the best player at the game of Go in 2015. He then became vice president of AI product management and AI policy at Google. He is now co-founder and CEO of [Inflection AI](https://inflection.ai/), which develops personal assistants with generative AI.

### Source
["The Coming Wave"](https://www.amazon.com/Coming-Wave-Technology-Twenty-first-Centurys/dp/0593593952), a book praised by a vast array of scientists, entrepreneurs and key opinion leaders.

![image](https://github.com/seinecle/blog/assets/1244100/745f71bc-31af-4590-a535-f38fdbfcde49)

Date: published in September 2023

### Argument
Generative AI will cause major disruptions at the societal level in the short term (5 to 10 years). Not because it will become super human (AGI) though it might, but because it is already an ACI (Artificial Capable Intelligence). Generative AI enables the development of intelligent agents at low cost and "en masse". Dilemna: this will probably create many good things, however it will be very hard to contain its nefarious uses because software is harder to trace than say, nuclear material.

### My personal opinion
Suleyman's argument is of course richer than the summary above, and includes descriptions of the risk of cheap synthetic biology, too.
I personally agree with the arguments of the book, even if they sound dramatic.
It is pretty pessimistic in the sense that it does not cheer up with an easy solution to the problems (the catastrophies, really) that he predicts.
"Containment" is the general direction he advocates, but containing AI is impossible to do or if done at full force, that would be at the price of our personal liberties (states tightly controlling what individuals do with IT).

## 4. Jony Ive: towards the new iPhone?

### Who
[Jony Ive](https://en.wikipedia.org/wiki/Jony_Ive) was Apple's lead designer from to 2015 to 2019, and contributed centrally to designing the series of iPhones.

### Source
["OpenAI and Jony Ive in talks to raise $1bn from SoftBank for AI device venture"](https://www.ft.com/content/4c64ffc1-f57b-4e22-a4a5-f9f90a7419b7), published by the Financial Times.

![image](https://github.com/seinecle/blog/assets/1244100/f542e191-4197-42cf-8841-f4c2f718a4d7)

Date: September 28, 2023

### Argument
ChatGPT opens a new era for user interactions, which feel different from the user interactions on mobile phones we have been used to: typing a prompt, reading the answer, and acting on it, is quite different from interacting with apps at the tap of our fingers. **This is very conditional**: Jony Ive **would be** talking to OpenAI and Softbank on the development of a device that would actually fit this new type of user interaction, and would deliver a better user experience than the textual chat interface which is now largely dominating our interactions with generative AI.

### My personal opinion
Yes there is definitely a need for a new type of interface. It feels so quaint to type long questions on the keyboard, and see the textual response. *Voicing* a prompt would seem the natural way: quicker, less formal than writing, and more precise because we could hesitate and rephrase while prompting. Choosing the format of the output would seem natural, too. Voice, text, writing to a file, searching a document on the phone and displaying it, or executing a command (opening and using an app, checking an agenda, sending an email, etc). A couple of random thoughts:

- personal conversational assistants, such as Siri or Alexa, seem like the natural starting point for such an interface
- a difficult issue is the use of voice in public space: we are all texting while commuting for instance, but I am pretty sure we are not ready to interact by speaking aloud to our phones while in the bus or subway. Thinking of that freely, I was thinking that "whispering as an interface" might then become a thing. You would whisper or murmure to your phone when interacting with it in public spaces. It paints a grim picture of our social interactions 😬 but it could solve the issue of voice interactions.
- SoftBank being involved as an investor in this potential project [sounds like the kiss of death 😅](https://www.ft.com/content/0e375355-85c7-4c4e-87fc-5e73ac268196).

## 5. Clément Delangue: no tsunami, lots of localized AIs

### Who
[Clement Delangue](https://www.linkedin.com/in/clementdelangue/) is co-founder & CEO at [Hugging Face](https://en.wikipedia.org/wiki/Hugging_Face), the company which made it so much easier to train, host and share models in AI - including in generative AI.

### Source
These posts on LinkedIn:

<iframe src="https://www.linkedin.com/embed/feed/update/urn:li:share:7117498531065511937" allowfullscreen="" title="Embedded post" width="504" height="399" frameborder="0"></iframe>

<iframe src="https://www.linkedin.com/embed/feed/update/urn:li:share:7112524133564870657" allowfullscreen="" title="Embedded post" width="504" height="588" frameborder="0"></iframe>

And a repost by Clément Delangue of this post by Yann Le Cun, Chief AI Scientist at Meta: 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">The heretofore silent majority of AI scientists and engineers who<br>- do not believe in AI extinction scenarios or<br>- believe we have agency in making AI powerful, reliable, and safe and<br>- think the best way to do so is through open source AI platforms<br>NEED TO SPEAK UP ! <a href="https://t.co/geptca8idf">https://t.co/geptca8idf</a></p>&mdash; Yann LeCun (@ylecun) <a href="https://twitter.com/ylecun/status/1711780316652990766?ref_src=twsrc%5Etfw">October 10, 2023</a></blockquote>

Date: September - October 2023

### Argument
The claims of an existential risk to humanity (posed by generative AI) are greatly exaggerated. Exagerated as well are the claims that AI, even when not AGI, is bound to cause severe troubles. Instead, what the future holds if we choose it, is an economy where companies and organizations develop and use special purpose AI models (generative or not), trained on datasets which reflect the particularities of their local context. The sharing of open source models of AI is one guarantee that AI becomes available to all and stays under the scrutiny of all.

### My personal opinion
I tend not to be convinced by this argument, for at least two reasons.

The first is that there are scenarios of generative AI getting super dangerous, which can't be evacuated by the argument above. Autonomous weapons on the battle field? [That seems pretty likely](https://www.defensenews.com/unmanned/2023/10/09/us-army-developing-integrated-formations-of-robots-and-humans/). Exploitation of the attention and emotions of customers, for the sake of the generation of ad revenues, with content / apps / bots powered by generative AI? Seems likely to me as well. Clement Delangue seems worried as well, actually:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Having worked on conversational AI in the past, I think that with the current capabilities, we should strongly discourage &amp; warn about the anthropomorphism and leverage of psychology patterns of users by chatbots. <br><br>For thousands of years, we&#39;ve been used to be able to have good… <a href="https://t.co/umlPKFq85M">https://t.co/umlPKFq85M</a></p>&mdash; clem 🤗 (@ClementDelangue) <a href="https://twitter.com/ClementDelangue/status/1710349025793159338?ref_src=twsrc%5Etfw">October 6, 2023</a></blockquote> 

The second reason for not being convinced by the alternative vision of companies each training localized versions of open source, smaller LLMs, instead of using one general-purpose, expensive and private GPT-4: the argument sounds like a straight defense of the business model of Hugging Face, which is about hosting a large number of models, as opposed to one hegemonic Bard or ChatGPT. In my personal experience using ChatGPT or Bard, it is very hard to scale down to less powerful models once you have experienced the quality of their seemingly near perfect human interaction.

So we'll see where things go. The terms of the argument ("specialized models because trained on local datasets" vs general models) might well evolve: what if OpenAI would offer versions of GPT-4 that you could then train and specialize on extra datasets? (if they don't already?). That would make the alternative void (either ChatGPT or less powerful models on Hugging Face).

## 6. Yuval Noah Harari: existential threat to humanity

### Who?
[Yuval Noah Harari](https://en.wikipedia.org/wiki/Yuval_Noah_Harari), author of the book [Sapiens](https://en.wikipedia.org/wiki/Sapiens:_A_Brief_History_of_Humankind) in 2011.

### Source
Several interviews and debates, eg:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Author of Sapiens, Homo Deus &amp; Unstoppable Us, Yuval Noah Harari (<a href="https://twitter.com/harari_yuval?ref_src=twsrc%5Etfw">@harari_yuval</a>) and Financial Times&#39;, Gillian Tett (<a href="https://twitter.com/gilliantett?ref_src=twsrc%5Etfw">@gilliantett</a>) discuss if AI could drive humans to extinction <a href="https://t.co/S7WeCqM73Y">https://t.co/S7WeCqM73Y</a> <a href="https://t.co/COBibcYPFi">pic.twitter.com/COBibcYPFi</a></p>&mdash; CogX Festival (@CogX_Festival) <a href="https://twitter.com/CogX_Festival/status/1709670282099634337?ref_src=twsrc%5Etfw">October 4, 2023</a></blockquote>

["Yuval Noah Harari argues that AI has hacked the operating system of human civilisation"](https://www.economist.com/by-invitation/2023/04/28/yuval-noah-harari-argues-that-ai-has-hacked-the-operating-system-of-human-civilisation) (The Economist)

![image](https://github.com/seinecle/blog/assets/1244100/ff243ed4-a1da-44ca-8cb5-6f195630c794)

Date: April - October 2023

### Argument
A model in generative AI is capable of getting out of hands of the humans who created it. If that happens and in the worst case scenario, this model could pursue its own objectives, which would not necessarily be compatible with human's welfare.

### My personal opinion
I would tend to side with this opinion. People arguing that this overly pessmistic, dramatic and overall ill founded, tend to bring several arguments forward:

1. people making the argument for an existential risk [are not engineers, they use sloppy arguments and imprecise vocabulary, they don't know what they talk about](https://twitter.com/ylecun/status/1711780316652990766)
2. there is an agenda by some making these claims, to close up AI and keep it to a handful of monopolies (the GAFAMs)
3. those who know about LLMS know that they are far from truly intelligent, purposeful, self reflexive AGIs (this is a variation on argument 1.)

To which I would reply:

1. the argument about who is a true engineer or not seems pretty bad. I give all the credit to Yuval Harari to be able to express a sensible opinion on LLMs. Mustafa Suleyman, who expresses similar opinions (see above), is a cofounder of Google's DeepMind: good enough credentials.
2. This is true that (anti-)competitive dynamics are very strong. Microsoft, Google and a couple of others probably dream to see the ecosystem of generative AI being closed up to a small club composed of... themselves, to reproduce the walled gardens that they are used to enjoy. That said: it does not follow that generative AI is inocuous.
3. AGI or not? The term "AGI" is so poorly defined that the debate is moot. Suleyman introduced the term "Artifical Capable Intelligence" to distinguish between today's LLMs, and an super intelligent one. To clarify these issues, I have written a short [blog post trying to list the features defining an AGI](https://nocodefunctions.com/blog/chatgpt-agi/). LLMs check most of them.

# Next
The goal of this blog post was simply to gather in one place some influential opinions on the consequences of ChatGPT, LLMs and generative AI in general, as of October 2023.
What did we learn?

- a diring absence of women's voices, and other minorities. That reflects the biases of my sources of information.
- a lack of consensus on the effects of generative AI: dramatic or not
- the involvement of the GAFAMs and a recent entrant (Hugging Face) in the debates: competitive dynamics are clearly at play, with the topic of the regulation of AI being perceived by the new entrants as a potential form of [regulatory capture](https://en.wikipedia.org/wiki/Regulatory_capture) used to clip their wings. At least that is what I read implicity in the debates about the necessity to keep AI open or to contain it.

# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.
