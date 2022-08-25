---
layout: page
title: Installing OpenCV
parent: Programming
nav_order: 8
permalink: /programming/install-opencv
comments: true
---

# Install OpenCV on your Raspberry Pi
{: .no_toc }

Below I guide you through the basic steps necessary to get OpenCV working on the Raspberry Pi as well as on Ubuntu and Mac.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## OpenCV
[OpenCV](https://opencv.org){:target="_blank"} is a very extensive and incredibly powerful library for (real-time) computer vision, including object detection, motion tracking, and camera calibration.

Installing OpenCV used to be a very complicated and long process, especially on older models. Luckily it is now relatively easy to [install OpenCV with pip](https://pypi.org/project/opencv-python){:target="_blank"}. For more background information, see [the article](https://www.pyimagesearch.com/2018/09/19/pip-install-opencv/){:target="_blank"} by Adrian Rosebrock.

## Install prerequisites
Pip is the main package manager for python that we will also use to install OpenCV. Pip should already be installed on your system (see [here](https://pip.pypa.io/en/stable/installing/){:target="_blank"})

Next, for some versions of Raspberry Pi OS we may need to install some additional packages. First make sure `apt-get` is fully up-to-date by entering the following in Terminal:

```
sudo apt-get update
```

Now install the prerequisites:

```
sudo apt-get install build-essential cmake pkg-config libjpeg-dev libtiff5-dev libjasper-dev libpng-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libfontconfig1-dev libcairo2-dev libgdk-pixbuf2.0-dev libpango1.0-dev libgtk2.0-dev libgtk-3-dev libatlas-base-dev gfortran libhdf5-dev libhdf5-serial-dev libhdf5-103 python3-pyqt5 python3-dev -y
```

## Install OpenCV with pip
Finally, we can install OpenCV very simply using pip. Note that if you still have python2.7 on your system and you are not working with a virtual environment with python3, you will need to type in `pip3` rather than `pip`. The standard command to install opencv is `pip install opencv-contrib-python` but don't immediately run this (!) as it will try to install the latest versio of OpenCV, which is not always fully functional on the Raspberry Pi. Furthermore, the installation may take a very long time. Therefore I recommend to run the below command that installs the latest known working version. Here I use 4.5.3.56 but it could be that already a newer stable version is available:

```
pip install opencv-python==4.5.3.56
```

If you still get an error message such as *Could not find a version that satisfies the requirement opencv-contrib-python (from versions: ) No matching distribution found for opencv-contrib-python*, try the alternative to use `apt-get` instead of `pip`:

```
sudo apt-get install python-opencv
```

## Testing
Now let's just make sure that OpenCV is working. Open a terminal window and enter `python3` to start Python. Now to make sure you have installed OpenCV correctly enter:

```
import cv2
cv2.__version__
```

Your terminal window should look like:

```
$ python3
Python 3.7.3 (default, Dec 20 2020, 18:57:59)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2
>>> cv2.__version__
'4.5.3'
```
You are done!

## Errors?
It might be that you got an error along the way. Here are some solutions:

If you get an error message some prerequisites are not available using the command provided above try and remove them. Opencv is continuously being updated and its required prerequisites change and are sometimes removed.

If you get an error along the lines 'could not build wheels' it might be your wheels and setuptools are not fully up to date. To update them:

```
pip install --upgrade pip setuptools wheel
```

now try again.

If you have an issue with importing cv2 but the installation finished succesfully, try:

```
sudo apt-get install python-opencv
pip install -U numpy
```

If you have an issue running the latest version of opencv on Raspberry Pi, it can sometimes work to start python3 using the following command:
```
LD_PRELOAD=/usr/lib/arm-linux-gnueabihf/libatomic.so.1 python3
```

If you still have issues, please leave a commment!
