---
layout: page
title: Connecting via SSH
parent: Networking
nav_order: 1
permalink: /networking/connecting-via-ssh
comments: true
---

# Connecting to your Raspberry Pi via SSH
{: .no_toc }

The Raspberry Pi can be controlled like any other Desktop computer using a keyboard, mouse, and monitor. However, there are also various ways to command the Raspberry Pi remotely, of which SSH is one of the best and often used.
{: .fs-6 .fw-300 }

# Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## What is SSH
Secure Shell (SSH) enables you to access the command line of a Raspberry Pi from another computer or device on the same network. This is very handy for quickly installing software or editing configuration files. SSH is pre-installed on Linux, Mac and some Windows operating systems and can also be installed on mobile devices. SSH does not provide any visual access to the Raspberry Pi Desktop. If this is needed, I recommend to use [VNC](connecting-via-VNC.html).

## Enable SSH on the Raspberry Pi
By default, SSH is disabled on the Raspberry Pi. It is however very easy to enable it, both using the Desktop and via the terminal. To enable SSH via the Desktop, go to the start menu > `Preferences` > `Raspberry Pi Configuration`.

[![Desktop Configuration](/assets/images/desktop-configuration.jpg?style=centerimgmed)](/assets/images/desktop-configuration.jpg)

Now click on `Interfaces` and click `enable` next to SSH and click `OK`.

[![SSH desktop configuration](/assets/images/desktop-ssh-configuration.jpg?style=centerimgmed)](/assets/images/desktop-ssh-configuration.jpg)

To enable SSH via the terminal, open a terminal window and enter `sudo raspi-config`. Now with the arrows select `Interfacing Options`, navigate to and select `SSH`, choose `Yes`, and select `Ok`.

[![SSH terminal configuration](/assets/images/terminal-ssh-configuration.jpg?style=centerimgmed)](/assets/images/terminal-ssh-configuration.jpg)

If you want SSH to be enabled upon first boot, such as for a headless installation, follow [this short guide](../getting-started/raspberry-pi-headless-setup.html).

## Connecting via SSH
Now SSH is enabled, we need to know the hostname of the Raspberry Pi or use its IP address to connect to it. To know the ip address, on your Raspbery Pi type in:

```
hostname -I
```

Now to connect, on the host computer open a terminal window and type in

```
ssh [username]@[hostname].local
```
or

```
ssh [username]@[ip address]
```

It is also possible to directly send a single command to your Raspberry Pi, such as to shut it down:

```
ssh pi@mypi.local "sudo shutdown -h now"
```

## Enable SSH on the host device
SSH is standard available on Linux distributions and on Mac so should work automatically.

To enable ssh on a Windows 10 computer, make sure it has the October 2018 Update or later and go to `Settings` > `Apps` > `Apps & features` > `Manage optional features` > `Add a feature`, and choose to install OpenSSH Client.

On other Windows installations you may need to install an SSH client, of which PuTTY is the most commonly used. Go to [putty.org](https://www.putty.org){:target="_blank"}, download the 64-bit MSI (Windows Installer), and open it to run the installer. Now launch PuTTY, set the Host Name (or IP address) field, `Port` to `22`, and `Connection type` should be set to `SSH`. Now click `Open` and a new terminal window should appear prompting you for a user name.

Finally, it is also possible to use SSH on your mobile device. Several good quality clients are available, of which I recommend Termius ([termius.com](https://www.termius.com){:target="_blank"}), an application that is availble for both iOS and Android.

[![SSH iOS configuration](/assets/images/iOS-ssh-configuration.jpeg?style=centerimgsmall)](/assets/images/iOS-ssh-configuration.jpeg).

## Passwordless SSH
When using SSH, each time you connect you will be asked for the password of your Raspberry Pi. In some cases it may be preferable to access your Raspberry Pi from another computer without a password, such as to (automatically) send files using `rsync` (follow the guide [here](../filesharing/file-synchronisation-rsync-rclone.html)). To enable password-less access with SSH you will need to generate an SSH key. To do so, open a terminal window and enter:

```
ssh-keygen
```

Now click `Enter` twice to generate and store the unique key in the default location and with the default passphrase. The private and public keys will now be stored in `~/.ssh`.

Next we need to copy the public key to your Raspberry Pi. To do so, simply enter:

```
ssh-copy-id [username]@[ip address]
```

Authenticate this step with your password and you are done. To verify the SSH key was successfully copied to the remote host, SSH to the Raspberry Pi from the host device or vice versa. No password should be required if the key was copied successfully.
