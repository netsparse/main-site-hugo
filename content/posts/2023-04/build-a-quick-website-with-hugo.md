---
layout: post
author: Angel
date: 2023-04-04T21:25:31-05:00
title: "Build a Quick Website With Hugo"
tags: ["hugo", "website", "blog", "static-site", "markdown", "web", "html", "javascript", "css"]
showToc: true
TocOpen: false
hidemeta: false
comments: true
#canonicalURL: "https://canonical.url/to/page"
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

## Overview

[Hugo](https://gohugo.io/) is a popular static site generator written in Go. It allows you to create and manage static websites quickly and easily. 

In this guide, we will cover the basics of getting started with Hugo.

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy 0RKpf3rK57I >}}

## Get Started

### Installation

Download the appropriate package for your system.

- [Windows](https://gohugo.io/installation/windows/#prebuilt-binaries)
- [Mac OS](https://gohugo.io/installation/macos/#package-managers)
- [Linux](https://gohugo.io/installation/linux/#repository-packages)

## Content Management

### Creating a New Site

```bash
hugo new site <your-site-name>
```

This will create a new Hugo site in a directory named mysite.

### Creating a New Page

```bash
hugo new page/about.md
```

This will create a new Markdown file named `about.md` in the `content/page` directory.

### Adding Content

To add content to your site, open the Markdown file you created in the previous step and add your content using Markdown syntax.

For example, to add a heading, use the `#` character followed by your heading text:

```md
# About Us

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

### Building Your Site

To build your site, navigate to the root directory of your site and run the following command:

```bash
hugo serve
```

This will generate your site in a directory named `public`

### Viewing Your Site

To view your site, open a web browser and navigate to `http://localhost:1313`

### Theming

If you wish to make your site look awesome or more polished, make sure to check out the Hugo community themes at https://themes.gohugo.io/.

## Deployment & Hosting

Once you have tested your site, the final step is to deploy it. 

There are several options for deploying your Hugo site, including [GitHub Pages](https://pages.github.com/), [Netlify](https://www.netlify.com/), [Cloudflare Pages](https://pages.cloudflare.com/), [Vercel](https://vercel.com/) & more.

We'll set it up on [Netlify](https://www.netlify.com/) as an example, for that we'll need to:

- Create a new repository on GitHub with the same name as your Hugo site.
- Push your Hugo site to the new repository using `Git`.
- Setup a Netlify account and connect it to the repository in the settings.
- Choose the branch and folder where your site is located.
- Wait for the site to be built and deployed.

### Quick Start

Check out Netlify's [quick start](https://app.netlify.com/start/deploy?repository=https://github.com/netlify/netlify-feature-tour) page to connect your GitHub repo to Netlify and launch your site in under a minute.

Once your site is deployed, you can access it using the Netlify-generated URL, which will look something like: `https://<random-id>.netlify.app`.

### Custom Domains

If you own a custom domain, configure your DNS records with your Registrar, and check out [how to assign a domain to your site](https://docs.netlify.com/domains-https/custom-domains/#assign-a-domain-to-a-site)

## Conclusion

In this guide, we have covered the basics of getting started with Hugo. 

By using Hugo, you can create and manage static websites quickly and easily, it also provides many features and options for customizing your site, making it a powerful tool for building websites.

## Learn More

Check out the official [Hugo documentation](https://gohugo.io/documentation/).