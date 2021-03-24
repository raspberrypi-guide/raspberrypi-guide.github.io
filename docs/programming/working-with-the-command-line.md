---
layout: default
title: Working with the command line
parent: Programming
nav_order: 1
---

# Working with the command line
{: .no_toc }

You will likely be using the command line a lot when working with Raspberry Pi's. Below I provide a concise list of the essentials. If you are not already a bit familiar with the command line, I recommend the free [Raspberry Pi Command Line book](http://).
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

[![terminal window](/assets/images/terminal.jpg?style=centerimgmed)](/assets/images/terminal.jpg)


## Terminal control
- Hold option (`alt`) and click a position in the current line to move your cursor to that position.
- Pressing the UP key will print the last command entered into the command prompt. This is a quick and easy way to repeat or correct previous commands.
- Show the history of all entered commands: `history`
- Clear the current window, useful if your previous commands are cluttering things up.: `ctrl + l` or `clear`
- Stop the process currently running: `ctrl + c`
- While writing in terminal, jump to left and right on the same line: `ctrl + a` and  `ctrl + e`.
- To let something run in the background, even when you close a session you can use `screen`. To start a new screen `screen -s <name>` and to later resume it `screen -r <name>` If you forgot the name of your screen just type `screen -r` to show the list of screens
- To exit the terminal (or screen): `exit`

## File and directory commands
- Get the path of the current directory: `pwd`
- Go to directory/go to home directory: `cd sample-dirname` / `cd ~`
- Go to previous directory: `cd -`
- Make a directory: `mkdir sample-dirname`
- Remove an empty directory: `rmdir sample-dirname`
- Remove a directory and all of its contents: `rm -rf sample-dirname/`
- Create a symlink: `ln -s source-dirname destination-dirname`
- List the contents of the directory: `ls`
- Show the entire lower file tree: `tree`
- Show details of multiple files: `file filename1 filename2`
- Create a new, empty file (e.g. named example.txt) in the current directory: `touch sample-filename.txt`
- Create a file/display the contents of a file: `nano sample-filename.txt`
- To save and exit a file (when editing with nano): `ctrl+x`, `y`, `Enter`
- Display the contents of a file: `cat sample-filename.txt`
- Remove a file: `rm sample-filename.txt`
- Move/rename a file: `mv current-filename.txt new-filename.txt`
- Copy file or directory: `cp examplefile.txt /home/pi/office/`
- Copy file from server to local via SSH: `scp pi@192.168.0.0:/path/to/file.png ~/Desktop/`
- Copy file from local to server via SSH: `scp ~/Desktop/file.png pi@192.168.0.0:/path/to/folder `

## Networking and system commands
- Check the status of the network connection you are using: `ifconfig`
- Print a list of the currently available wireless networks: `iwlist wlan0 scan`
- Test connectivity between two devices connected on a network or with the internet: `ping 10.0.0.32` and `ping http://google.com`.
- Download a file (e.g. example.txt) from the web and saves it to the current directory: `wget http://www.website.com/example.txt`
- Connect to a device using SSH and the device name: `ssh pi@rasperrypi.local`
- Connect to a device using SSH and the IP-addres of the device: `ssh pi@192.168.64.xxx`
- Find all available devices on the network: `arp -a`
- Get the hostname: `hostname`
- Get the hostname IP: `hostname -I`
- List USB hardware connected to your Raspberry Pi: `lsusb`
- Check free space on your Raspberry Pi: `df -h`
- Show the current date and time: `date`

## Raspberry Pi specific commands
- Synchronize the list of packages on your system to the list in the repositories: `apt-get update`
- Upgrade all of the software packages you have installed: `apt-get upgrade`
- Following from these, update raspbian to latest version: `sudo apt-get update && sudo apt-get upgrade`
- Open the configuration settings menu: `raspi-config`
- To shutdown: `sudo halt` or `shutdown -h now`
- To reboot: `sudo reboot`
- Take an image with the camera module: `raspistill -0 image.jpg`
- Stream the camera: `raspistill -t 0 -k` (to exit: `ctrl+x`)
- Record a 10s video with the camera module: `raspivid -o video.h264 -t 10000`

## Sudo
There are two user “modes” you can work with on the command line. The standard one is a user with basic access privileges. The other is a mode with administrator access privileges (AKA super user, or root). Some tasks can’t be performed with basic privileges and the super user must be used. To do so, the prefix `sudo` needs to be added to the command.

## Installing software using apt
`apt` is a package manager included with the Raspberry Pi OS that makes it very easy to install and manage new software packages on your Raspberry Pi. Note that a super user (see above) is needed to install or remove packages.

- To install a new package: `sudo apt install <package-name>`
- To update list of software packages available on your system: `sudo apt update`
- To remove and uninstall a package: `sudo apt remove <package-name>`
- List all packages on your system: `dpkg -l`
