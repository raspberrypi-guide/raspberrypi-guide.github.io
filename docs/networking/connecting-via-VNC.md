---
layout: page
title: VNC Connection
parent: Networking
nav_order: 2
---

# Connecting to your Raspberry Pi via VNC
{: .no_toc }

The Raspberry Pi can be controlled like any other Desktop computer using a keyboard, mouse, and monitor. VNC makes it possible to connect to and work with the Desktop interface of your Raspberry Pi remotely, even across the internet.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---



## What is VNC
VNC (Virtual Network Computing) allows you to remotely control the desktop interface of the Raspberry Pi from another computer or mobile device without the need for a monitor, enabling you to control your Raspberry Pi from anywhere. This contrasts with [SSH](http://), which only provides terminal access.

[![VNC connection](/assets/images/vncconnection2.jpg?style=centerimgmed)](/assets/images/vncconnection2.jpg)

## Enable VNC on the Raspberry Pi
By default, VNC is disabled on the Raspberry Pi. It can be easily enabled both using the Desktop and via the terminal. To enable VNC via the Desktop, go to the start menu > `Preferences` > `Raspberry Pi Configuration`.

[![Desktop Configuration](/assets/images/desktop-configuration.png?style=centerimgmed)](/assets/images/desktop-configuration.png)

Now click on `Interfaces` and click `enable` next to VNC and click `OK`.

To enable VNC via the terminal, open a terminal window and enter `sudo raspi-config`. Now with the arrows select `Interfacing Options`, navigate to and select `VNC`, choose `Yes`, and select `Ok`.

## Connecting via VNC
The full image of the Raspberry Pi OS comes with RealVNC Connect software. If you are using a different version, you can install VNC via the terminal:

```
sudo apt update
sudo apt install realvnc-vnc-server realvnc-vnc-viewer
```

We need to make sure the VNC server of the Raspberry Pi is running. Open a terminal window and enter:

```
sudo raspi-config
```

Now navigate to `Interfacing Options` > `VNC` > `Yes`.

Next, install the VNC Viewer software on your other device ([download link]([https://www.realvnc.com/en/connect/download/viewer/). Now get the ip address of your Raspberry Pi by typing in:

```
hostname -I
```

And finally, copy this IP address to the VNC Viewer window to connect. In a couple seconds a window with the virtual desktop should open up, giving you full access to your Raspberry Pi.

## Enable camera view on VNC
Streaming the camera while using VNC is not enabled by default. To enable this, on the desktop, click the VNC icon in the menu bar and then click the menu button in top right corner. Now go to `options` > `troubleshooting` and click `Enable direct capture mode` as well as `Enable harwarde JPEG encoding`. Now you should be able to see a live stream of the camera by opening a terminal window and entering:

```
raspistill -t 0 -k
```

To exit, enter `ctrl+x`.

## Connecting via VNC over the internet
Besides direct connections on a private network, also end-to-end encrypted cloud connections are possible (free for non-commercial use), enabling you to create a VNC connection over the internet. These connections are encrypted end-to-end and do not require (complicated) firewall or router configuration.

All you need to do is [sign up](https://www.realvnc.com/en/raspberrypi/#sign-up) for a RealVNC account, sign-in to your account on both your Raspberry Pi and the host computer, and then simply click connect to connect to your Raspberry Pi.
