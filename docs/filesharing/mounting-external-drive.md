---
layout: page
title: Mounting an external drive
parent: Filesharing
nav_order: 2
permalink: /filesharing/mounting-external-drive
comments: true
---

# Mounting an external drive
{: .no_toc }

To mount an external drive on the Raspberry Pi, a couple extra steps may be needed but this will help you get a solid connection to your drive.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Mounting automatically using the Desktop
Using the Raspberry Pi OS Desktop, any (readable) hard drive that is connected will be mounted automatically in the folder `/media/pi/`. It is subsequently very easy to share this folder over the network and thereby make the Raspberry Pi into a NAS, following the [filesharing guide](filesharing-raspberry-pi.html). In this way you can connect your external hard disk, SSD, or USB stick to any of the USB ports on the Raspberry Pi, and mount the file system to access the data stored on it. Your Raspberry Pi is actually in that way acting as a dedicated NAS-drive!

## Mounting manually
If you want to mount your drive manually, such as to make sure that the mount location is always the same or when not having access to the Desktop interface, connect the drive to your Raspberry Pi and create a target folder to be the mount point of the storage device, e.g. `exdisk`:

```
sudo mkdir /mnt/exdisk
```

Now find the name of the external disk:

```
fdisk -l
```

and look for the partition starting with `/dev/` that has the expected file size, e.g. `/dev/sdb2/`. Use that to mount the storage device at the mount point you just created:

```
sudo mount /dev/sdb2 /mnt/exdisk
```

You can verify that it is successfully mounted by listing the contents (`ls /mnt/exdisk`). To unmount a storage device:

```
sudo umount /mnt/mydisk
```

## Set up automatic mounting
You can modify the `fstab` file to define where storage devices will be automatically mounted when the Raspberry Pi boots. For this we will need the UUID of the disk partition:

```
sudo blkid
```

Now open the fstab file:

```
sudo nano /etc/fstab
```

and add the following lines, replacing with your UUID, mount location and filesystem type (e.g. ntfs, fat32, ext4):

```
UUID=D632-BE5F /mnt/exdisk fstype defaults,auto,users,rw,nofail 0 0
```

The same can be done with a network drive:

```
//NASdrive.local/data /home/pi/NAS cifs -o username=pi,password=naspassword 0 0
```

As this exposes your username and password this is not ideal and much better is to create a credentials file. Follow the security guide [here](../networking/raspberry-pi-security.html).

Now edit the `/etc/fstab` file as root user again to add your samba share:

```
//NASdrive.local/data /home/pi/NAS cifs -o credentials=mycredentials.env 0 0
```

Now test with

```
sudo mount -a
```

If the drive does somehow not mount, try adding `uid=1000,gid=1000,iocharset=utf8` to the fstab command.

## Drive not mounting at startup
The drives added to your fstab file should be automatically mounted upon startup. In some cases this does not happen, which may be to due with the type of drive you are mounting (e.g. `cifs`) or that your Raspberry Pi has not yet connected to the network at the mounting it is trying to mount the drive. To help overcome this I found it is best to add a mount command to the rc.local file. To do so, edit the rc.local file:

```
sudo nano /etc/rc.local
```

scroll to the bottom and just above `exit 0` add your command:

```
# Mount drive
sleep 5
sudo mount -t cifs //<drive location> <mount location> -o user=<username>,password=<password>
```

making sure to change the parameters within the <> brackets. The `sleep 5` command is needed to let the Raspberry Pi wait for a couple seconds to properly connect to the network and mount the drive.

Finally make  sure that the file rc.local is executable otherwise it will not run:

```
sudo chmod +x /etc/rc.local
```
