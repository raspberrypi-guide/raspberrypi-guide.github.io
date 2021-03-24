---
layout: page
title: Set-up a real-time clock
parent: Electronics
nav_order: 2
---

# Setting-up a real-time clock
{: .no_toc }

The Raspberry Pi keeps track of time by checking the internet, which becomes problematic when no internet connection is available. In this guide I explain how to add a real-time clock.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Time keeping
Because the Raspberry Pi is designed as an ultra-low cost computer, it lacks the little coin-battery-powered 'Real Time Clock' (RTC) module that sits in your laptop or desktop computer. Instead, the Raspberry Pi updates the time automatically from the global ntp (nework time protocol) servers. This can be a problem for stand-alone projects with no network connection, as your Raspberry Pi will not be able to accurately keep the time. There are various inexpensive add-on RTC boards available that simply plug on top of the Raspberry Pi's GPIO pins.

## Setting-up I2C
Any RTC uses the I2C protocol to communicate with the Raspberry Pi. So the first thing to enable a RTC is to set up I2C. To do so, run the following command:

```
sudo apt-get install -y i2c-tools
```

Make sure I2C is enabled by going to `Preferences` > `Raspberry Pi Configuration` > `Interfaces` > click `Enable` next to `i2c`, and click `OK`. Now turn off your Raspberry Pi (`sudo halt`).

## Setting up the RTC
Now plug your RTC board onto your Raspberry Pi GPIO pins. Here we will be setting up the DS1307 Real Time Clock, but many others exist (e.g. [this list](https://github.com/raspberrypi/linux/blob/rpi-4.4.y/arch/arm/boot/dts/overlays/i2c-rtc-overlay.dts)). Verify that the board is connected successfully by running:

```
sudo i2cdetect -y 1
```

You should see ID `#68` show up:

[![i2c sensor](/assets/images/i2c-sensor.png?style=centerimgmed)](/assets/images/i2c-sensor.png)

## Using the RTC
Before the RTC module can be used, we need to run a couple more commands. First, the RTC module must be loaded by the kernel:

```
sudo modprobe rtc-ds1307
```

Next, add the RTC kernel to the `/etc/modules` file so it is loaded when it boots:

```
sudo nano /etc/modules
```

adding `rtc-ds1307` at the end of the file.

Now add the device creation at boot by editing the rc.local file:

```
sudo nano /etc/rc.local
```

making sure to include the following lines just before `exit 0`:

```
echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device
sudo hwclock -s
date
```

If you now reboot, the Raspberry Pi should have the correct time from the hardware RTC.

## Commands for using the RTC
To read the time from the hardware RTC:

```
sudo hwclock -r
```

To copy the time from the Raspberry Pi system to the Hardware RTC:

```
sudo hwclock -w
```

To copy the time from the hardware RTC to the Raspberry Pi:

```
sudo hwclock -s
```
