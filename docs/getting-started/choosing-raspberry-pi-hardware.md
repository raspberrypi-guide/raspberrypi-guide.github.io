---
layout: page
title: Choosing your hardware
parent: Getting started
nav_order: 1
permalink: /getting-started/choosing-raspberry-pi-hardware
---

# Raspberry Pi hardware
{: .no_toc }

Here I provide an overview of what hardware you may need for your project, from the bare essentials, to recommended peripherals, and tools to work with electronics.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## The bare essentials

1. A Raspberry Pi. The optimal model depends strongly on the processing power and connectivity required, see [the Raspberry Pi page](raspberry-pi.html) to help you decide which model to choose.
2. A micro-SD card to store the operating system and user data.
3. A power supply of 5V DC, with 2.5A recommended to guarantee a stable working system.

[![Raspberry Pi Hardware](/assets/images/raspberry-pi-equipment.jpg?style=centerimgmed)](/assets/images/raspberry-pi-equipment.jpg)

## What Raspberry Pi model to choose
The [different models of Raspberry Pi](https://www.raspberrypi.org/products/) are all built with broadly the same functionality but differ considerably in processing speed, power requirements, and connectivity.

At the time of writing, the Raspberry Pi 4 is the fastest model, both in terms of its computing power (quad-core 1.5GHz; 2-8 GB RAM) and its connectivity, due to its USB 3.0 ports (read/write speeds up to 300 Mbps), high-speed Gigabit Ethernet (900 Mbps) and Wireless LAN (up to 100 Mbps). It is however also the most power hungry (2.7W-6.4W based on [benchmarks](https://www.pidramble.com/wiki/benchmarks/power-consumption)).

The Raspberry Pi Zero (W) is half the physical size, lacks a considerable part of the connectivity, and has much lower processing power (single-core 1GHz; 512 MB RAM), but only needs 0.8 W at idle, making it ideal for simpler, battery-powered solutions.

The Raspberry Pi 3A+ is an in-between model for users that seek to balance performance with power requirements, and the Raspberry Pi 400 is a Raspberry Pi 4B integrated in a keyboard and lacks a camera port and hence best for Desktop use.

Machine learning is possible with the more powerful Raspberry Pi’s, but a dedicated Neural Compute Stick is still needed for real-time object detection.

[![Raspberry Pi's](/assets/images/raspberry-pis.jpg?style=centerimgmed)](/assets/images/raspberry-pis.jpg)

## Recommended additional hardware
A keyboard, mouse, and computer screen are generally recommended for first-time users, and many small, cheap versions are available. Although these are not actually needed (see the [headless installation](gettomg=started/raspberry-pi-headless-setup.html) guide), for flexibility and testing it is recommended to have them as well as additional Raspberry Pi’s, micro-SD cards and chargers where possible.

The Raspberry Pi Touchscreen is also a great tool that can for example be used to quickly connect for troubleshooting, such as when you are not able to get a remote network connection to your Raspberry Pi.

It is also recommendable to use a case for your Raspberry Pi to give the bare circuit board a bit more protection, especially to prevent short-circuits.

The Raspberry Pi camera will come to great use for many projects, and a variety of cameras exist, both from the Raspberry Pi Foundation and other companies (see the [camera guide](http://)).

Also a Raspberry Pi power management HAT (such as the [PiJuice](https://uk.pi-supply.com/collections/pijuice)) will be of great use to many projects.

## Hardware for working with electronics
When building custom electronic solutions, one may additionally need some or all of the following: electrical tape, wire cutters, pliers, bread boards, jumper wires, standard electrical wire, soldering equipment, heat shrink sleeves, and a heat gun. Also, a soldering helping hand and a multi-meter may come in handy.

When building custom solutions, aluminium profiles (like from [makerbeam.com](http://makerbeam.com_)) can help to create a sturdy, organised structure for your device.
