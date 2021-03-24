---
layout: page
title: Creating a headless set-up
parent: Getting started
nav_order: 3
permalink: /getting-started/rasperry-pi-headless-setup
---

# Creating a headless Raspberry Pi
{: .no_toc }

Using a standard operating system installation you won't be able to connect to your Raspberry Pi remotely upon first boot. However, with a couple easy steps this is possible, thus overcoming the need for any keyboard or mouse to be attached.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Enable SSH
With the default installation your Raspberry Pi, [SSH](http://) is not enabled by default for security reasons. We can however enable it by placing an empty file named `ssh` (no extension) in the root of the boot disk.

You can either do this using a text editor program or using the terminal by going to the directory of the drive `cd PATHOFDRIVE` and then typing `touch ssh` when on a Mac computer or `type NUL >> ssh` on windows.

## Add network info
Next your Raspberry Pi will need to know the wireless network from which you will connect. To do so, create a file called `wpa_supplicant.conf` on the Raspberry Pi SD-card, such as with a text editor program, and add the following information:

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
Update_config=1
Country=DE

Network={
    ssid="YourWifiNetwork"
    psk="WifiPassword"
}
```

Make sure to edit the country code and WiFi credentials such that the WiFi works properly.This file will be automatically picked up on first boot and enabling the Raspberry Pi to connect to the network.

Now simply eject the micro SD card safely and boot up the Raspberry Pi.

## Login over WiFi
Following the above steps, SSH should be enabled on your new device and it should be connected to your WiFi network. The default user is `pi`, the hostname `raspberrypi`, and the password `raspberry`. You can use these credentials now to log in to your Raspberry Pi remotely by typing in the following:

```
ssh pi@raspberrypi.local
```

Note, to be able to access your Raspberry Pi on your network by its hostname on Windows you have to install the Bonjour service first unless you have iTunes installed, find the installer [here](https://support.apple.com/kb/DL999?locale=en_US).

Now you should have been able to connect to your newly installed Raspberry Pi without the need of any peripherals! Do not forget to change your hostname and password (follow [this guide](http://)).
