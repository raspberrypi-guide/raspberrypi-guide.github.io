---
layout: page
title: First boot configuration
parent: Getting started
nav_order: 4
permalink: /getting-started/raspberry-pi-configuration
---

# First boot configuration
{: .no_toc }

Upon first boot of your Raspberry Pi you may want to make a number of changes to the configuration to finish setting-up. Here are some of the steps I recommend.
{: .fs-6 .fw-300 }


## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Start up your raspberry pi
Make sure you have  [installed your Raspberry Pi](http://), powered it up, and are either connected directly (using keyboard, mouse, and screen) or remotely using [SSH](http://) or [VNC](http://). If using a direct connection make sure your Raspberry Pi is connected to the internet, either via WiFi or Ethernet, otherwise you won't be able to set it up properly.

## Welcome wizard
The Raspberry Pi Desktop interface starts a Welcome setup wizard. This may be helpful for some but not needed for others and actually not available with an SSH connection. If you do decide to not want to use the wizard and set things up further via the terminal, we need to make sure the welcome wizard does not come up anymore in the future. To do so open a terminal window, if you haven't already, and type in:

```
sudo rm /etc/xdg/autostart/piwiz.desktop
```

```
sudo apt purge piwiz
```

[![Welcome Wizard](/assets/images/piwiz.gif?style=centerimgmed)](/assets/images/piwiz.gif)

## Make sure the Raspberry Pi is fully up to date
A first step is to make sure the Raspberry Pi is fully up to date. When not using the welcome wizard, we can do this by typing in the following commands in the terminal:

```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get autoremove -y
```

## Configuring Raspberry Pi
Now let's change some configuration settings. This can both be done visually or with the `raspi-config` tool using the terminal (find more information [here](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)).

### Using the terminal
Type in the following command to start the configuration panel:

```
sudo raspi-config
```

First, let's change the password by selecting `Option 1 > S3`. Also change the hostname (`Option 1 > S4`). This is especially needed if you have two or more Raspberry Pi's to prevent name conflicts. Also change the localisation if needed (`Option 5`).

I recommend to set the system to wait for network at boot (`option 1 > S6`) as sometimes the system continues booting when not yet a working internet connection has been established, making it hard to subsequently connect. By default the Raspberry Pi shows a splash screen at boot. I prefer to disable this and see the actual boot-up sequence commands. To do so, choose `Option 1 > S7`.

Next we want to enable SSH, VNC, and the Camera, unless you really do not plan on using them. SSH will already be enabled if you did a [headless installation](http://), otherwise choose `Option X > 1 Yes`. To enable VNC, simply click `Option 3 > 3 Yes`, and to enable the camera `Option 3 > 1 Yes`.

For some uses of the Raspberry Pi it is recommendable to increase the memory dedicated to the GPU, such as when recording videos at high resolution and frame-rate. You can choose to split the memory for the GPU using `Option 4 > 2` and I recommend to set this at `256mb`.

Finally, we will want to expand the filesystem (`Option 6 > A1`) to be able to use all the space of the memory card (note this is not needed when you have used NOOBS).

Now click `yes` to reboot when asked.

[![SSH terminal configuration](/assets/images/terminal-ssh-configuration.jpg?style=centerimgmed)](/assets/images/terminal-ssh-configuration.jpg)

### Using the Configuration Menu using the Desktop interface
 1. Select raspberry symbol in the top left of the screen.
 2. Scroll down to preferences.
 3. Select *Raspberry Pi Configuration*.
 4. Click the *interfaces tab*, and enable: a. SSH, to connect wirelessly. b. I2C, for the light sensor. c. Camera, to use the camera. d. Remote GPIO, to use our sensors over the internet.
5. Click Localization tab. 6. Select “Set WiFi Country” and scroll down to select the appropriate country.
7. Select “Set Time Zone” and select the appropriate time zone.
8. Select “Keyboard” and select the corresponding locality/language that matches the appropriate keyboard configuration.
9. Click “OK” and reboot the Raspberry Pi.

[![Desktop Configuration](/assets/images/desktop-configuration.jpg?style=centerimgmed)](/assets/images/desktop-configuration.jpg)

## Remove default folders
I tend to remove the default folders to minimize clutter:

```
rm -R MagPi Music Pictures Public Templates Videos
```

## Install virtual Keyboard
I recommend to install a virtual keyboard just in case I have issues with a headless setup and have the Raspberry Pi touchscreen. Simply run the command:

```
sudo apt-get install matchbox-keyboard -y
```

and access the keyboard via `menu` >> `accessories` >> `keyboard`.

## Enable camera view on VNC
If you are planning on connecting to the Raspberry Pi via VNC and want to stream the Raspberry Pi camera, you need to first enable this. On the desktop, click the VNC icon in the menu bar and then click the lines in top right corner, go to `options > troubleshooting` and click `Enable direct capture mode` as well as `Enable harwarde JPEG encoding`. Now you should be able to see a live stream of the camera when entering `raspistill -t 0 -k` in the terminal (exit by `ctrl+x`).

[image here]
