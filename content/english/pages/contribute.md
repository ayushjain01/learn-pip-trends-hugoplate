---
title: Contribute to learn-piptrends.com
description: Make your first open-source contribution with learn.piptrends.com. Contribute by submitting articles, adding related articles or answering FAQs.
---

Thank you for considering a contribution to learn-pip-trends! This can be a wonderful opportunity for your first open-source contribution. We are excited to accept well-crafted articles discussing the latest trends and updates in the world of Python.

Before submitting your contribution, we kindly ask you to read and follow our [contributing guidelines](./contributing) to ensure a smooth and efficient review process.


#### Prerequisites

- [Hugo Extended v0.115+](https://gohugo.io/installation/)
- [Node v18+](https://nodejs.org/en/download/)
- [Go v1.20+](https://go.dev/doc/install)

#### Project Setup

Use the following command to setup your project.

```bash
npm run project-setup
```

#### Install Dependencies

Install all the dependencies using the following command.

```bash
npm install
```

#### Development Command

Start the development server using the following command.

```bash
npm run dev
```

#### Add An Article
To contribute by submitting an article to learn-piptrends.com, please follow these steps:

- [Fork this repository](https://github.com/tankala/learn-pip-trends/fork){:target="_blank"}
- Create a new branch: `git checkout -b your-branch-name`
- Create an article `(.md)` and store it in the respective folder (```content\english\getting-started``` for getting started articles) following the article structure, including the following front matter:

```markdown
---
title: <Replace with your article title>
description: <Replace with your article description>
tags: <Replace with your article tags here>
categories: <Replace with your article categories here>
image: <Optional - Replace with image path>
date: <Replace with date of publication>
author: 
    title: <Replace with author name>
    twitter: <Replace with author twitter handle>
---
```
  Please visit [this link](./images) for detailed guidance on the various types of images used with an article and instructions on their creation. 
  
  Example front matter - 
  ```markdown
  ---
title: asyncio — Asynchronous I/O
description: A comprehensive guide on how to work with asyncio.
tags: [asyncio, async await]
categories: [Tutorial, Getting Started, Python Package, Asynchronous I/O]
image: "/images/getting-started/asyncio.png"
date: 2024-04-01
author:
    title: Ashok Tankala
    twitter: ashok_tankala
---
  ```
- Commit your changes: ```git commit -m "Brief description of your changes"```
- Push your branch: ```git push origin your-branch-name```
- Submit a [pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

**Please ensure that the front matter is included as specified above when contributing an article. You can refer to previous articles and their respective front matter for examples. Thank you for your contributions!**