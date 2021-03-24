---
layout: page
title: Create a local network
parent: Networking
nav_order: 3
permalink: /networking/create-local-network
---

# Create a local network
{: .no_toc }

A great way to work with arrays of Raspberry Pi's, is to create a dedicated local network. Many types of setup are possible, but below I guide you through my suggested setup.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Planning your network
LAN stands for Local Area Network. It is basically like the internet, just a lot smaller, with a group of devices all connected to each other. A LAN can be connected to the internet or be completely separate from it.

The minimum you will need for a LAN is a (wireless) router and/or a network switch. A wireless network will be easier to set up physically but a wired (ethernet) network will provide a more stable and high-bandwidth connection.

If you have a lot of devices and plan to use ethernet connections you will need to get a network switch as a router only tends to have a maximum of four ethernet ports.

Determine if you want your devices to have internet access or not. The most simple network that does not need an internet connection only needs a network switch (not a router). For security one may also decide to have one host computer connected to the internet that in turn commands all Raspberry Pi units.

## Set up the local network
If you are working with a new network switch or router, the first thing to do is set it up. You will need to do this by connecting it to a computer via an ethernet cable.

A router will automatically handle assigning IP-addresses to each device on the network. In contrast, a network switch will allow connected devices to talk to each other but will not automatically assign IP addresses so works better when connected to a router or for setting up a static network.

I tend to prefer to have a static network as it can make it easier to find and connect to your devices as upon restarting the whole system Raspberry Pi's may change (and swap) their IP-address. The first thing to do is set it up on your host computer.

On a Mac, go to `System Preferences` > `Network` > `Built-in Ethernet` > `Advanced` where you can set up your network. On a windows PC, go to the `Network and Sharing Centre` in the control panel and select `Set up a new connection or network` and follow the steps. To set up a static IP-address on your Raspberry Pi, follow [these steps](http://).

If you want to create a wireless network you will have to have a device that broadcasts Wi-Fi, such as a Wi-Fi router. How to set it up depends on the device and brand, but generally you will connect to the router by typing in its ip-address in the browser. The IP-address tends to be printed on the bottom of the router.

Now login with the default username and password, which both tend to be `admin` by default, and go to the `wireless` section of your router to set up a new wireless network by choosing a new name (SSID) and password (WPA2) and make sure your network is enabled.

## Connect to the units individually
You will also have to decide how you will mainly communicate between your devices and set up your host computer accordingly (e.g. follow the guides for setting [SSH](http://) and [VNC](http://)).

Now connect each device via Wi-Fi or via ethernet cable and your devices should be able to speak to each other.

Now you are done, read about how to [share resources](http://) across the network to make full use of your new LAN.

For your local network it is key that all the Raspberry Pi's have a unique hostname and IP-address. If you want to set up a new system, I suggest to first [install the operating system](http://) on the SD-card for each of your units.

To connect to the Raspberry Pi it is perhaps easiest to use a keyboard, mouse, and screen. Another option is to to connect the host computer and Raspberry Pi with ethernet cable to the router, which are then both automatically given an IP-address. You can try and find the ip-address of the Raspberry Pi from your host machine by typing in `arp -a` or, if you know the current host name: `ping hostname.local`. A third option is to connect to it wirelessly immediately by editing the `wpa_supplicant` file, follow the [headless installation guide](http://).

After having decided your way of connecting, now we will change the hostname (and potentially IP address) for each of your devices.

By default, any Raspberry Pi thas “raspberrypi” as its hostname. Therefore when working with multiple units we need to make sure each has their own unique name. I tend to use a series name followed by a unique number (e.g. `jolpi020`, `jolpi100`).

It is easy to change the hostname. On the Desktop go to `Preferences` > `Raspberry Pi Configuration`. Enter a new name in the `host name` field, click `yes` when prompted, and your Raspberry Pi will restart. It is also possible to do this (similarly) using the `raspi-config` tool from the command line.

I tend to prefer to use static IP addresses for each Raspberry Pi such that I can always easily connect and link this to the hostname of the Raspberry Pi based on the subnet. For example, I would set up a local network with the subnet `192.168.2.X` and then have `jolpi020` with static ip address `192.168.2.020` and `jolpi100` with static ip address `192.168.2.100`. To learn how to set up a static IP address, follow [this guide](http://).

## Finishing the system
After following the above steps, turn off the Raspberry pi (`sudo halt -h now`), unplug the SD-card, label it if needed or connect to its dedicated Raspberry Pi, and continue with the next SD-card. Continue in this manner until all Raspberry Pi's have their own uniquely set-up SD-card.

When you have finished setting up your host machine and all the Raspberry Pi units, each of them should be able to communicate with all others. This is easiest done using the unique hostnames of the computers and can be tested with the `ping` command (e.g. `ping jolpi100.local`).

For a new system it is very handy to update and configure all your units at once using SSH. To not have to type in the commands separately for each unit, you can use a cluster SSH tool such as [csshX](https://github.com/brockgr/csshx).

[![csshx](/assets/images/csshx_windows.jpg?style=centerimgmed)](/assets/images/csshx_windows.jpg)
