---
layout: default
title: (Automatic) file synchronisation
parent: Filesharing
nav_order: 3
permalink: /filesharing/file-synchronisation-rsync-rclone
comments: true
---

# File synchronisation with rsync and rclone
{: .no_toc }

There are numerous ways to synchronise files on your Raspberry Pi with other systems. Here I provide a guide for using `rsync` an `rclone`, which make it very straight-forward to synchronise files with any device.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Local file synchronisation
One of the best ways to synchronise files across computers on the same network is using `rsync`. Rsync, which stands for remote sync, transfers and synchronises files while comparing the modification dates and sizes of files, thereby only changing files when needed.

## Enable remote connections on client computer
To be able to send files from the Raspberry Pi we need to enable remote connections on the clients.

To enable remote connections on a Mac go to `System Preferences` > `Sharing` and tick the `on` box next to `Remote Login`. Now on the right side of the window it will display a command with which you will be able to connect to the computer using SSH.

To enable remote connections on Windows, open `Settings`, click `Network & Internet`, and click `Wi-Fi` or `Ethernet`, depending on your connection. Scroll down to the right and click `Change Advanced Sharing Settings`. In the Network Discovery section, select `Turn on network discovery` and also check the box that says `Turn on automatic setup of network connected devices`.

## Using rsync
It is very simple to use rsync. With the most basic command just needing `rsync` followed by the source and destination directory:

```
rsync sourcedirectory/ destinationdirectory
```

Make sure to add the `/` to the source directory unless you want to copy the source directory itself into the destination directory (rather than its contents).

To preserve everything and copy all files in a directory recursively, use the `-a` flag. Adding a `v` (e.g. `-av`) will show the verbose output and adding `P` (e.g. `-aP`) a progress bar.

Now to sync files to a remote system, make sure you have SSH access (see the [SSH guide](../networking/connecting-via-ssh.html). You can then use the following syntax for the destination directory: `user@remote-host:destinationdirectory`, e.g.:

```
rsync -a sourcedirectory/ user@remote-host:destinationdirectory
```

This is also called a "push" operation because it pushes a directory from the local system to a remote system. To do the opposite, i.e. a "pull" from the Raspberry Pi to the local system, the syntax would be:

```
rsync -a user@remote-host:directory localdirectory
```

In order to keep two directories truly in sync, it is necessary to delete files from the destination directory if they are removed from the source. By default, rsync does not delete anything from the destination directory. The `--delete` flag tells rsync to delete files in the destination directory when they do no (longer) exist in the source directory.

It is also possible to delete the source files automatically with the `--remove-source-files` flag. This can be handy to not use up the extra space on the Raspberry Pi when files have already been copied. But be careful with this command as it will thus delete the original files from the host computer.

## Uploading data to the cloud
There are a number of different ways to facilitate uploading of documents to the cloud. A great way to do this is using `Rclone`. This open-source software can be configured to connect to many popular cloud storage services such as google drive and dropbox, and update and manage files and folders between your Raspberry Pi and one or more remote services.

It is  very easy to set up and install, just follow the steps from the rclone website: [https://rclone.org/docs/](https://rclone.org/docs/){:target="_blank"}. When set up successfully, you should be able to sync to your cloud storage device using very similar commands as used by rsync, such as:

```
rclone sync -i /local/path remote:path
```

## Automatic synchronisation
A great way to automate the synchronisation of files using `rclone` and `rsync` is to create a [cron job](https://en.wikipedia.org/wiki/Cron){:target="_blank"} with a specific schedule.

To do so, we first need to create a bash script that contains the commands. In this example we will use `rsync`, but using `rclone` would be very similar. Open a terminal and enter:

```
nano /home/pi/autosync.sh
```

Now as an example we want to synchronise a folder `data` in the root directory and synchronise it with a folder `rpidata` in the user directory of the client computer. We also want it to add some print statements with the date and time:

```
#!/bin/bash
NOW = "$(date)"
echo "$NOW - Synchronising"
/usr/bin/rsync -a /data/ [user]@[clientcomputer]:rpidata
NOW="$(date)"
echo "$NOW - Synchronising finished"
```

Close and save the file (`ctrl+x`, `y`,`Enter`). Now to test the file, run the following:

```
bash autosync.sh
```

If it executes correctly we can create a schedule to automatically run the bash file with cron. To do so, enter:

```
crontab -e
```

Now let's say we want the Raspberry Pi to run the `autosync.sh` file every day at 18h and have the output written (append) to a logfile (e.g. called `synclog.txt`). Simply enter the following command:

```
* 18 * * * /home/pi/autosync.sh > /home/pi/synclog.txt 2>>&1
```

Close the editor (`ctrl+x`, `y`, `Enter`), and now the script will be automatically run and its output written to the provided logfile!

To help define the schedule, [crontab-generator.org](https://crontab-generator.org/){:target="_blank"} is a great tool.
