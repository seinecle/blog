---
layout: post
title: Light Stripe Flow
permalink: /light-stripe-flow/
published: true
date_readable:               March 10, 2025
last_modified_at_readable:   March 10, 2025
categories: [nocodefunctions, development, stripe]
---
Today, I'm thrilled to share how I recently updated my web app, [nocodefunctions.com](https://nocodefunctions.com), by adding a secure and lightweight approach to user management and payments. Inspired by Pieter Levels ([@levelsio](https://x.com/levelsio)) and closely following the customer management approach he used for [photoai.com](https://photoai.com), my goal was to minimize complexity and maximize security, by offloading nearly all customer management tasks directly to Stripe. This change marks a significant improvement in both the user experience and backend maintainability. Here's an in-depth look at how and why I implemented this approach:

# Why Simplify?

As an indie Java developer developping at nights and weekends, managing complex user authentication, account security, and billing flows would have been simply overwhelming. By leveraging Stripe’s capabilities, I completely eliminated the need to handle sensitive user credentials like passwords or payment details on my servers. Stripe securely manages everything from subscriptions and payments to essential customer metadata.

# The Simplified Flow

Here's a step-by-step breakdown of how the new simplified approach works:

1. **Email sent to the user**

   - Users sign up or log in simply by entering their email address on the [front page of the app](https://nocodefunctions.com/#input-email-container-anchor).
   - This sends them a link to a web page where the 2 paying plans are described. Why this detour, since these plans are already visible [on the front page of the app](https://nocodefunctions.com/#input-email-container-anchor)? The trick is that this allows to populate the links towards the corresponding Stripe checkouts with the email of the person navigating to the page. Simple stuff but that is the essential first step for the Stripe checkout.

2. **Checkout with Stripe**

   - Users have the option to select one of two premium plans: "Pro" or "Patron."
   - Selecting a plan redirects users to Stripe's secure and user-friendly hosted checkout page, completely removing any billing complexity from my application.
   - A customer is created on Stripe with two values stored on it: a hash (long String value), and a credit amount.

3. **Post-Payment Process**

   - Upon successful payment, Stripe sends a webhook notification to my backend, with the hash value of the customer. From there on, the hash value or the email of the user will be used to identify / retrieve their info from Stripe.
   - Stripe redirects the user to the app.
  
4. **Customer experience post-purchase**
   - The redirection to the app triggers the storing of the hash for this customer as a cookie for the app.
   - From now on, pages of the app use this cookie at load time to retrieve the customer information : check that the user has enough credits to access features, display customer-specific info, etc.
   - An item is added to the menu with a link to the billing portal where the user can manage its subscription. 

# Technical Highlights

- **Passwordless Authentication**: Completely eliminates traditional authentication mechanisms, thereby significantly reducing security vulnerabilities associated with password management.
- **Stripe-hosted Billing Portal**: Users independently manage their subscriptions, payment methods, billing history, and refunds through Stripe's comprehensive billing interface, drastically reducing backend responsibilities.
- **Secure Metadata Handling**: Critical user information like unique hashes, subscription tiers, and usage credits are securely managed by Stripe, ensuring reliable data protection and integrity.

# Enhanced Schematic Overview:

```
User → nocodefunctions.com
     ↓ enters email
Email → User (secure login link)
     ↓ clicks link to login
User → Stripe Hosted Checkout (Plan selection & secure payment)
     ↓ successful payment
Stripe → Webhook notification → nocodefunctions.com
     ↓                                ↘ User metadata securely stored: a credit amount, basically
User gains immediate access via unique hash
```

### Benefits

This approach significantly improves security by eliminating the storage of passwords and any sensitive financial information, thereby greatly reducing potential security breaches. Additionally, it drastically reduces application complexity, resulting in fewer bugs and easier ongoing maintenance. I have basically 3 classes:

- [one class in the front end listing operations with Stripe](https://github.com/seinecle/nocodefunctions-web-app/blob/main/src/main/java/net/clementlevallois/nocodeapp/web/front/stripe/StripeBean.java). These ops are not made by the front end but delegated to a separate backend module with http requests.
- a class in a backend module that receives these requests and *sends* calls to Stripe : very basic stuff ("retrieve customer email by hash", "retrieve customer hash by email", "get remaining credits", etc.)
- webhooks in a second class of this backend: endpoints that *receive* Stripe push notifications, again very simple stuff: notification by Stripe of customer creation, which triggers the creation of a hash and a credit amount for this customer... that's it. 

[TODO : adding a webhook that resets credits to the max at each start of the monthly billing cycle.]

Users benefit from greater empowerment (and I benefit from peace of mind) because they gain full control over billing, subscriptions, and account management through Stripe’s billing portal.

### Supporting Open Source

This freemium approach not only sustains the development of nocodefunctions but also supports broader open-source initiatives, such as my own contributions and tools like [Gephi](https://gephi.org/). Users can confidently use core functionalities for free while choosing premium plans to support continuous improvement and sustainability.

I warmly invite you to try this new streamlined user management experience on [nocodefunctions.com](https://nocodefunctions.com). Your feedback is highly appreciated—let me know your thoughts!

# About me
I am academic and independent web app developer. I build [nocode functions](https://nocodefunctions.com) 🔎, a free click and point web app to explore texts and networks. It is [fully open source](https://github.com/seinecle/nocodefunctions). Try it and give some feedback, I would appreciate it!

* my email: [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* or on Bluesky: [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* you can also read [the other articles of this blog](https://nocodefunctions.com/blog) 👓, where I write about the process of developing my apps.
