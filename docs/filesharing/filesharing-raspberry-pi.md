---
layout: page
title: Sharing files with the Raspberry Pi
parent: Filesharing
nav_order: 1
permalink: /filesharing/filesharing-raspberry-pi
comments: true
---

# Filesharing with the Raspberry Pi
{: .no_toc }

There are many ways to connect to see, copy, and edit files on a Raspberry Pi. Samba is one of the most versatile and is easy to configure to share directories with both Linux, Mac, and Windows operating systems.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Simple filesharing via SSH
The simplest way to share files with a Raspberry Pi is to use secure copy via SSH. To copy a file from the raspberry pi:

```
scp pi@<IP Address of Raspberry Pi>:<Path to File> .
```

Using a `.` at the end copies it to your current directory. To copy a file to the raspberry pi:

```
scp <Path to File To Copy> pi@<IP Address of Raspberry Pi>:<Path that File will Go>
```

## Installing Samba
A more versatile solution that also enables you to mount (drives on) your Raspberry Pi is to use Samba. To install, run the following command:

```
sudo apt install samba samba-common-bin
```

Next, we create a dedicated shared directory. It can be anywhere, but for this example we create a folder called `shared` at the top level of the root file system (`/`). Furthermore, to make the folder readable and writeable for all users while preventing it from accidentally deleted we add the permissions flag `1777`:

```
sudo mkdir -m 1777 /shared
```

To share the folder, we need to tell samba where it is. Open up the samba configuration file:

```
sudo nano /etc/samba/smb.conf
```

At the end of the file, add the following to share the folder, giving the remote user read/write permissions:

```
[pishare]
path = /shared
writable = yes
browseable = yes
create mask = 0777
directory mask = 0777
public = no
```

In brackets, in our example `[pishare]`, you can provide the name as the folder will appear on connected computers. If besides specific users you also want to enable guest access, add the line `Guest ok = yes`. Now exit and save the file by `ctrl+x` then `y` followed by `Enter`.

Now we want to set a Samba password, which can be the same as your standard password:

```
sudo smbpasswd -a pi
```

Finally restart the samba service for the changes to take effect:

```
sudo systemctl restart smbd
```

Samba will automatically start whenever you power on your Raspberry Pi.

## Sharing the home folder
To share the home folder and make it editable on Mac and Windows systems add the following code:

```
[pihome]
    comment = Pi Home
    path = /home/pi
    browsable = yes
    writable = yes
    force create mode = 0777
    force directory mode = 0777
    public = yes
```
Make sure to adapt the `comment` which is the name that will appear in the folder window and the `path` to take into account your username.

## Connecting to the shared folder
Connecting to the shared folder is quite easy with any computer on the network.

On a Mac, go to the `Finder` > `Go` > `Connect to server`. Now click `browse` to find the shared folder automatically, or you can directly enter the address in the address box as follows `smb://[ip-address]/[nameofshare]`.

On Windows, within the File Explorer click `Network` and there your Raspberry Pi should automatically appear. Click on it to see the folder you just shared.
