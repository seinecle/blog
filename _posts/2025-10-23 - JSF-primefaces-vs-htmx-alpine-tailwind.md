---
layout: post
title: "Comparison: JSF + PrimeFaces vs HTMX + Alpine.js"
permalink: /jsf-primefaces-vs-htmx-alpine-tailwind/
published: false
date_readable: October 23, 2025
last_modified_at_readable: October 23, 2025
categories: [frameworks, web development, java, JSF, primefaces, htmx, alpine, tailwind]
---

## 🧩 Comparison: JSF + PrimeFaces vs HTMX + Alpine.js


I develop nocodefunctions.com for 4 years now. Being a Java developer with limited skills and taste for front-end development, I rely on JSF + Primefaces for the front-end, integrated with the backend through JakartaEE.

Trying to redesign the pages with tailwind, I realized that there is some work and tooling needed to make tailwind styles coherent with Primefaces styles.

I also realized that I relied a lot on Gemini or ChatGPT's canvases to create, preview, interate on the new styles I designed: and that is hard to do with xhtml pages, while it is just natural with html documents, even loaded with external css and js libs.

So I considered removing Primefaces..

|   | **JSF + PrimeFaces (strengths)**                                                            | **HTMX + Alpine.js (cons)**                                                       |
| - | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| 1 | Complex components out of the box (data tables, image croppers, etc.)                       | Lacks complex components — requires specific JS libraries and custom backend code |
| 2 | Strong IDE integration: refactoring a backend method refactors the front end as well        | Logic is separated — no automatic synchronization between front and back          |
| 3 | Same programming language and framework on both sides (e.g., file upload easily integrated) | Different languages/frameworks: file upload must be fully defined on both ends    |
| 4 | User session management provided out of the box                                             | No session mechanism — must be implemented manually (cookies, tokens, etc.)       |
| 5 | Security and accessibility built into the framework                                         | No built-in security or accessibility mechanisms                                  |
| 6 | Easy internationalization (i18n) support                                                    | No i18n provided by default                                                       |
| 7 | Coherent default styling with theme support                                                 | Styling must be designed entirely from scratch                                    |
| 8 | Proven, long-term ecosystem (20+ years, likely stable for 20 more)                          | Younger frameworks — shorter historical lifespan and uncertain long-term support  |

---

| # | **HTMX + Alpine.js (strengths)**                                                                | **JSF + PrimeFaces (cons)**                                                                                             |
| - | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 1 | Static HTML files (not server-generated): easy to host, patch, and reload; ensures fast loading | XHTML pages are server-generated, requiring full app redeployment (including backend) for any small UI or CSS/JS change |
| 2 | Simple Nginx setup: one route for static assets, one for each API endpoint                      | Complex Nginx configuration required for JSF applications                                                               |
| 3 | Transparent handling of Server-Sent Events (SSE), including through Nginx                       | SSE handling is a “black box,” difficult to debug behind a proxy                                                        |
| 4 | Manual styling = total creative freedom and perfect consistency between pages and components    | Default component styling is hard to override and align with custom page design                                         |
| 5 | Excellent compatibility with LLMs (HTML/CSS/JS easily generated and previewed)                  | LLMs cannot preview XHTML pages — breaks interactive design workflows                                                   |
| 6 | Strong and active open-source community (HTMX, Alpine, Tailwind)                                | JSF and PrimeFaces communities are small and aging                                                                      |
| 7 | Close to native HTML: lightweight, transparent, and easily replaceable if needed                | Heavy abstraction over HTML, with complex internal JS/CSS layers that obscure rendering and server interaction          |

---
# About Me

I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
