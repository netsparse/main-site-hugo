---
layout: post
author: Angel
date: {{ .Date }}
title: "{{ replace .Name "-" " " | title }}"
tags: ["", ""]
categories: ["", ""]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
#canonicalURL: "https://canonical.url/to/page"
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: true
---


{{ range first 10 ( where .Site.RegularPages "Type" "cool" ) }}
* {{ .Title }}
{{ end }}