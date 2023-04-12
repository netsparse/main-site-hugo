---
layout: post
author: Angel
date: 2023-01-22 12:00:00
title: Starting This Site
description:
tags: ["blog", "website", "jekyll", "hugo", "homelab"] 
categories: [""]
excerpt_separator: <!--more-->
## end of jekyll ##

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

So it's been quite the journey figuring out the ins & outs of setting up a blog and writing posts in markdown.
So I figured I may as well write about it. <!--more--> 

Coming briefly from writing posts on [Wordpress](https://wordpress.com/), I wanted to take on the challenge in learning how to use [Git](https://git-scm.com/), treating the setup of this site as code, and jumping into a bit of [CI/CD](https://www.redhat.com/en/topics/devops/what-is-ci-cd) when it comes to deploying some of the changes to this site, as it is currently now hosted on [Netlify](https://www.netlify.com/).

### Previous Iteration of this Site

Previously, I was testing the waters with running Wordpress in a docker container on a AWS EC2 instance.

Amazon's [free-tier program](https://aws.amazon.com/free/) lets me run 1 instance for free, for 12-months, so long as I don't exceed any bandwidth, disk usage, and so forth.

I liked the idea and the setup was a bit straightforward for me, as I was already familiar with [docker](https://www.docker.com/) and running services in my homelab for quite some time now.

After setting up the site and launching it, I began seeing many attempts to login to the ```/wp-admin``` site.

I read that this is usually a common thing with internet facing sites, but was able to mitigate it by adding some WAF rules in Cloudflare.

All worked fine and the brute force attempts went away.

I let the host run for about 3 months, just to see how it dealt with any inbound bots and whatnot, and it actually did quite well.

### Slowdown

As I started posting, adding some testing material and so forth, I began to notice Wordpress slowing down _(differences in speed and also when loading any other webpages)_. This was minimal at first but began to incrementally get worse over time. 

Given that Wordpress was running as a lightweight docker container, I do think I was pushing the EC2 instance quite a bit once I started adding and changing the content, and also adding more containers.

I started experimenting with hosting the blog separately on the same machine as a separate docker container running [Ghost](https://ghost.org/). I believe this is when I started to see the slow down a lot more. 

I want to be honest and say that this is likely not best practice as I had no load-balancing or any redundancy whatsoever, although I do think it makes for an invaluable learning experience.

As I managed the new site and worked my way through learning AWS, I kind of wanted to push it a bit further to see what this little instance could handle, so I setup a separate container running [Matomo](https://matomo.org/) for analytics. I knew there was an add-on for Wordpress but wanted to try the full suite on its own.

And voila! It kept running!

After the fun and experimentation, and after learning and realizing that the tiny machine on the cloud could keep up _(with minimal traffic of course, since any substantial increase would otherwise trample it)_, I had to eventually move on to something more robust, simpler, and possibly cooler to manage. And that is where I ended up here.

### Static Site Generators
For those of you that may be new to SSGs (like me), they're essentially a way to automate the creation (or generation) of full static HTML webpages using templates, without needing to fully code the HTML from scratch. 

You can find a good explanation from Cloudflare [here](https://www.cloudflare.com/learning/performance/static-site-generator/).

I had several options I could choose from initially, I was mixed between going with some of the popular ones like [Hugo](https://gohugo.io/), [Jekyll](https://jekyllrb.com/), [11ty](https://www.11ty.dev/) and a few others. 

I have also wanted to learn Git for quite some time now, so I figured this would be a good opportunity to give it a shot.

Although I've managed to setup and experiment with both Hugo and Jekyll, I decided to stick with Jekyll for now since I had pretty much set up this site on Jekyll, plus I liked the minimal theme of this site.

Though I may plan on moving this blog into Hugo in the future!

**UPDATE: This blog has now been successfully transferred to Hugo as of April 2023.**

### What now?

The goal of this site is not only to document my learning, but also, to share it. 

Any content here is both for my reference, but also for you, any value you get out of it is both a win/win. 

Anyone out there that is also on their journey in IT, or any career in tech, I wish you the best, and good luck!

Thanks again for reading!