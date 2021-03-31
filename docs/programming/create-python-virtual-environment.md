---
layout: page
title: Python virtual environment
parent: Programming
nav_order: 2
permalink: /programming/create-python-virtual-environment
comments: true
---

# Create a Python virtual environment
{: .no_toc }

Virtual environments are a great way to stay organised with your Python libraries, which can be very helpful when testing custom scripts and packages and their dependencies.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Installing
First we need to install the virtual environments. To do so type in:

```
pip3 install virtualenv virtualenvwrapper
nano ~/.bashrc
```

Append the following lines to the bottom of the file:

```
#Virtualenvwrapper settings:
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_VIRTUALENV=~/.local/bin/virtualenv
source ~/.local/bin/virtualenvwrapper.sh
export VIRTUALENVWRAPPER_ENV_BIN_DIR=bin
```

Note that if you use an older version of Raspbian, virtualenvwrapper is installed in `/usr/local/bin/` instead so change lines 4 and 5 above accordingly. Now reload the file:

```
source ~/.bashrc
```

## Working with virtual environments
To create a virtual environment (e.g. named `main`):

```
mkvirtualenv main
```

Now to go and work inside the virtual environment, simply type:

```
workon main
```

and to exit again:

```
deactivate
```

To list all the Python packages in the virtual environment:

```
pip freeze
```
