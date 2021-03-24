---
layout: page
title: Mount Raspberry Pi SD card
parent: Filesharing
nav_order: 4
---

# Mounting the Raspberry Pi SD card
{: .no_toc }

In some cases you may wish to mount the Raspberry Pi SD card, such as to access your files or to change some configuration.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Mount the Raspberry Pi SD card on Linux
The Raspberry Pi OS is written to a partition with an `ext4` journaling file system. This is a native file system for Linux operating systems, so the moment you insert the Micro SD card with your Raspberry Pi installation on another Linux computer using a USB SD card reader, it should automatically mount on your computer and enable you to see all files.

## Mount the Raspberry Pi SD card on Mac
Unfortunately Mac computers cannot read the `ext4` journaling file system by default. This can however be enabled with a couple steps.

First we need to install Homebrew. Enter the following command in the terminal:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Now install oxfuse and ext4fuse

```
brew install osxfuse --cask
brew install ext4fuse
```

These steps may take a while..

Now plug your Raspberry Pi SD card in your mac. To find the name of the disk, enter `diskutil list`. Here it will show you a name like `disk2s2`. To mount it create a mount point:

```
sudo mkdir /Volumes/raspberry
```

And now mount the SD card with the following command:

```
sudo ext4fuse /dev/disk2s2 /Users/me/RPi -o allow_other
```

Now your SD card should be mounted on your Mac and give you access to all its files.

[![mounted SD card](/assets/images/mounted-sd-card.png?style=centerimgmed)](/assets/images/mounted-sd-card.png)

To unmount again:

```
sudo umount /Users/me/RPi
```

## Mount the Raspberry Pi SD card on Windows
Although `ext4` is the most common Linux file system, it's not supported on Windows by default either, which uses `FAT32` and `NTFS` as main file systems. There are a couple software packages that make it possible to mount an `ext4` drive. I suggest to use the Windows file system driver software Ext2Fsd.

First download the free software at [http://Ext2Fsd.com](http://Ext2Fsd.com). Then install and launch the program on your Windows PC.

In the program go to `Tools` > `Service Management` > `Start` before accessing Linux files. Also check *Mount all volumes in read-only mode* and *Assign drive letter automatically* boxes and click *Apply*.

[![windows mounted SD card](/assets/images/windows-mounted-sd-card.png?style=centerimgmed)](/assets/images/windows-mounted-sd-card.png)

In the window, scroll down to see if the `ext4` partition of the SD card indeed has its own drive letter. If not, right-click the entry and add Drive letter. You should now be able to find your Raspberry Pi SD Card mounted in Windows Explorer.
