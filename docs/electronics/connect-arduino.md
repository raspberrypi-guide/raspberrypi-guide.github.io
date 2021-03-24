---
layout: default
title: Connect an Arduino
parent: Electronics
nav_order: 1
permalink: /electronics/connect-arduino
---

# Connecting an Arduino to the Raspberry Pi
{: .no_toc }

In some cases it may be very helpful to combine an Arduino with a Raspberry Pi and luckily this is very easy to do
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---
## Install Arduino IDE
The Raspberry Pi makes a great host for the Arduino, which is a much simpler microcomputer but with some complementary capabilities. To control the Arduino we will use the Arduino IDE like on any other computer. To install:

```
sudo apt-get update
sudo apt-get install arduino
```

## Connect the Arduino

Now to connect, simply plug in the USB-cable into the Arduino and any of the USB ports on the Raspberry Pi. When you launch the Arduino IDE, it polls all the USB devices and builds a list that is shown in the `Tools` > `Serial Port` menu.

In order to access the serial port, you’ll need to make sure that the Raspberry Pi user has permission to do so. You can do that by adding the user (e.g. `pi`) to the so-called `tty` and `dialout` groups, which needs to be done before running the Arduino IDE:

```
sudo usermod -a -G tty pi; sudo usermod -a -G dialout pi
```

## Sending files to your Arduino
Click `Tools` > `Serial Port` and select the serial port (most likely `/dev/ttyACM0`), then click `Tools` > `Board`, and select the type of Arduino Board you have (e.g., the Uno).

Now to start, click `File` > `Examples` > `01.Basics` > `Blink` to load a basic example sketch. Click the Upload button in the toolbar or choose `File` > `Upload ` to upload the sketch to your Rasbperry Pi. If everything worked correctly, the LED on your Raspberry Pi should start blinking continuously.
