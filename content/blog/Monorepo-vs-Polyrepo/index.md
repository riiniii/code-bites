---
title: "Monorepo vs Polyrepo"
date: "2021-10-30T07:26:03.284Z"
description: "A short blurb on monorepo vs polyrepo."
categories: [repository, svc]
comments: true
---

_For more detailed differences and explanations, please go to the link(s) provided below! This was written to decide what to use for a project I was taking on, but I quickly decided that monorepo is sufficient for my needs and thus this articles is not quite fleshed out as others available on the web!_

We're starting a new project and wondering how we should structure our repository? I've seen code bases be contained in a single repository and in multiple. This sounded somewhat like monorepo and polyrepo. These two phrases mean exactly what they say, but lets go through two examples to make it very clear.

When we have a monorepo, it can contain our code for our web application, our mobile application, our server/backend code, and maybe any microservices too all in **one repository**.

When we have a polyrepo, our code for our web application, mobile application, server/backend code, etc., would all be located in separate repositories.

From reading the article above, it looks like for smaller sized projects where you are creating for only one product, one repository is sufficient for your code.

If you have multiple products, or as your code base scales to above certain sizes (ex. 10-100 developers writing code full time, 1k-10k versioned dependencies), then it'd be good to consider a polyrepo.

I would write more, but there are too many great articles out there so I'll leave that to them.

For my case, I've concluded that at least for the next two plus years our project will be sufficiently contained and workable in a monorepo.

Kind, amazing, and great resources used to write this up.

- **[monorepo-vs-polyrepo](https://github.com/joelparkerhenderson/monorepo-vs-polyrepo)**
- [monorepo-vs polyrepo 2](https://earthly.dev/blog/monorepo-vs-polyrepo/)
