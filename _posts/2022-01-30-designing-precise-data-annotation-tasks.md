---
layout: post
title: The mundane work of designing precise data annotation / labelling tasks
permalink: /designing-precise-data-annotation-tasks/
published: false
date_readable:               Jan 30, 2022
last_modified_at_readable:   Jan 30, 2022
---

Annotating or labelling data is an essential step in the chain of data processing, for at least two use cases:

* in supervised learning, labelled datasets provide a ground for the model to train on. Good annotations make good training sets, which determine the quality of the model
* in data analysis models that are "rule based", a dataset which is accurately labelled make sure the rules and heuristics get triggered in the appropriate circumstances.

Computer vision is a domain where data labelling has taken off big time.
To get good results, it is important in an initial step to provide models with examples of a "ground truth": scenes which have been annotated by humans following precise instructions, to ensure the labels they create are precise and accurate.
The analysts first train the model on these scenes, which are similar to the scenes the model will be tasked to classify and categorize, in a second step.

How is this first step (annotating a dataset) being conducted? The scene is rapidly moving.

Until ~ 2015, Amazon Mechanical Turk ([MTurk](https://www.mturk.com/)) was the dominant solution to design tasks and crowd-source them to people recruited on the same platform.
It has profoundly changed practices in the industry, and in academia as well.
In 2016, 43% of behavioral studies featured in the academic _Journal of Consumer Behavior_ were conducted on MTurk! ([^1])

MTurk is the dominant, generalist platform to design any type of crowd-sourced task - not just annotation tasks. This positon evolved:

- new actors emerged
- these actors positioned themselves on a specific segment: becoming the specialists of crowd-sourcing __annotation__ tasks.

Today, querying "annotation platform" on your favorite search engine will return the names of [Toloka](https://toloka.ai), [SuperAnnotate](https://www.superannotate.com), [Basic.ai](https://www.basic.ai), etc.

Together, these companies coalesce into a new, specific industy proposing part or all of:

- tools for annotating text, image, video, audio
- project management (curation, quality control, time management, data security, etc.)
- management of the workforce of annotators - including the setup of world-wide marketplaces 
- integration with the rest of the flow of data analysis

Amazon has followed up these developments by adding an "[Amazon SageMaker Data Labeling](https://aws.amazon.com/sagemaker/data-labeling/?nc=sn&loc=0)" (aka Amazon SageMaker Ground Truth Plus) to their MTurk offer.



![image](/images/image_labelling.jpg)

[^1]: [ Joseph K Goodman & Gabriele Paolacci (2017): Crowdsourcing Consumer Research](https://doi.org/10.1093/jcr/ucx047).
