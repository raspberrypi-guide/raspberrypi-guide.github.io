---
layout: default
title: Send email notifications
parent: Programming
nav_order: 5
permalink: /programming/send-email-notifications
---

# Sending automatic email from your Raspberry Pi
{: .no_toc }

Using the Raspberry Pi it is quite easy to send automatic emails, such as warning messages or notifications. While there are various ways to do this, I suggest to use the Yagmail library and Python.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Create Gmail account
First create a new (throw-away) gmail account and remember the username and password. Turn on less secure app access in this gmail account by going to [https://myaccount.google.com/](https://myaccount.google.com/), click *Security*, scroll down to *Less Secure App Access* and toggle *On*. A more secure way is to use OAuth2 in combination with Google’s API console. You can find a guide how to do that [here](https://blog.macuyiko.com/post/2016/how-to-send-html-mails-with-oauth2-and-gmail-in-python.html).

## Install software
Next we are going to install the Yagmail Python package. It builds on the possibility to use the Operating System's keychain, so we will install a corresponding package for that as well, and let it automatically install a backend:

```
pip install yagmail
pip install keyring
pip install keyrings.alt
```

## Sending an email from Python
Okay now we are ready to send an email from Python with very straightforward code:

```
import yagmail

# start a connection
yag = yagmail.SMTP("your_gmail_username")

# define the variables
to = "recipient_email_address"
subject = "A message from your Raspberry Pi!"
body = "This is an automated message"

# send the email
yag.send(to, subject, body)
print("Email sent!")
```

When running the script for the first time, you will be prompted for the email password. Upon entering this once, it will be stored in the keyring and not asked again. You should receive your first email within the next seconds!

As a next step you could wrap the code in a function and implement it with other functions that for example read sensors or check folders and thereby send automatic emails with subject and contents adjusted based on the events. Another great way is to use [cron jobs](https://www.raspberrypi.org/documentation/linux/usage/cron.md) to send emails at scheduled intervals.  
