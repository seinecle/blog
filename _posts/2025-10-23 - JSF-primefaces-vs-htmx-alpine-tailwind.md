---
layout: post
title: "Comparison: JSF + PrimeFaces vs HTMX + Alpine.js"
permalink: /jsf-primefaces-vs-htmx-alpine-tailwind/
published: false
date_readable: October 23, 2025
last_modified_at_readable: October 23, 2025
categories: [frameworks, web development, java, JSF, primefaces, htmx, alpine, tailwind]
---

## Comparison: JSF + PrimeFaces 🆚 HTMX + Alpine.js

I develop [nocodefunctions.com](https://nocodefunctions.com) since 2021. Being a Java developer with limited skills and taste for the key technologies in front-end development (css and js), I rely on JSF + Primefaces for the front-end, integrated with the backend through JakartaEE that manages both.

This stack served me well: as a solo developer with limited spare time for this side project, I could focus on developing the core features of the app. I have been able to serve [hundreds or thousands of requests per month](https://public.nocodefunctions.com/).

Today I am exploring if or how I could achieve a better, more personal design of the web site.

I tried first to custimoze the css with tailwind but I realized that it conflicts with the css applied by default Primefaces. There are ways out but they involve to create some devops scaffolding, which will be a burdeon to maintain in the long term.

I also use Gemini or ChatGPT's canvases a lot to imagine this redesign. These canvases can't render the xhtml files that are central to my current tech stack, while they render html + css + js effortlessly.

So I came to wonder:

> what if I made a different choice for my frontend stack, for a better experience as a front end developer? What would I loose, what would I gain?

Saying that ditching JSF and Primefaces would remove difficulties is obvious, but what would I loose? What additional difficulties does it introduce?

Here is a comparison between my current stack (JSF + Primefaces) and the alternative I am considering (htmx + alpine.js + tailwind)

> nota bene : I am well aware that JSF and Primefaces can work with tailwind with no fuss, so one might find it unfair to pit JSF + Primefaces against a solution with tailwind. But as I said above, making tailwind work in coherence with Primefaces need some extra tooling which I personally find too heavy, compared to "just add tailwind" in the htmx + alpine solution.

### from the point of view of JSF + Primefaces strengths...


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

### from the point of view of HTMX + Alpine + Tailwind strengths...


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

What made me tilt towards HTMX + Alpine + Tailwind is that LLMs will handle it for me, so obstacle number one ("I hate css and js, they are too brittle") just disappears. Don't jump and shame me ("ohh he is ok with vibe coding and AI slope!"). Keeping to very simple frameworks like HTMX, tailwind and alpine ensures that I remain very close to the native html of the pages. This means the generated html, CSS classes and js will not be a black box that I'll have to trust blindly. I'll be able to debug it, modify it and remove it if necessary, in a way that is much more transparent than I was in my current situation with JSF.

And the benefits of the switch are mouth watering: I'll finally be able to design pages in a more personal way than the design I was stuck with until now. Don't get me wrong: I thank and praise JSF and Primefaces for having provided these techs that allowed me to create a workable and successful (to my standards) web app without touching CSS and JS, which I dare anyone trying without these Java techs. But LLMs provide new opportunities and I believe they diminish the need for frameworks like these. Coding relatively closer to native html, css and js is a viable option today.



---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
