---
layout: post
title: Request for feedback: developing a Best-Worst Scaling (BWS) free web app for any researcher to use 
permalink: /best-worst-scaling-bws-in-progress/
published: false
date_readable:               Nov 11, 2021
last_modified_at_readable:   Nov 11, 2021
---

### Your suggestions are welcome: I am developing a free web app for Best-Worst Scaling (BWS)

Best-Worst Scaling is a fantastic - yet still relatively underused - tool to collect data on how people compare / evaluate a list of items. That can be as diverse as:

- ordering a list of items from least preferred to most preferred (candidates, brands, places...)
- ordering a list of features from least to most important (political issues, product characteristics...)
- ordering a list of features from least to most important (political issues, product characteristics...)
- classifying statements or single terms based on how "relevant" they are on a given dimension

## Advantages of Best-Worst Scaling

There are many well established scales to do these kinds of ratings, such as this linear rating scale that is very commonly used:
<div align="center">
   <kbd>
      <img src="https://user-images.githubusercontent.com/1244100/141346470-14a43c76-3dd1-411c-8001-b65839618307.png" width="350"/>
   </kbd>
</div>
<br/>
<br/>
Best-Worst Scaling is different and introduces a smart twist. With BWS, __the respondent must choose among several options at once, and is simply asked to select the best and worst option__:
<br/>
<br/>

<div align="center">
   <kbd>
     <img src="https://user-images.githubusercontent.com/1244100/141345964-4622087f-19fc-4402-98d0-a6f623065129.png" width="350"/>
   </kbd>
</div>
<br/>
<br/>
This slight change in the design of the questions has two important benefits:

1. contrary to rating scales, there is no trouble guessing what the respondents meant with their scoring, or correcting for possible biases (such as a tendency to choose scores near the middle of the scale).
2. faster collection of data - many items are scored at once. This reduces the number of questions to be asked.

On the first point, [a recent study](https://link.springer.com/article/10.1007%2Fs10579-020-09524-2)[^1] speaks volumes: Best Worst Scaling elicits judgements which spread smoothly and "naturally" over the space of all possibilities. The study used BWS, pairwise comparison and a rating scale to ask respondents about how they value words in terms of their positive / negative "valence" ("happy" is a term with a positive valence, "depressed" in a term with a negative valence).

You would expect that respondents would find that most of the words have a neutral or quasi neutral valence. The more we go to the extreme on the positive or negative side, the fewer words there should probably be. That is indeed the case, see the graphic below. But look at the differences between the three methods: BWS (__green line__, very smooth) and rating scale / pairwise comparison (blue and red lines, pretty irregular):
<br/>
<br/>

<div align="center">
   <kbd>
     <img src="https://user-images.githubusercontent.com/1244100/141371606-6df024e3-c554-4b60-98bc-a339d61fb7b7.png" width="400"/>
   </kbd>
</div>
<br/>
<br/>
BWs is the only method which produced a smooth ranking, as should be expected. The two other methods have big ups and downs which are due to their design specificities - clearly artefacts of measurement. 

## Project: a web app to facilitate running BWS tasks
The project is driven by my need to run such a task. While many survey tools exist, few of them provide BWS scaling as a type of data collection. As far as I could see, there is no free tool.
Hence goal is to develop a free web app for BWS scaling. The advantages will be:

- a web application: makes it easy to share it with the respondents / human annotators
- responsive and mobile friendly to allow for the greatest engagement of human annotators
- free tool, for any use (academic and commercial)
- very easy to use: no complex registration or else. Just set up a task and run it

## Design of the BWS task: special attention to make it engaging to human annotators
My feeling is that using a specific type of input could have a great impact on the quality of the responses and on the engagement of the human annotators recruited on BWS tasks. Namely, designing a user interface that allows for drag-and dropping the items in a block of items to compare. The user would drag the best option to the top of the list, and drag the worst option to the bottom of the list:


![bws_ordered_list](https://user-images.githubusercontent.com/1244100/141376242-4c6806f9-7b29-4c41-898c-f8e07e3ce731.gif)






------
And discover all the other functions of the nocode functions web app: [https://nocodefunctions.com/](https://nocodefunctions.com/)

[^1]: by [Luna De Bruyne](https://research.flw.ugent.be/en/luna.debruyne) et al. to appear in the Dec 2021 issue of the journal _Language Resources and Evaluation_
