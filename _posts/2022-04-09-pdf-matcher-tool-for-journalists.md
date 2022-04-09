---
layout: post
title: Publishing a free in-browser tool to mine pdfs on a precise keyword or expression
permalink: /pdf-matcher-tool-for-journalists/
published: false
date_readable:               Apr 09, 2022
last_modified_at_readable:   Apr 09, 2022
---

_A new function has been added to Nocodefunctions.com in response to a need by journalists _

# The need: helping journalists sift through pdfs

Early April, journalist Runa Sandvik posted:

<blockquote class="twitter-tweet" data-dnt="true"><p lang="en" dir="ltr">Imagine having 1000 PDFs and needing to find those with specific keywords. Here’s a tool many, many journalists need that someone could easily write and share. 🔍🗞<br><br>- Take PDFs as input<br>- Convert to text <br>- Search for keywords (UTF-8)<br>- Output result as CSV</p>&mdash; Runa Sandvik (@runasand) <a href="https://twitter.com/runasand/status/1510246476315865095?ref_src=twsrc%5Etfw">April 2, 2022</a></blockquote>

It felt like a feature Nocodefunction.com was well positioned to offer. So I ended up developing it in exactly a Sunday afternoon, and you can now find it here:

[https://nocodefunctions.com/pdfmatcher/pdf_matcher_tool.html](https://nocodefunctions.com/pdfmatcher/pdf_matcher_tool.html).

I reported it to Runa:

<blockquote class="twitter-tweet" data-conversation="none" data-dnt="true"><p lang="en" dir="ltr">Hi, please find the function here:<a href="https://t.co/N9oM7dBOPN">https://t.co/N9oM7dBOPN</a><br><br>The export to Excel stalls for some reason but otherwise the results can be seen on the page. Please submit bug reports etc. to analysis@exploreyourdata.com<br><br>(free to use, respectful of the data, of course!)</p>&mdash; Clement Levallois (@seinecle) <a href="https://twitter.com/seinecle/status/1510661117768515586?ref_src=twsrc%5Etfw">April 3, 2022</a></blockquote>

... and was disappointed to get no reply. But looking back at the original post, I realized it got tons of replies (91 so far), with "less than helpful comments" but also pointers to useful resources.

I'll post links to them here for your convenience, noting whether they are desktop solutions 💻, browser-based ☁️ or command-line interfaces 🔤 and whether it is free ✔️ or not 💰:

<ul>
  <li>[Documentcloud](https://www.documentcloud.org/home)  ☁️ ✔️</li>
  <li>[Google Drive](https://drive.google.com)  ☁️ ✔️</li>
  <li>[Google Journalist Studio's Pinpoint](https://journaliststudio.google.com/pinpoint/about)  ☁️ ✔️</li>
  <li>[Aleph](https://docs.alephdata.org/)  💻 ✔️</li>
  <li>[Open Semantic Search](https://opensemanticsearch.org/)  💻 ✔️</li>
  <li>[pdfind](https://github.com/dolanor/pdfind)  🔤 ✔️ (linux and mac)</li>
  <li>[pdfgrep](https://pdfgrep.org/)  🔤 ✔️ (linux)</li>
  <li>[Acrobat DC](https://www.adobe.com/fr/acrobat/acrobat-pro.html)  💻 💰</li>
  <li>[dnGrep](https://dngrep.github.io/)  💻 ✔️ windows only</li>
  <li>[ripgrep-all](https://github.com/phiresky/ripgrep-all)  🔤 ✔️ linux mac windows</li>
  <li>[Agent Ransack](https://www.mythicsoft.com/agentransack/)  💻 ✔️ windows only (freemium)</li>
  <li>[🤖 PDF Keywords Extractor 🤖](https://github.com/bendersej/pdf-keywords-extractor)  💻 ✔️  not sure which platforms are supported?</li>
  <br/>
  <p>and the solution I developed! :-)</p>
  <li>[🎯 pdf matcher tool](https://nocodefunctions.com/pdfmatcher/pdf_matcher_tool.html)  ☁️ ✔️</li>
</ul>    


# Your feedback

Speaking of feedback: try the app and let me know of what you think of it! -> https://nocodefunctions.com/


