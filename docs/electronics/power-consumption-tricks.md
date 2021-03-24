---
layout: page
title: Reduce power consumption
parent: Electronics
nav_order: 6
---

# Reduce power consumption of the Raspberry Pi
{: .no_toc }

There are various ways to save power on your Raspberry Pi. Besides the model and reducing the processing needs, here are some extra steps to further reduce power consumption.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## First steps
If power consumption is critical for your project you should have already decided to use a power efficient Raspberry Pi, such as the Raspberry Pi A+ or Raspberry Pi Zero. Power consumption can be further reduced considerably by trying to keep processing needs to a minimum.

## Turn off USB/LAN
The most power hungry devices are the ones that use a USB connection, such as hard drives and peripherals like a mouse and keyboard. It is therefore best to minimise the use of these devices as much as possible.

To completely turn off the USB and Ethernet BUS chip, which can save up to 100mA, open a terminal window and enter:

```
echo '1-1' |sudo tee /sys/bus/usb/drivers/usb/unbind
```

To turn it back on again:

```
echo '1-1' |sudo tee /sys/bus/usb/drivers/usb/bind
```

## Turn of HDMI output
Similarly it is best to not use the HDMI output to further save power consumption of your Raspberry Pi. To do so, enter:

```
sudo /opt/vc/bin/tvservice -o
```

And to turn it back on again:

```
sudo /opt/vc/bin/tvservice -p

```

## Turn of Bluetooth
You will likely not need to use Bluetooth for your project, especially when power consumption is critical. To disable bluetooth, change the Raspberry Pi's config file:

```
nano /boot/config.txt
```

and add the following line:

```
dtoverlay=pi3-disable-bt
```

Now restart your Raspberry Pi to take effect. This should again help a bit to reduce the power consumption of your device.

## Turn off the on-board LEDs
Turning off the on-board LEDs may only help to shave off a couple mA. To do so, edit the `/boot/config.txt` file and add the following lines:

```
dtparam=act_led_trigger=none
dtparam=act_led_activelow=on
```

Now reboot for the changes to take effect.
