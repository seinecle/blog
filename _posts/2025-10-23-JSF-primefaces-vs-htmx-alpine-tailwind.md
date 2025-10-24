---
layout: post
title: "Comparing JSF + PrimeFaces 🆚 HTMX + Alpine"
permalink: /jsf-primefaces-vs-htmx-alpine-tailwind/
published: true
date_readable: October 23, 2025
last_modified_at_readable: October 23, 2025
categories: [frameworks, web development, java, JSF, primefaces, htmx, alpine, tailwind]
---

### Why a Java stack for the front-end?

I've been developing [nocodefunctions.com](https://nocodefunctions.com) since 2021. My skills (and, frankly, my taste) for the key technologies in front-end development (CSS and JS) are very limited:

![css-is-awesome](https://github.com/user-attachments/assets/5903b606-3238-4c91-9fad-f966476d269c)

For this reason, and because I enjoy developing in Java, my entire stack is Java: [JSF](https://github.com/jakartaee/faces) + [Primefaces](https://showcase.primefaces.org) for the front-end, integrated with the backend through [JakartaEE](https://jakarta.ee/learn/starter-guides/) that manages both.

[This stack served me very well](https://nocodefunctions.com/blog/java-frontend-web-app/): it did the job. The web app displays complex data tables, it includes an image cropper function so that a user can select a region on specific pdf pages ... pretty advanced stuff for somebody who doesn't want to touch Javascript even with a stick. It is even [internationalized on 104 languages](https://nocodefunctions.com/blog/translated-web-app-in-107-languages-i18n/), and is fully responsive.

As a solo developer with limited spare time for this side project, I managed all this while still developing and expanding the app’s core features. It has handled [hundreds or thousands of requests per month](https://public.nocodefunctions.com/).


### Why reconsider my Java stack?

Today, I’m exploring whether I could achieve a better, more personal design for the website.

I tried first customizing the css of the pages with [Tailwind](https://tailwindcss.com/) but quickly realized it conflicts with the css theme applied by default by Primefaces. There are ways to have Tailwind and Primefaces theming to work hand in hand but they involve to setup a dedicated scaffolding to manage it, which adds cognitive load and will be a burdeon to maintain in the long term.

I also use Gemini or ChatGPT's canvases extensively to prototype this redesign. However these tools can't render the XHTML files central to my current tech stack, while they render HTML + CSS + JS effortlessly.

So I came to wonder:

> what if I made a different choice for my frontend stack, for a better experience as a developer? What would I loose, what would I gain?

It's easy to assume that ditching JSF and PrimeFaces would simplify things, but what exactly would I lose? And what new difficulties would appear?

Here is a comparison between my current stack (JSF + Primefaces) and the alternative I am considering (HTMX + Alpine.js + Tailwind)

> **nota bene** : I am well aware that JSF and Primefaces can work with Tailwind with no fuss, so one might find it unfair to pit JSF + Primefaces against a solution with Tailwind. But as I said above, making Tailwind work in coherence with Primefaces needs some extra tooling which I personally find too heavy, compared to "just add Tailwind" in the HTMX + Alpine solution.

### Comparison: from the point of view of JSF + Primefaces strengths


|   | **JSF + PrimeFaces (strengths)**                                                            | **HTMX + Alpine.js (cons)**                                                       |
| - | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| 1 | No need to touch css or js, or very minimally                                               | it is all about adding css classes and js (but a lot of complexity remains hidden)|
| 2 | Complex components provided out of the box (data tables, image croppers, etc.)              | Lacks complex components — requires specific JS libraries and custom backend code |
| 3 | Strong IDE integration: refactoring a backend method refactors the front end as well        | Logic is separated — no automatic synchronization between front and back          |
| 4 | Same programming language and framework on both sides (e.g., file upload easily integrated) | Different languages/frameworks: file upload must be fully defined on both ends    |
| 5 | User session management provided out of the box                                             | No session mechanism — must be implemented manually (cookies, tokens, etc.)       |
| 6 | Security and accessibility built into the framework                                         | No built-in security or accessibility mechanisms                                  |
| 7 | Easy internationalization (i18n) support                                                    | No i18n provided by default                                                       |
| 8 | Coherent default styling with theme support                                                 | Styling must be designed entirely from scratch                                    |
| 9 | Proven, long-term ecosystem (20+ years, likely stable for 20 more)                          | Younger frameworks — shorter historical lifespan and uncertain long-term support  |

---

### Now from the point of view of HTMX + Alpine + Tailwind strengths...


| # | **HTMX + Alpine.js + Tailwind (strengths)**                                                                | **JSF + PrimeFaces (cons)**                                                                                             |
| - | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 1 | Static HTML files (not server-generated): easy to host, patch, and reload; ensures fast loading | XHTML pages are server-generated, requiring full app redeployment (including backend) for any small UI or CSS/JS change |
| 2 | Simple Nginx setup: one route for static assets, one for each API endpoint                      | Complex Nginx configuration required for JSF applications                                                               |
| 3 | Transparent handling of Server-Sent Events (SSE), including through Nginx                       | SSE handling is a “black box,” difficult to debug behind a proxy                                                        |
| 4 | Manual styling = total creative freedom and perfect consistency between pages and components    | Default component styling is hard to override and align with custom page design                                         |
| 5 | Excellent compatibility with LLMs (HTML/CSS/JS easily generated and previewed)                  | LLMs cannot preview XHTML pages — breaks interactive design workflows                                                   |
| 6 | Strong and active open-source community (HTMX, Alpine, Tailwind)                                | JSF and PrimeFaces communities are small and aging                                                                      |
| 7 | Close to native HTML: lightweight, transparent, and easily replaceable if needed                | Heavy abstraction over HTML, with complex internal JS/CSS layers that obscure rendering and server interaction          |

## 🔀 Decision after comparison

What made me tilt towards HTMX + Alpine + Tailwind is that LLMs can handle it for me, removing my biggest obstacle ("I hate css and js, they are too brittle").

Don't jump and shame me ("ohh he is fine with vibe coding and AI slope!"). By sticking to very simple frameworks like HTMX, Tailwind and Alpine,  I remain very close to the native HTML of the pages. This means the generated HTML, CSS classes and JS are not a black box I have to trust blindly. I'll be able to debug, modify, and remove them if necessary, in a way that is much more transparent than I was in my current situation with JSF.

And the benefits of the switch are mouth-watering: I'll finally be able to design pages in a more personal and distinctive way than the design I was stuck with until now.

Don't get me wrong: I am grateful to JSF and Primefaces for providing the tools that allowed me to create a functional and (to my standards) successful web app without touching CSS and JS, which I dare anyone trying without these Java techs. But LLMs change the game. They reduce the need for such heavy frameworks. Coding closer to native HTML, CSS and JS is now a viable, even enjoyable option.

This new stack does come with trade-offs: some features will be dropped because they're too time-consuming to rebuild. For instance, the complex UI with data tables and the "PDF region selector" using an image cropper. That is a trade-off I'm ready to make.

## 🎯 Results: let's wait for the refactoring

I am currently working at this refactoring. Visit [nocodefunctions.com](htpps://nocodefunctions.com) to see how it looks with the current Java stack, and come back in a few months, realistically, to see how it has evolved.

---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
