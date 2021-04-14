---
layout: page
title: Overview Guide
nav_order: 3
permalink: /overview-guide
comments: true
---

# Raspberry Pi Overview Guide
{: .no_toc }

This overview guide is meant to help you get started and use your Raspberry Pi to its full potential in no time, from getting the right hardware together, to networking, filesharing, and connecting electronics. Follow the links to find the specific guides. For more background information and detail, read the preprint article [here](https://ecoevorxiv.org/qh9sz/)!
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Setting up and configuring
To start, let's first of all make sure you have the [right hardware](getting-started/choosing-raspberry-pi-hardware.html) together. Then let's [Install the operating system](getting-started/install-operating-system) on the micro-SD card or use a pre-installed [NOOBS card](https://github.com/raspberrypi/noobs/blob/master/README.md){:target="_blank"}. If you do not have a keyboard, mouse and screen follow a couple more steps to [create a headless setup](/getting-started/raspberry-pi-headless-setup).

Now plug-in the SD-card and connect the power to start your Raspberry Pi for the first time. Upon first boot let's  [configure your Raspberry Pi](/getting-started/raspberry-pi-configuration), such as to change the default password and hostname, enable various options, and make sure everything is up-to-date. For security measures you may also want to [change the default username](/networking/raspberry-pi-security). To get to know how to use the Raspberry Pi, the Raspberry Pi Foundation has a [great beginners tutorial](https://projects.raspberrypi.org/en/projects/raspberry-pi-using){:target="_blank"}.

## Connecting and networking
If you want to connect remotely, make sure your Raspberry Pi has a [wireless](https://www.raspberrypi.org/documentation/configuration/wireless/README.md){:target="_blank"} or [ethernet connection](/networking/create-direct-ethernet-connection) and read the guides on how to connect [via SSH](/networking/connecting-via-ssh) and [via VNC](/networking/connecting-via-VNC). You may want to [create a static ip address](/networking/create-static-ip-address) for better connectivity or even set up the Raspberry Pi as a [wireless access point](/networking/create-wireless-access-point) to make it possible to connect remotely even when no other network is available. When wanting to set up an array of Raspberry Pi computers, the [local network guide](/networking/create-local-network) may be of great help. Finally, you may want to [set up a firewall](/networking/raspberry-pi-security) when your Raspberry Pi(s) will be connected to the internet.

## Filesharing
There are a number of ways to share files with your Raspberry Pi. Read the [filesharing guide](/filesharing/filesharing-raspberry-pi) to start sharing files with Mac, Windows, and Linux operating systems. You may also want to learn how to [mount an external drive](/filesharing/mounting-external-drive) on the Raspberry Pi. To synchronise files between different computers and even over the internet, the `rsync` and `rclone` packages will be of great help, as detailed in the [file synchronisation guide](/filesharing/file-synchronisation-rsync-rclone).

## Programming
One can get the most out of the Raspberry Pi by writing custom scripts to help control and automate tasks. Although the Raspberry Pi OS provides an easy-to-use Desktop interface, one will likely do most with their Raspberry Pi using the terminal. I recommend to read the free ebook ["Conquer the Command Line"](https://magpi.raspberrypi.org/books/command-line-second-edition/pdf) and have a look at the guide [working with the command line](/programming/working-with-the-command-line). The Raspberry Pi OS also comes with a variety of programming and scripting languages such as Python, allowing for easy automated control of a wide range of sensors and devices. If you are planning on working with Python, it is a good idea to [create virtual environments](/programming/create-python-virtual-environment) and you may also need to [install OpenCV](/programming/install-opencv). It may also be helpful for your project to [run scripts at boot](/programming/run-script-on-boot) or [print statements at boot and shutdown](/programming/print-at-boot-and-shutdown), such as for on-time monitoring. Finally, learn how to use your Raspberry Pi to set up [email notifications](/programming/send-email-notifications), [sms notifications](/programming/send-sms-messages), and even [send messages to slack](/programming/send-slack-notifications).

## Image and video recording
If you are planning to use the Raspberry Pi for image and video recording, the Raspberry Pi Foundation has a good [beginner tutorial](https://projects.raspberrypi.org/en/projects/getting-started-with-picamera){:target="_blank"}. To help you select the right camera for your project and help you get started with controlled and automated image and video recording, follow the [image and video recording overview guide](/electronics/image-and-video-recording).

## Power solutions
When working with a non-mains powered Raspberry Pi, you may want to read the detailed section on power solutions and calculating power consumption in the accompanying paper. To help reduce your Raspberry Pi's power consumption, follow [this guide](/electronics/power-consumption-tricks). You may also want to follow my tutorial on [working with the PiJuice](/other/boot-automation-pijuice), a great [power management HAT](https://uk.pi-supply.com/collections/pijuice){:target="_blank"} for the Raspberry Pi.
