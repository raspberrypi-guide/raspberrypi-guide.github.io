---
layout: default
title: Setting up the camera
parent: Electronics
nav_order: 1
---

# Connecting an Arduino to the Raspberry Pi
---
## Enable and test the camera
To be able to use the camera we need to enable it in the configuration menu. Enter:

```
sudo raspi-config
```

go to `5 Interfacing options`, then `P1 Camera`, and click `yes`. Alternatively you can go to the main menu and use the Raspberry Pi Configuration tool there. Now reboot your pi if you have already set up your raspberry pi camera. If not, turn of your raspberry pi and now connect one part of the ribbon cable to the camera and the other end to the raspberry pi by pulling up the edges of the plastic clip of the camera module port and sliding in the ribbon cable, making sure the cable is the right way around.

You can test the camera quickly by entering the command `raspistill -t 0 -k` in a terminal window. To exit again, press `ctrl+c`. If you get an error message, then double check the cable is properly connected to the raspberry pi and the camera and try restarting.
