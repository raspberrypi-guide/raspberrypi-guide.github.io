---
layout: page
title: Installing Jekyll webserver
parent: Other
nav_order: 4
permalink: /other/installing-jekyll-webserver
comments: true
---

# Install Jekyll on a Raspberry Pi
{: .no_toc }

Set up your Raspberry Pi to host a static website using Jekyll, the same software used to run this website!
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## What is Jekyll
There are many ways to host a website on your Raspberry Pi, of which I think Jekyll ([jekyllrb.com](https://jekyllrb.com/){:target="_blank"}) is one of the best solutions. Jekyll is a static site generator that specifically helps to render Markdown and template files into a complete static website. Jekyll was also used to create this website, hosted from a Github repository using [Github Pages](https://pages.github.com/){:target="_blank"}.

## Installing Jekyll
First we will install Ruby, which is a package manager that we use to install jekyll:

```
sudo apt-get update
sudo apt-get install software-properties-common -y
sudo apt-get install ruby-full -y
```

Next, to install jekyll, use the following commands:

```
sudo gem install jekyll
sudo gem install bundler
```

Now navigate to the folder where you want your website (folder) to reside, e.g.:

```
mkdir /home/pi/websites
cd /home/pi/websites
```

Run the following command to set up a new jekyll website:

```
jekyll new websitename
```

A new folder with the name you provided will be created with all the basic files you will need for your website.

## Running and updating the website
To run the wesbite, navigate into its folder, e.g.:

```
cd websitename
```

Now to serve the website at [http://localhost:4000](http://localhost:4000){:target="_blank"}, enter:

```
bundler exec jekyll serve 2>/dev/null
```

This will continuously update your website while you edit files. Read more about how to create a jekyll website [here](https://jekyllrb.com/){:target="_blank"}.

Your website will be hosted locally but with some extra steps it is also possible to serve the website to the broader internet, such as by using [ngrok](https://ngrok.com/){:target="_blank"}.
