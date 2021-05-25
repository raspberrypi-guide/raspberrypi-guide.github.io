---
layout: page
title: Direct ethernet connection
parent: Networking
nav_order: 6
permalink: /networking/create-direct-ethernet-connection
comments: true
---

# Connect directly to your Raspberry Pi by network cable
{: .no_toc }

In some cases, one may want a more direct connection with the Raspberry Pi, such as when neither a wireless nor a wired network are available. Below I describe how to configure a direct computer-to-computer connection using an ethernet cable.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Direct connection with a Mac
Connect your Mac and Raspberry Pi with an ethernet cable and power up your Raspberry Pi. Now on your Mac, go to `System Preferences` > `Sharing`, click on `Internet Sharing` and choose the Wi-Fi interface to share from, and below check the box next to your wired network interface, e.g. `USB 10/100/1000 LAN`. Now check the `On` checkbox next to Internet Sharing to enable it.

[![Internet sharing](/assets/images/internet-sharing-mac.jpg?style=centerimgmed)](/assets/images/internet-sharing-mac.jpg)

Now open a terminal window and type in `ifconfig` to show the list of all interfaces. At the bottom there should be an interface called `bridge100`. The IP address that the Raspberry Pi will get is the the IP address shown here+1. For example if it shows `192.168.2.1` then your Raspberry Pi will have `192.168.2.2`.

In the terminal window, now enter `ssh pi@[ip-address]` to connect to the Raspberry Pi. If using a stock installation the default password will be `raspberry`.

That's it! Now make sure to add the wireless network or make any other required changes to be able to connect without the ethernet cable again.

## Direct connection with a Windows PC
Coming soon
{: .label .label-yellow }
