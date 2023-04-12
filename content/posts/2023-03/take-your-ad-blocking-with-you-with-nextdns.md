---
layout: post
author: Angel
date: 2023-03-07T22:48:26-05:00
title: "Take Your Ad Blocking With You On The Go With NextDNS"
tags: ["dns", "nextdns", "adblock", "ads", "networking"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
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

In our [previous post](/posts/2023-03/pihole-dns-with-docker), we setup a Pi-hole DNS server to block ads on our local network. 

Although the Pi-hole is awesome, unfortunately it only works on our local network, and thus we don't get the same benefits of ad blocking when we leaving the network.

Today, I'll show you how you can setup NextDNS on your mobile or laptop devices for whenever you need ad blocking on the go.

## Overview

[NextDNS](https://nextdns.io/) is a cloud-based, privacy-focused DNS service that allows users to block ads, trackers, and malware across all their devices. 

It was founded in May 2019 by two French founders, [Romain Cointepas](https://twitter.com/RomainCointepas) and [Olivier Poitrey](https://twitter.com/Olivier_Poitrey).

It works by intercepting DNS queries made by devices on the network and routing them to NextDNS servers (similar to Pi-hole), which then filter and block unwanted content based on various criteria such as malware, phishing, and adult content. 

It utilizes DNS over HTTPS (DoH), DNS over TLS (DoT), DNS over QUIC (DoQ) and [more](https://help.nextdns.io/t/x2hmvas/what-is-dns-over-tls-dot-dns-over-quic-doq-and-dns-over-https-doh-doh3), which also provide a level of security for your DNS queries.

You can define rules for filtering on a per device basis on the setup [dashboard](/posts/2023-03/take-your-ad-blocking-with-you-with-nextdns/#try-it-now).

NextDNS utilize their own custom DNS servers which you can find on under the `Endpoints` tab on the [Setup Page](/posts/2023-03/take-your-ad-blocking-with-you-with-nextdns/#try-it-now). 

You can learn more about the company [here](https://help.nextdns.io/t/y4hmv0n/who-is-behind-nextdns).

## Setup

### Try It Now

To get started with NextDNS, you can follow their [try it now link](https://my.nextdns.io/start) which you can use to get started immediately, although to take full advantage of the service and be able to customize it, you'll need to [create an account](https://my.nextdns.io/signup). 

**Note**: If you use the `try it now` link, the account will expire in 7 days and is only accessible from the browser you initially set it up from. You'll need to sign in in order to keep your customizations.

Once you sign up, you'll be taken to the dashboard, where you can manage your settings and configure your DNS preferences.

### Windows

To configure NextDNS on a Windows machine, follow these steps:

#### NextDNS App for Windows (Recommended)

1. Download the installer [here](https://nextdns.io/download/windows/stable).
2. After installing, right-click on NextDNS icon in the Systray, then open the Settings. Set `<your-nextdns-config-id>` as Configuration ID.
3. Right-click on NextDNS icon in the Systray, then click on Enable.

#### Manual Configuration

- Open the Start menu and type "Control Panel." Click on the Control Panel app to open it.
- Click on "Network and Internet" and then "Network and Sharing Center."
- Click on "Change adapter settings."
- Right-click on your network adapter and select "Properties."
- Click on "Internet Protocol Version 4 (TCP/IPv4)" and then click "Properties."
- Click on "Use the following DNS server addresses" and enter the IP address of the NextDNS server you want to use. You can find the latest IP addresses in the NextDNS dashboard under `Setup Guide`.
- Click "OK" to save your changes.


### macOS

#### Configuration Profile (Recommended)

macOS Big Sur or higher

Use the Apple Configuration Profile Generator available at [apple.nextdns.io](https://apple.nextdns.io).

#### App Store

{{< rawhtml >}}
 <!DOCTYPE html>
  <html>
  <div class="mt-4"><a href="https://apps.apple.com/app/nextdns/id1464122853"><img alt="" src="https://my.nextdns.io/static/media/mac-app-store.96c04ace686fb808e7039f7f50ceb2d3.svg" class="d-inline-block" style="height: 46px;"></a></div>
  </html> 
{{< /rawhtml >}}

1. Install our official app from the Mac App Store.
2. Click on `Preferences` in the app status bar menu and go to the `Configuration` tab.
3. Check `Use Custom Configuration` and enter `<your-nextdns-config-id>` as Configuration ID.
4. Enable NextDNS.

#### Manual Configuration

To configure NextDNS on a macOS machine, follow these steps:

- Click on the Apple menu and select "System Preferences."
- Click on "Network."
- Select your network connection and click "Advanced."
- Click on the "DNS" tab.
- Click on the "+" button to add a new DNS server.
- Enter the IP address of the NextDNS server you want to use. You can find the latest IP addresses in the NextDNS dashboard under `Setup Guide`.
- Click "OK" to save your changes.

### iOS / iPadOS

#### Configuration Profile (Recommended)

iOS 14 or higher

Use the Apple Configuration Profile Generator available at [apple.nextdns.io](https://apple.nextdns.io).

- Download the configuration profile.
- Open the Settings app.
- Tap `Profile Downloaded`.
- Tap Install in the upper-right corner, and follow the onscreen instructions.

#### App Store

{{< rawhtml >}}
 <!DOCTYPE html>
  <html>
  <div class="mt-4"><a href="https://apps.apple.com/app/nextdns/id1464122853"><img alt="" src="https://my.nextdns.io/static/media/app-store.0f8524437a4f5e73e02608131614f879.svg" class="d-inline-block" style="height: 46px;"></a></div>
  </html> 
{{< /rawhtml >}}

1. Install the official app from the App Store.
2. Open the app then go to Settings and toggle "Use Custom Configuration". Enter `<your-nextdns-id>` as Configuration ID.
3. Enable NextDNS.

### Android

#### Private DNS (Recommended)

Android 9 or higher

1. Go to Settings → Network & internet → Advanced → Private DNS.
2. Select the Private DNS provider hostname option.
3. Enter `<your-nextdns-config-id>.dns.nextdns.io` and hit Save.

#### App Store

{{< rawhtml >}}
 <!DOCTYPE html>
  <html>
  <div class="mt-4"><a href="https://apps.apple.com/app/nextdns/id1464122853"><img alt="" src="https://my.nextdns.io/static/media/play-store.b35e70ab7c2bfa851e0247dd4a874225.svg" class="d-inline-block" style="height: 46px;"></a></div>
  </html> 
{{< /rawhtml >}}

NextDNS App for Android
1. Install the official app from the Play Store.
2. In the NextDNS app, enter `<your-nextdns-config-id>` in Settings → Configuration ID, then connect.

### Linux

#### systemd-resolved (Recommended)

Use the following in `/etc/systemd/resolved.conf`:

**Note**: Make sure to replace `<nextdns-id-here>` with your Configuration ID. 

```ini
[Resolve]
DNS=45.90.28.0#<nextdns-id-here>.dns.nextdns.io
DNS=2a07:a8c0::#<nextdns-id-here>.dns.nextdns.io
DNS=45.90.30.0#<nextdns-id-here>.dns.nextdns.io
DNS=2a07:a8c1::#<nextdns-id-here>.dns.nextdns.io
DNSOverTLS=yes
```

#### NextDNS Command-Line Client

1. Run the following command: `sh -c "$(curl -sL https://nextdns.io/install)`
2. Follow the instructions.
Head over to our open-source repository at https://github.com/nextdns/nextdns/wiki for manual installation instructions.

### Identify Your Devices

Follow the instructions below to identify your devices in `Analytics` and `Logs`.

#### NS-over-TLS/QUIC
Prepend the name to the provided domain (the name should only contain a-z, A-Z, 0-9 and -). Use -- for spaces.
For "John Router", you would use `John--Router-<nextdns-config-id>.dns.nextdns.io` as your DNS-over-TLS endpoint.

#### DNS-over-HTTPS
Append the name to the provided URL (the name should be URL encoded).
For "John's Firefox", you would use `https://dns.nextdns.io/<nextdns-config-id>/John's%20Firefox` as your DNS-over-HTTPS endpoint.

#### Apps
Enable `Send Device Name` in the app settings.

## Note

Keep in mind that the above setup is only a guideline as of `03-2023`. 

The information may become outdated or changed. Always consult with the latest official documentation from NextDNS on their [site](https://my.nextdns.io), Setup Guide, and their [Help Center](https://help.nextdns.io/).

## Conclusion

NextDNS is a powerful DNS service that offers a range of privacy-focused features to protect your devices from ads, trackers, and malware. By following the steps above, you can easily configure NextDNS on your devices and start enjoying a safer, more secure online experience.

### Learn More
- [NextDNS Wiki (GitHub)](https://github.com/nextdns/nextdns/wiki)
- [NextDNS Help Center](https://help.nextdns.io/)
- [NextDNS Privacy Policy](https://nextdns.io/privacy)
- [Source Code](https://github.com/nextdns)
- [NextDNS and Pi-hole](https://help.nextdns.io/t/q6hmvay/what-is-the-advantage-of-using-nextdns-over-pi-hole)

### Tools
- [Ping Check](https://ping.nextdns.io/)
- [Routing Check](https://router.nextdns.io/)
- [DNS Leak Test](https://dnsleaktest.com/)
- [RIPEstat BGP Lookup NextDNS](https://stat.ripe.net/app/launchpad/S1_34939_C13C31C4C34C9C22C28C20C6C7C26C29C30C14C17C2C21C33C16C10)