---
layout: page
title: FAQ
nav_order: 10
permalink: /FAQ
comments: true
---

# Frequently Asked Questions
{: .no_toc }

Here you will find an overview of Frequently Asked Questions with my concise answers. These are meant to complete the detailed [FAQ](https://www.raspberrypi.org/documentation/faqs/){:target="_blank"} on the Raspberry Pi Foundation website. If you have any further questions, please leave a comment below!
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## How many models are there?
There have been several generations of Raspberry Pi's, which can be broadly categorised in the Raspberry Pi A, the more powerful Raspberry Pi B, and the simpler and much smaller Raspberry Pi Zero. In addition there is the Raspberry Pi 400, which is a Raspberry Pi 4B integrated into a keyboard, and the Raspberry Pi Compute Module, which is mainly used in industrial applications.

## Do I require a programming knowledge?
You do not need any programming knowledge when wanting to work with the Raspberry Pi, and it can be used like any other (Desktop) computer. But to get the most out of your Raspberry Pi, some experience of working with the command line, and potentially Python, as well as interest in learning more about computing and electronics is recommended!

## Where to buy a Raspberry Pi?
The Raspberry Pi is available via a large number of distributors, including online retailers like amazon. For an overview, see the [Raspberry Pi products page](https://www.raspberrypi.org/products){:target="_blank"}.

## What other equipment to get?
As bare essentials, all you need is a Raspberry Pi, a micro-SD card, and 5V (2.5A+) power supply. See the [suggested hardware page](/getting-started/choosing-raspberry-pi-hardware) for more details.

## Do I need a keyboard, mouse, and screen to install my Raspberry Pi?
No, it is possible to install the Raspberry Pi as a *headless* unit, to enable you to connect to it over a wireless network via SSH upon first boot. Follow [the guide](/getting-started/raspberry-pi-headless-setup).

## How to set up and install a Raspberry Pi?
Please follow the detailed step-by-step instructions of the [installation guide](/getting-started/install-operating-system).

## Can I power the Raspberry Pi with a powerbank?
Yes, as long as it is 5V and provides at least 2.5A. Also note that if you let your Raspberry Pi run until the battery is empty, it will turn off abruptly, which may result in the system being corrupted.

## Can I power the Raspberry Pi with solar panels?
Yes, as long as it provides a current of at least 2.5A at 5V. A small 5V 6W solar panel can suffice for the most basic requirements. Larger, more permanent systems can be an ideal solution for many field systems, such as using a 12V/18V 50W solar panel, but then a 12V battery, a power converter, and solar charger will be needed. I suggest to read [this paper](http://doi.org/10.1111/2041-210X.13456){:target="_blank"}.

## How to shutdown the Raspberry Pi (when connected via SSH)
All you need is the simple command `sudo halt`.

## How to turn the Raspberry Pi back on
If you turned-off your Raspberry Pi, there is no easy way to remotely turn it back on again beyond simply disconnecting and reconnecting power again. If it is important for you to do this, one option might be to use a PoE HAT and power the Raspberry Pi using the ethernet cable from a dedicated router, with which you should be able to remotely connect and disconnect the power to your Raspberry Pi.

## Can I connect a Camera Module to the Raspberry Pi 400?
The Raspberry Pi 400 doesn't have the same CSI camera connector as the Raspberry Pi 4, so it's not possible to use a Camera Module or High-Quality Camera. You can, however, use USB cameras using the USB ports on the back of the Pi 400 keyboard.

## Is it possible to boot the Raspberry Pi form usb?
Yes this is possible on later models, but only after the Raspberry Pi has already been set up at least once. For more information, see [this page](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md){:target="_blank"}.

## Where can I get more help?
The best way to start is to search your specific issue online to see if others have also encountered and solved it, or post a message on a one of the community support forums, such as [raspberrypi.stackexchange.com/](https://raspberrypi.stackexchange.com/){:target="_blank"} and [raspberrypi.org/forums/](raspberrypi.org/forums/){:target="_blank"}.

*Many more questions will be added soon!*
{: .fs-5 .fw-300 }
