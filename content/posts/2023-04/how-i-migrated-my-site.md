---
layout: post
author: Angel
date: 2023-04-04T13:03:23-05:00
title: "Migrating My Site From Jekyll to Hugo"
tags: ["hugo", "website", "blog", "static-site", "jekyll", "markdown", "web", "html", "javascript", "css"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
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

I've been utilizing [Jekyll](https://jekyllrb.com/) for the past few months to build my website. Although it does a pretty good job at doing so, I've been taking a look at [Hugo](https://gohugo.io/) and experimenting alongside it.

I was able to replicate my website on Hugo with a better looking theme and decided to take the leap. I went ahead and migrated my posts and basic items, making sure everything was nicely organized. And so far, it works pretty good!

I've went ahead and archived the old site, but still host it with GitHub Pages. If you are curious, it is still accessible [here](https://netsparse.github.io/).

If you are looking to migrate your Jekyll website to Hugo, fortunately, the migration process from Jekyll to Hugo is relatively straightforward. 

## Preparation

### Install Hugo

Download the appropriate package for your system.

- [Windows](https://gohugo.io/installation/windows/#prebuilt-binaries)
- [Mac OS](https://gohugo.io/installation/macos/#package-managers)
- [Linux](https://gohugo.io/installation/linux/#repository-packages)

### Create a New Hugo Site

Open your terminal or command prompt and type the following command:

```
hugo new site <your-site-name>
```

## Migration

### Copy the Content

The next step is to copy the content from your Jekyll site to your Hugo site. 

Navigate to the directory of your Jekyll site and copy the following directories:

```
_posts/
_layouts/
_includes/
```

These directories contain your blog posts, page layouts, and includes respectively. Once you have copied these directories, you can paste them into your Hugo site's directory.

### Convert the Front Matter

The next step is to convert the front matter of your Jekyll site to the Hugo format. 

The front matter is the metadata at the beginning of each file that specifies the title, author, date, and other information about the post or page. 

In Hugo, the front matter is specified in YAML format.

To convert the front matter, you need to open each file in your `_posts` directory and change the front matter to `YAML` format. 

For example, if your Jekyll front matter looks like this:

```yml
---
layout: post
title: My First Post
date: 2019-01-01 00:00:00 +0000
---
```

You need to convert the date or other information to the `YAML` format, it will look very similar, it could pretty much be copied over, you'll just need to modify `date:`.

```yml
---
layout: post
title: My First Post
date: 2019-01-01T00:00:00Z
---
```

### Configure the Site

The next step is to configure your Hugo site. 

Hugo uses a configuration file called `config.yml`, which contains settings such as the site title, description, and other options.

It will look something like this:

```yml
baseURL: "/"
languageCode: "en-us"
title: "My Hugo Site"
theme: "my-theme"
```

You can replace the values of these options with your own preferences, as well as define other settings for your site.

## Test the Site Locally

The final step is to test your Hugo site. You can do this by running the following command:

```
hugo serve
```

This will start a local server that you can access in your web browser at `http://localhost:1313` 

If everything has been set up correctly, you should see your newly created Hugo site running on the local server.

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

Migrating your Jekyll website to Hugo is a straightforward process that can be completed in a few steps. 

By following the steps outlined in this article, you can quickly and easily migrate your website to Hugo and take advantage of its speed, ease of use, and flexibility. 

Whether you are a seasoned web developer or a beginner, Hugo is a great choice for building fast and secure static websites.

## Learn More

Learn more about [migrating your site to Hugo](https://gohugo.io/tools/migrations/).