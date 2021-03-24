---
layout: page
title: Set up a static IP-address
parent: Networking
nav_order: 5
---

# Set up a static IP-address on the Raspberry Pi
{: .no_toc }

By default, the IP-address of the Raspberry Pi is dynamic, meaning it changes as you restart it or potentially when new devices are added to the wireless network. To make it easier to connect and have a more stable connection I recommend to set up a static IP address.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Get a static IP-address
To get a static IP-address that works, it will need to be within the range provided by the router. We will therefore first need to find the router’s ip address. This tends to be written on the bottom of the router. If not, simply open a terminal window and type in `netstat -nr`.  Now look under `Gateway`:

[![internet gateway](/assets/images/internet-gateway.jpg?style=centerimgmed)](/assets/images/internet-gateway.jpg)

You can also use the command `ip route | grep default | awk '{print $3}'`.

In this example it is `192.168.0.1`. Using the router’s ip address we can choose a static ip address in the range between 1 and 255, which will become the last number of your ip-address, e.g. `192.168.0.40`.

Determine if you want a static ip address over WiFi or Ethernet. The interfaces are called respectively `wlan0` and `eth0`.

## Setting up using the Desktop
It is very simple to set up your static ethernet address. Simply right-click on the Wi-Fi icon in the menu bar (top-right on the left of the speaker icon) and select the `Wireless & Wired Network Settings`.

Now click the empty dropdown menu and select the network interface you want to configure. Now for `IPv4 Address` enter your chosen ip address, for `Router` the IP address of the router. AS DNS Servers add `8.8.8.8`. Finally, click the `Disable IPv6` option.

## Setting up with the Terminal
One can also set-up a static ip address via the terminal. For this we need to enter the `dhcpcd.conf` file:

```
sudo nano /etc/dhcpcd.conf
```

Now scroll to the bottom, and add the following text:

```
interface INTERFACE
static ip_address=YOURSTATICIP/24
static routers=YOURGATEWAYIP
static domain_name_servers= YOURGATEWAYIP
```

replacing the words in capital by what is desired. Now save the file by pressing `ctrl+x` then `y` to exit.

## Prioritising internet interface

To make one internet interface have priority over the other, such as Ethernet over Wifi, add a `metric` number to each, with the higher metric being prioritised first. Open the `dhcpcd.conf` file:

```
sudo nano /etc/dhcpcd.conf
```

And add the metrics. For example:

```
interface eth0
metric 300
static ip_address=192.168.0.40/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1

interface wlan0
metric 200
```

Now finally reboot your Raspberry Pi for the changes to be incorporated:

```
sudo reboot
```

Once your raspberry pi has finished restarting, connect to it locally to verify the static IP address `hostname -I` or ping from it on a networked computer `ping YOURSTATICIP`.

## Disabling static IP-address
In many cases you may not want your Raspberry Pi set to use a static IP address. You can change the network configuration back by editing `dhcpcd.conf` again (`sudo nano /etc/dhcpcd.conf` and removing all the lines you added in the previous step.
