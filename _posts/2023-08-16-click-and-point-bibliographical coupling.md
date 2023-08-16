---
layout: post
title: New function - easy bibliographic coupling from an Excel file
permalink: /easy-bibliographic-coupling-bibliometric-scientometric-network-with-excel-file/
published: true
date_readable:               Aug 16, 2023
last_modified_at_readable:   Aug 16, 2023
categories: [nocodefunctions,bibliometrics,scientometrics,network,excel]
---
[A new function is available](https://nocodefunctions.com/bibliocoupling/bibliographic_coupling_tool.html): send an Excel file with titles or DOIs, receive a network based on the common references they share ("bibliographic coupling")

![screenshot of nocodefunctions.com](https://github.com/seinecle/blog/assets/1244100/71735d1a-2b5a-445f-a08c-e86900747925)

# A free, easy and transparent method to generate bibliometric networks from Excel or .txt data
The general idea behind bibliometric networks is that you want to find relations and similarities (or lack of) among the authors, publications, and organizations active in science and research.

The function presented here makes a focus on one of these networks, called **"[bibliographic coupling](https://en.wikipedia.org/wiki/Bibliographic_coupling)"**:

> **2 publications will be connected if they cite one or several references in common.**

The function is free, click and point, and fully transparent: the code is [open sourced](https://github.com/seinecle/nocodefunctions-web-app) with a Creative Commons license and the data used for the calculations can be retrieved, reused and shared.

# Existing tools: the case of VOSviewer
There are many tools which provide such a service already. Let's mention [VOSviewer](https://www.vosviewer.com/), which is the leading desktop software specializing in exactly this.
To create such a bibliographic coupling network using VOSviewer, you:

1. Click on create
2. Choose "bibliographic data / bibliographic coupling"

![the interface to create networks from bibliometric data in VOSviewer](https://github.com/seinecle/blog/assets/1244100/250dcfc1-309a-4019-9f3d-db95c0fe4fa7)

Then, choose a type of bibliometric data which will be loaded either from an API source or from a bibliometric file you have.

![the interface to fetch bibliometric data in VOSviewer](https://github.com/seinecle/blog/assets/1244100/1d58602f-6198-419c-84c7-0e1d9094b400)


# Comparison: what's new with this function?
The function just published has a few interesting features which can complement what VOSviewer already offers:

## 1. it accepts publication titles and DOIs as ways to identify the publications that you want to analyze.
My use case was that my bibliometric data is sitting in an Excel file, and it does not follow one specific bibliometric format.
It is a collage of several sources: extraction from Web of Science, my own refs stored in Zotero, and the references extracted from a publication formatted as a pdf.
How to create a bibliograpic coupling network from the 200+ refs I had in my table? I figured that using the titles of the publications, or their DOIs, was the best route.

### Publication titles: super handy  but not super accurate
A slight difference in the way an apostroph is written in a title can prevent it from being recognized: ' is not ʼ !
So don't expect to retrieve a network that will cover 100% of your publications. Titles remain a very convenient way to have a rough idea of the network that your dataset will create.

### DOIs
[Digital Object Identifiers](https://fr.wikipedia.org/wiki/Digital_Object_Identifier) are always attached to a publication these days, so you can expect that most if not all of your publications will be identified. The function accepts DOIs formatted in many forms, from the shortest to the very long:

-> 10.1016/j.ecolecon.2010.06.020

-> doi.org/10.1016/j.ecolecon.2010.06.020,

-> https://doi.org/10.1016/j.ecolecon.2010.06.020,

-> https://doi-org.em-lyon.idm.oclc.org/10.1016/j.ecolecon.2010.06.020

## 2. you can use data from an Excel or .txt file.
This is convenient if the data you handle is not formatted in a classic bibliometric format (bibtex, RIS, Zotero...).
In the case of an Excel file, just upload it, select the column where your titles or DOIs are, and you are all set.
For txt files that's even simpler: upload a txt file where there is a title or a DOI on each line (careful: for one analysis your file should contain titles or DOIs, not a mix of both.)

## 3. The output is an online visualization with the VOSviewer app and a gexf file for Gephi
As usual for [nocodefunctions.com](https://nocodefunctions.com), the output can be directly visualized and explored online (thanks to [VOSviewer online](https://app.vosviewer.com/)), or downloaded as a gexf file for further analysis in [Gephi](https://gephi.org), [NodeXL](https://www.smrfoundation.org/nodexl/) and more.

## 4. The data used for the computations can be shared
This current version of the function outputs the bibliographic coupling network.
The underlying data for creating the network is simple and could be interesting to retrieve as well: this is the list of references of each publication, which has been used to assess the similarity between any 2 publications and hence create the network.
This list of references is not shared with the user at the moment, but it could be done without too much work, as an Excel file that the user would download at the end of the analysis.
Get in touch at analysis@exploreyourdata.com if that would be something you need.

# How does it work? Thank you OpenAlex!
The function proceeds in two steps:

## a. it searches for your titles or DOIs on OpenAlex, and retrieves the references
This step happens in [this part of the code](https://github.com/seinecle/OpenAlexCitedRefs). What is [OpenAlex](https://openalex.org/)?
It is this relatively new, free data source for bibliometrics.
As of August 2023 it is not perfect in terms of coverage or data quality but [they keep improving](https://blog.ourresearch.org/new-study-shows-openalex-is-a-good-alternative-to-scopus-for-demographic-research/) and that is what you should bet on for the future.

## b. each pair of journals is compared for the references they share
This part happens in [this part of the code](https://github.com/seinecle/Gaze).
It was already written for [this other function (check option 2)](https://nocodefunctions.com/gaze/network_builder_tool.html), because similarity computations is actually a very common operation.

# Next steps
I developed this function for my research needs, so I don't have precise plans to expand it further.
Unless you provide feedback and requests! 


# About me
I am a [professor at emlyon business school](https://www.linkedin.com/in/levallois/) where I conduct research in Natural Language Processing and network analysis applied to social sciences and the humanities. I teach about the impact of digital technologies on business and society. I  build [nocode functions](https://nocodefunctions.com) 🔎, a click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Twitter: [@seinecle](https://twitter.com/seinecle) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing the app.

