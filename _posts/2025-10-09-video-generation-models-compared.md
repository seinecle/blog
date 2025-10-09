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

Prompt used for all models:

*Make a video of a paper boat descending and whirling in a natural torrent water stream from the Alps.*

*A few natural rocks are in the torrent, the torrent is small and the banks are made of herb, flowers, small bushes, in spring season.*

*No wild life.*

*Just the boat descending on the stream, with realistic physics for lights, water and boat movements: it whirls, slows down and goes faster depending on the current.*

⏩ all generations presented below are first try

⏩ **Except for LUMA, geenrated videos come with sound. So please swith the sound ON on the videos.** 

### RAY3 (by Luma Labs AI)

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=7heRRNdXUxE" target="_self">
    <img src="https://img.youtube.com/vi/7heRRNdXUxE/1.jpg" alt="RAY 3" style="max-width: 100%; width: 500px; height: auto;">
  </a>
</div>

- Time to generate : about 1 minute if I remember correctly.
- Where? on a free plan on Luma Labs's dream machine: [https://dream-machine.lumalabs.ai/](https://dream-machine.lumalabs.ai/)
- Evaluation: my paper boat is sailing upstream! 🤦‍♂️ Also, no sound.
- Remarks: I made a second try with a prompt asking the boat to sail [more naturally, downstream](https://github.com/user-attachments/assets/eace0c9c-52e7-4749-8fec-0e8dbfc7b8e6).



### WAN 2.5 (by Alibaba)

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=8wRwwivEtwM" target="_self">
    <img src="https://img.youtube.com/vi/8wRwwivEtwM/1.jpg" alt="WAN 2.5" style="max-width: 100%; width: 500px; height: auto;">
  </a>
</div>

- Time to generate: at least 20 minutes . It took so long that I closed the tab and came back several hours later
- Where? on a free plan with [https://create.wan.video/generate](https://create.wan.video/generate)
- Evaluation: great fidelity to the prompt, level of details, great sound. The movement of the boat is not really coherent though (should not be so idle given the current)


### GROK (by xAI)

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=EvwKxAJDj3w" target="_self">
    <img src="https://img.youtube.com/vi/EvwKxAJDj3w/1.jpg" alt="GROL" style="max-width: 100%; width: 500px; height: auto;">
  </a>
</div>

- Time to generate: 10 to 20 seconds.
- Where? on a free plan with [https://grok.com/imagine](https://grok.com/imagine)
- Evaluation: no photo realistic, movement of the boat is not natural, resolution is low, sound is compressed


### SORA 2 (by OpenAI)

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=67AW4DPvzHk" target="_self">
    <img src="https://img.youtube.com/vi/67AW4DPvzHk/1.jpg" alt="SORA 2" style="max-width: 100%; width: 500px; height: auto;">
  </a>
</div>

- Time to generate: between 5 and 10 minutes if I recall correctly
- Where? on a free plan with [https://vidgo.ai/](https://vidgo.ai/)
- Evaluation: photo realistic, camera angles feel elaborated, movement of the boat is so natural, resolution is high and even the blur feels as if an amateur would have shooted out of focus. Sound is realistic and detailed though not perfect.


### VEO 3 (by Google)

<div style="display: flex; justify-content: center;">
  <a href="https://www.youtube.com/watch?v=5BAc526iVdk" target="_self">
    <img src="https://img.youtube.com/vi/5BAc526iVdk/1.jpg" alt="VEO 3" style="max-width: 100%; width: 500px; height: auto;">
  </a>
</div>

- Time to generate: a few minutes if I recall correctly
- Where? on a Google pro plan with [https://labs.google/fx/tools](https://labs.google/fx/tools)
- Evaluation: photo realistic, movement of the boat is so natural, resolution is high. Sound is realistic, really good.


# Conclusion

### Rankings
- There is a tie between SORA 2 and VEO 3 in my honest opinion.
- WAN 2.5 is just behind, not because of the quality of the video but because the boat movements are not really natural.
- GROK and RAY3's quality is frankly below in terms of photorealism, level of details and physics.

### The case of GROK
- GROK's approach is distinctive: first, it generates *in seconds* literally *dozens* of images following the prompt, all with slight variations. The user is then invited to choose one of these frames as the preferred starting point to generate the video. The video is created at extreme speed (10 to 20 seconds or less in my experience). The video is produced in vertical mode and has a discreet but visible anime style, making it popular for shorts posted on social media. Also, it probably has lower standards in terms of controls on the type of content being produced. All these ingredients could foster its adoption despite not being the highest quality video generator.

### Other models, newer models?
This comparison was made in relation to a list I maintain on [AI apps for visual creation: image, video, dubbing, 3D models and more](https://nocodefunctions.com/blog/list-of-ai-apps-for-visual-creation/). This list is made to save you time by providing a frequently updated, one-stop landscape of AI apps for visual creation, grouped in meaningful categories.

---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
