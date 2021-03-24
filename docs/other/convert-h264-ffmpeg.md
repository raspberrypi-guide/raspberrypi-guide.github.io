---
layout: page
title: Convert .h264 videos with ffmpeg
parent: Other
nav_order: 9
---

# Installing FFmpeg on a Raspberry Pi with .h264 support
{: .no_toc }

FFMpeg is a great and highly versatile utility for converting image and video from the command line. Follow the below steps to learn how to install and use FFMpeg.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## FFmpeg
The Raspberry Pi is great for recording images and video. One issue is that it records videos in the compressed `.h264` container, which is hard to work with. In many cases it is desirable to convert videos to widely applicable formats like `.mp4` to be able to view them properly and get the right meta information. For this I recommend the program `FFmpeg`.

[ffmpeg](https://www.ffmpeg.org/ffmpeg.html) is a very fast video and audio converter that can also grab from a live audio/video source. Installing FFmpeg on a Raspberry Pi is not as simple as downloading an executable from the command line, but it is also not too difficult.

## Install h264 library
Open a terminal window on the Raspberry Pi (or via SSH connection). First we will download the h264 library:
```
git clone --depth 1 https://code.videolan.org/videolan/x264
```

Now change to the x264 folder:

```
cd x264
```

and configure installation the installation as follows:

```
./configure --host=arm-unknown-linux-gnueabi --enable-static --disable-opencl
```

We can now create the installation (for four cores):

```
make -j4
```

And finally we can install the h264 library on the system:

```
sudo make install
```

## Install ffmpeg with h264
Now we will install FFmpeg. First change to the home directory:

```
cd ~
```

Now download ffmpeg:

```
git clone git://source.ffmpeg.org/ffmpeg --depth=1
```

Change to the ffmpeg directory:

```
cd ffmpeg
```

Configure the installation:

```
./configure --extra-ldflags="-latomic" --arch=armel --target-os=linux --enable-gpl --enable-omx --enable-omx-rpi --enable-libx264 --enable-nonfree
```

Create the installation for four cores:

```
make -j4
```
*Note this step may take a long time!* And now finally run the installation:

```
sudo make install
```

There are many options available and other ways to convert h264 videos with ffmpeg, but the above commands are the quickest of the methods that I tested.

Note: If you are working with an older model of the raspberrypi (&lt; 3 B+) then you may not have 4 cores available. You will then have to change `make -j4` to `make -j`.

## Converting (h264) videos
Now you are ready to convert (h264) videos on your Raspberry Pi. To convert a single video with ffmpeg:

```
ffmpeg -i USER_VIDEO.h264 -vcodec copy USER_VIDEO.mp4
```

It is a bit more tricky to (automatically) convert whole folders of videos. I have written a special `Convert` functionality as part of my [pirecorder](https://github.com/JolleJolles/pirecorder) package to facilitate this. For example, to convert a folder of videos, add frame numbers to the topleft corner of each video frame, and resize the video by half:

```
convert --indir VIDEOS --outdir CONVERTED --withframe True --resizeval 0.5
```

You can read its documentation [here](https://github.com/JolleJolles/pirecorder/wiki/pirecorder-convert/).
