---
layout: post
title: The mundane work of designing precise data annotation / labelling tasks
permalink: /designing-precise-data-annotation-tasks/
published: false
date_readable:               Jan 30, 2022
last_modified_at_readable:   Jan 30, 2022
---

_or, why did I add annotation tasks to Nocode functions if there is so much already on offer?_

# Annotating or labelling data is an essential step in the chain of data processing, for at least two use cases:

* in supervised learning, labelled datasets provide a ground for the model to train on. Good annotations make good training sets, which impact greatly the quality of the model.
* in data analysis models that are "rule based", a dataset which is accurately labelled makes sure the rules and heuristics get triggered in the appropriate circumstances.

Annotating data consists for a person to point the absence or presence of a specific feature in a piece of text, an image, a video or audio content...
For instance, the open source solution Label Studio offers tools to annotate audio segments, by adding tags [in a very intuitive interface](https://labelstud.io/playground/):

![image](https://user-images.githubusercontent.com/1244100/151705003-f9c8212c-e76e-4550-8926-8605ca7c307f.png)

# How are annotations managed, in practice?

Until ~ 2015, Amazon Mechanical Turk ([MTurk](https://www.mturk.com/)) was the dominant solution to design tasks and crowd-source them to people recruited on the same platform.
It has profoundly changed practices in the industry, and in academia as well.
In 2016, 43% of behavioral studies featured in the academic _Journal of Consumer Behavior_ were conducted on MTurk! ([^1])

MTurk is the dominant, generalist platform to design any type of crowd-sourced task - not just annotation tasks. This positon evolved:

- new actors emerged, integrating additional services
- some actors positioned themselves on a specific segment: crowd-sourcing __annotation__ tasks.

Today, querying "annotation platform" on your favorite search engine will return the names of [Toloka](https://toloka.ai), [SuperAnnotate](https://www.superannotate.com), [Basic.ai](https://www.basic.ai), and many others.

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/151705453-f40cea8d-f5c9-4e86-8dcb-1ef3a2463718.png"/>
  <br/>
   <img src="https://user-images.githubusercontent.com/1244100/151705462-3be1f08b-caa3-4bfb-b72c-a7c3ebfafeb3.png"/>
</div>  

Together, these companies coalesce into a new, specific industy proposing part or all of:

- tools for annotating text, image, video, audio
- project management (curation, quality control, time management, data security, etc.)
- management of the workforce of annotators - including the setup of world-wide marketplaces
- integration with the rest of the flow of data analysis

Amazon has followed up these developments by adding an "[Amazon SageMaker Data Labeling](https://aws.amazon.com/sagemaker/data-labeling/?nc=sn&loc=0)" (aka Amazon SageMaker Ground Truth Plus) to their MTurk offer.



Considering all this, why did I add a tool to perform annotation tasks to [Nocode functions](https://nocodefunctions.com/)? Isn't it very redundant, given the plethora of offer? These are the reasons:

1. To be effective, annotation tasks need to be precisely taylored to the case.
2. 


[^1]: [ Joseph K Goodman & Gabriele Paolacci (2017): Crowdsourcing Consumer Research](https://doi.org/10.1093/jcr/ucx047).
