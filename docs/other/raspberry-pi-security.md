---
layout: default
title: Increasing security
parent: Other
nav_order: 1
permalink: /other/Improve-raspberry-pi-security
comments: true
---

# Improve Raspberry Pi security
{: .no_toc }

When working with the Raspberry Pi, it is a good idea to keep the following security considerations in mind.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Raspberry Pi security
The level of security you need for your Raspberry Pi will strongly depend on how you plan to use it. By default it is already quite secure and using it for a local network only simple changes may be needed. But when your Raspberry Pi is connected to the internet and for example used to broadcast live data, further security measures are recommended.

## Update the system
It is first of all important to ensure your system has the latest security fixes. This is as simple as keeping your version of Raspberry Pi OS  up-to-date. To do so, open a terminal window and enter:

```
sudo apg-get update && sudo apt-get full-upgrade
```

## Change default password
By default, the Raspberry Pi uses `pi` as  username and `raspberry` as password. So the next thing to do is change these. This can be easily done via the Raspberry Pi configuration panel via the Desktop or the terminal. Simply enter:

```
passwd
```

Now type in your new password and confirm it.

## Change default username
As deleting the default account could be dangerous without ensuring you have the correct permissions elsewhere, it is best to first create a new superuser account:

```
sudo useradd -m JUSTME -G sudo
```

Next, enter:

```
sudo passwd JUSTME
```

This will allow you to set a password for the new user. Your new account should now have the same permissions as pi, as both are in the sudo usergroup.

Before deleting the user pi, logout and then log in again using your new account, and attempt to run:

```
sudo visudo
```

If successful, you can delete the default pi user. In the terminal, enter

```
sudo deluser pi
```

If you want, you can also simultaneously remove the /home/pi directory:

```
sudo deluser -remove-home pi
```

## Install a firewall
There are a number of ways to add a firewall to your Raspberry Pi, including the `iptables` that comes with Raspberry Pi OS. I recommend to use the [UFW](https://wiki.ubuntu.com/UncomplicatedFirewall){:target="_blank"} ('uncomplicated firewall') interface.

To install the UFW software, open a terminal window and enter:

```
sudo apt install ufw
```

UFW will be installed but not active yet. Also by default it will block all incoming traffic and allow all outgoing traffic, this includes any SSH connections.

To open a port while using UFW, such as port 22, the default used for SSH, type in:

```
sudo ufw allow 22
```

You can also make it more specific to only allow specific IP-addresses:

```
sudo ufw allow from 192.168.1.100 port 22
```

Don’t forget to replace values with your own settings. On a local network you can get your ip address with the command `ipconfig` (Windows) or `ifconfig` (Linux/Mac).

To list the enabled firewall rules:

```
sudo ufw show added
```

Now to enable the firewall:

```
sudo ufw enable
```

Be careful as this will enable the firewall now, and you will get the message *Firewall is active and enabled on system startup*.

To display your current rules once ufw enabled, use this command:

```
sudo ufw status verbose
```

Quite complicated rules can be provided, such as to allow specific IP addresses to be blocked, specifying in which direction traffic is allowed, or limiting the number of attempts to connect. For more complex configurations, I suggest to check the manual, just type:

```
man ufw
```

## Work with credentials files
The final security recommendation (for now) is to make use of environmental variables to store credentials, such as email logins, that may be needed in user scripts. Environment variables are operating system level variables whose value can be used by software programs. As the values remain in the system, not in the script, there is less risk of exposing credentials.

Let's create a simple file called `mycredentials`:

```
nano ~/. mycredentials.env
```

Now enter any information you may want and use a variable name you can call upon in your scripts prepended with an `export` command. For example:

```
export GMAIL_USERNAME='XXXXXXX'
export GMAIL_PASSWORD='XXXXXXX'
```

Now save the file and change its permissions so it is not readable by others:

```
chmod 600 ~/.mycredentials.env
```

Make sure the variables are loaded:

```
source ~/.mycredentials.env
```

And finally, adapt your script to use the stored variables. For example, in Python:

```
import os
GMAIL_USERNAME = os.environ['GMAIL_USERNAME']
GMAIL_PASSWORD = os.environ['GMAIL_PASSWORD']
```

That's it!
