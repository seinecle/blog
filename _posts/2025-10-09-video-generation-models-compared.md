---
layout: post
title: "Comparing video generation models with a childhood memory"
permalink: /video-generation-models-compared/
published: true
date_readable: October 9, 2025
last_modified_at_readable: October 9, 2025
categories: [AI, genAI, video, video generation, benchmark, comparison]
---
Comparing Wan, VEO, SORA, LUMA and GROK with a paper boat navigating on a mountain torrent.

Prompt (I am not a native English speaker and was too lazy on that one to check for correctness) :

```
Make a video of a paper boat descending and whirling in a natural torrent water stream from the Alps.

A few natural rocks are in the torrent, the torrent is small and the banks are made of herb, flowers, small bushes, in spring season.

No wild life.

Just the boat descending on the stream, with realistic physics for lights, water and boat movements: it whirls, slows down and goes faster depending on the current.
```

*All generations are first try*

**Except for LUMA the video generation also generates sound, so please SOUND ON on the videos.** 

### RAY3 (by Luma Labs AI)

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%;">
  <iframe 
    src="https://www.youtube.com/embed/7heRRNdXUxE?si=pWnXe4fSEjFeXKx7" 
    style="position: absolute; top:0; left:0; width:100%; height:100%;" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

- Time to generate : about 1 minute if I remember correctly.
- Where? on a free plan on Luma Labs's dream machine: [https://dream-machine.lumalabs.ai/](https://dream-machine.lumalabs.ai/)
- Evaluation: my paper boat is navigating the stream up! 🤦‍♂️ Also, no sound.
- Remarks: I made a second try where the paper boat sails [more naturally, downstream](https://github.com/user-attachments/assets/eace0c9c-52e7-4749-8fec-0e8dbfc7b8e6).



### WAN 2.5 (by Alibaba)

<iframe width="560" height="315" src="https://www.youtube.com/embed/8wRwwivEtwM?si=_tGM_KEFa95nvq3-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- Time to generate: at least 20 minutes . It took so long that I closed the tab and came back several hours later
- Where? on a free plan with [https://create.wan.video/generate](https://create.wan.video/generate)
- Evaluation: great fidelity to the prompt, level of details, great sound. The movement of the boat is not really coherent though (should not be so idle given the current)


### GROK (by xAI)

<video controls width="640">
  <source src="https://github.com/user-attachments/assets/e2f3ebda-a948-4c7e-9d37-d292a13916f9" type="video/mp4">
  Your browser does not support the video tag.
</video>

- Time to generate: less than a minute.
- Where? on a free plan with [https://grok.com/imagine](https://grok.com/imagine)
- Evaluation: no photo realistic, movement of the boat is not natural, resolution is low, sound is compressed


### SORA 2 (by OpenAI)

<video controls width="640">
  <source src="https://github.com/user-attachments/assets/07829bb3-10fe-41b2-875c-2f89fbc7b36e" type="video/mp4">
  Your browser does not support the video tag.
</video>

- Time to generate: between 5 and 10 minutes if I recall correctly
- Where? on a free plan with [https://vidgo.ai/](https://vidgo.ai/)
- Evaluation: photo realistic, camera angles feel elaborated, movement of the boat is so natural, resolution is high and even the blur feels as if an amateur would have shooted out of focus. Sound is realistic and detailed though not perfect.


### VEO 3 (by Google)

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%;">
  <iframe 
    src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
    style="position: absolute; top:0; left:0; width:100%; height:100%;" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

- Time to generate: a few minutes if I recall correctly
- Where? on a Google pro plan with [https://labs.google/fx/tools](https://labs.google/fx/tools)
- Evaluation: photo realistic, movement of the boat is so natural, resolution is high. Sound is realistic, really good.


# Conclusion

There is a tie between SORA 2 and VEO 3 in my honest opinion. WAN 2.5 is not far behind. GROK and RAY3 a

This quick comparison was made in relation to a list I maintain on [AI apps for visual creation: image, video, dubbing, 3D models and more](https://nocodefunctions.com/blog/list-of-ai-apps-for-visual-creation/).

---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
