---
layout: page
title: Installing the operating system
parent: Getting started
nav_order: 2
---

# Installing the operating system
{: .no_toc }

The Raspberry Pi does not come as a pre-installed computer, but luckily installing an operating system for your Raspberry Pi has become easier then ever before.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Using NOOBS
It is generally recommended that beginners buy the Raspberry Pi with a micro SD-card that has [NOOBS](https://www.raspberrypi.org/documentation/installation/noobs.md) (New Out Of Box Software) installed. This enables you to simply plug-in the SD card into your Raspberry Pi and follow the installation steps to install a wide range of operating systems.

Rather than use NOOBS, which adds another installation step, I tend to recommend to install the operating system manually. This is almost as easy as using NOOBS but gives more flexibility, such as to work with already downloaded image files and enabling a [headless setup](http://).

## Using the Raspberry Pi Imager
On another computer,  download and install the Raspberry Pi installer ([raspberrypi.org/downloads/](raspberrypi.org/downloads/)). Open the program and  select the desired operating system in the list. I recommend to choose the latest version of Raspberry Pi OS (previously called Raspbian) with Desktop.

Now plug in your SD card into the computer, select it using the *Choose storage* option, and click *write*. In a couple minutes your SD card with a freshly installed operating system should be finished!

[![Raspberry Pi imager](/assets/images/raspberry-pi-imager.png?style=centerimgmed)](/assets/images/raspberry-pi-imager.png)

After the SD card is written, plug it in your Raspberry Pi and start it up by connecting power. Upon first boot in the Raspberry Pi OS Desktop environment, you will be guided through a short series of steps to help configure and update your system.

## Using Etcher
[Etcher](https://etcher.io) is another way to install the operating system that tends to be slightly faster than the Raspberry Pi Imager tool. You can download it from [https://etcher.io](https://etcher.io), making sure to select the right version compatible with your operating system. Now set up the Etcher software and accept the license agreement and install.

[![Balena Etcher](/assets/images/balena-etcher.png?style=centerimgmed)](/assets/images/balena-etcher.png)

To install you will need to have an image file of the operating system on your computer. You can for example download the latest version of the Raspberry Pi OS [here](https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit). Now Open Etcher, select the downloaded image file, select the SD card, and click *flash*. That's it.


## Connecting
Whatever approach you used above, to be able to connect to your Raspberry Pi you will need a screen, keyboard, and mouse. However, with a couple of simple additional steps it is also possible to immediately run your freshly installed SD card without these peripherals. See the [Raspberry Pi headless setup guide](http://).
