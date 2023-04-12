---
layout: post
author: Angel
date: 2023-01-23
title: 2023 Lab Overview
description: A general overview of the 2 home labs and networks I have designed, currently manage, and maintain.
tags: ["homelab", "docker", "virtualization", "networking", "ups"] 
excerpt_separator: <!--more-->
## end of jekyll ##

showToc: true
TocOpen: false
hidemeta: false
comments: true
canonicalURL: "https://canonical.url/to/page"
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

**H1DC** and **H2DC** are projects I've been actively working on long before starting this site. Both labs are meant to be a testing platform for me in learning new technologies. I've been able to build them throughout the past 4 years, although they have been in constant flux, I believe these labs have definitely influenced my journey and development as an IT professional, and continue to influence my learning everyday.

## Homelab #1 "H1DC" Logical Layout
![diagram](https://d287cykochbccj.cloudfront.net/diagrams/h1dc-lab-diagram-2023-v2.svg)

### Physical Layout
![img](https://d287cykochbccj.cloudfront.net/pictures/h1dc/IMG_20210219_141819.webp)
![img](https://d287cykochbccj.cloudfront.net/pictures/h1dc/IMG_20201221_183413.webp)

The first home lab titled "H1DC" ("DC" short for Datacenter), was actually my first lab, it is at my family's residence, but I do manage it remotely if needed.

Although the lab has gone through many changes over the years, the diagram above illustrates the most recent version of how the network is laid out, and the services currently hosted there.

I've tried to keep things a bit logically simple, as compared to Homelab #2, as H1DC is no longer my primary lab, therefore I only host a few docker containers there.

### Devices
1 Mini Server
- Raspberry Pi 3b+

3 Network Devices
- Edgerouter X router (as the "CORE" router)
- TP-Link 5 port PoE switch (as my "CORE" switch)
- Ubiquiti AP-AC Lite Access Point

3 IP cameras
- Reolink

Power Supplies
- APC Back-UPS (BE425M) 425VA/255W

### Services
Local:
- SMB
- DNS
- FTP
- VPN (through [Pi-VPN](https://pivpn.io/), and [WireGuard on Edgerouter X](https://www.wireguard.com/install/#edgeos-module-tools))

Deployed using [Docker](https://www.docker.com/):
- [Portainer](https://www.portainer.io/)
- [Nginx Proxy Manager](https://nginxproxymanager.com/)
- [Jellyfin](https://jellyfin.org/)
- [Heimdall](https://heimdall.site/)
- [Bookstack](https://www.bookstackapp.com/)
- [Watchtower](https://containrrr.dev/watchtower/)
- [Uptime Kuma](https://github.com/louislam/uptime-kuma)
- [Pi-hole](https://pi-hole.net/)
- [UniFi controller](https://hub.docker.com/r/jacobalberty/unifi)
- [Speedtest-tracker](https://github.com/henrywhitaker3/Speedtest-Tracker)
- [Filebrowser](https://filebrowser.org/)

## Homelab #2 "H2DC" Logical Layout
![diagram](https://d287cykochbccj.cloudfront.net/diagrams/h2dc-lab-diagram-2023-v2.svg)

### Physical Layout
![img](https://d287cykochbccj.cloudfront.net/pictures/h2dc/IMG_20221107_164928.webp)

The second lab, titled "H2DC", is my lab at my current residence, it has been in development since 2020.

### Devices
2 Servers
- Synology DS720+ NAS (as my "STORAGE" node)
- Dell Optiplex Micro 3020M (as my "COMPUTE" node)

4 Network Devices
- Ubiquiti Edgerouter X (as the "CORE" router)
- UniFi Flex Mini (as the "CORE" switch)
- Netgear switch (as an "ACCESS" switch)
- Ubiquiti AP-AC Lite Access Point

Power Supplies
- 2 x APC Back-UPS Pro (BR1000MS), 1000VA/600W Sine Wave

### Services
Local:
- SMB
- DNS
- VPN (through WireGuard via [Tailscale](https://tailscale.com/))
- Active Directory (planned)

Deployed using [Docker](https://www.docker.com/):
- [Portainer](https://www.portainer.io/)
- [Nginx Proxy Manager](https://nginxproxymanager.com/)
- [Jellyfin](https://jellyfin.org/)
- [Tailscale](https://hub.docker.com/r/tailscale/tailscale)
- [Heimdall](https://heimdall.site/)
- [Watchtower](https://containrrr.dev/watchtower/)
- [Uptime Kuma](https://github.com/louislam/uptime-kuma)
- [Pi-hole](https://pi-hole.net/)
- [UniFi controller](https://hub.docker.com/r/jacobalberty/unifi)
- [Speedtest-tracker](https://github.com/henrywhitaker3/Speedtest-Tracker)
- [Filebrowser](https://filebrowser.org/)
- [Bookstack](https://www.bookstackapp.com/)
- [Mealie](https://hay-kot.github.io/mealie/)
- [Kiwix](https://www.kiwix.org/en/)
- [Navidrome](https://www.navidrome.org/)

& more...

The physical layout in my opinion is not very sophisticated, all the lab devices are actually housed in my TV stand in the living room as you can see below:

![img](https://d287cykochbccj.cloudfront.net/pictures/h2dc/IMG_20221105_143007.webp)
![img](https://d287cykochbccj.cloudfront.net/pictures/h2dc/IMG_20221105_143110.webp)

The devices are not entirely enclosed as there is an inlet in the back of the TV stand, which allows some airflow to and from the devices.

You can also see where my UPS is located:

![img](https://d287cykochbccj.cloudfront.net/pictures/h2dc/IMG_20221105_143035.webp)

I have 2 of these APC UPS devices, one in the living room and the other in my office/bedroom. 

## Power Utilization

Both UPS devices are 1000VA/600W.

The one in the living room can run for about 1hr 30min at 37-40W in the event of a power outage.

![img](https://d287cykochbccj.cloudfront.net/pictures/h2dc/IMG_20221105_143048.webp)

## In Summary

The home lab projects have been an invaluable learning experience.

I hope to continue my learning through the use of these labs, as they have definitely been a great learning experience and hobby.