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

## Install pip
Pip is the main package manager for python that we will also use to install OpenCV. Pip should already be installed on your system (see [here](https://pip.pypa.io/en/stable/installing/){:target="_blank"}), but if it's not, we can install it with wget. Open a Terminal window and enter:

```
wget https://bootstrap.pypa.io/get-pip.py
```

Now to install pip for Python 3 enter:

```
sudo python3 get-pip.py
```

## Install prerequisites
Next, for some versions of Raspberry Pi OS we may need to install some additional packages. First make sure `apt-get` is fully up-to-date by entering the following in Terminal:

```
sudo apt-get update
```

Now install the prerequisites:

```
sudo apt-get install build-essential cmake pkg-config libjpeg-dev libtiff5-dev libjasper-dev libpng-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libfontconfig1-dev libcairo2-dev libgdk-pixbuf2.0-dev libpango1.0-dev libgtk2.0-dev libgtk-3-dev libatlas-base-dev gfortran libhdf5-dev libhdf5-serial-dev libhdf5-103 libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5 python3-dev -y
```

## Install OpenCV with pip
Finally, we can enter install OpenCV very simply with the command:

```
pip install opencv-contrib-python
```

However, before running above command, it is important to note that the latest version of OpenCV may not always be fully functional on the Raspberry Pi. Therefore I recommend to run the below command that installs the latest known working version:

```
pip install opencv-contrib-python==4.1.0.25
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
'4.1.0'
```

You are done!

Note: an alternative to getting to run the latest version of opencv on Raspberry Pi is to run the following command rather than `python3`: `LD_PRELOAD=/usr/lib/arm-linux-gnueabihf/libatomic.so.1 python3`.

## Installing OpenCV on Windows
Coming soon
{: .label .label-yellow }
