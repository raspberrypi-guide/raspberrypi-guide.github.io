---
layout: page
title: Send text messages
parent: Programming
nav_order: 6
permalink: /programming/send-sms-messages
comments: true
---

# Sending a text message (SMS) with your Raspberry Pi
{: .no_toc }

Using Twilio we can use our Raspberry Pi to send text messages to any phone number. Follow the below steps to get started!
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## What is Twilio
[Twilio](https://www.twilio.com){:target="_blank"} is a communications platform designed to link and engage with users from a number of different platforms such as Email, SMS, WhatsApp, Voice and many more. It allows users to create their own applications using a number of different programming language and provided examples. Here we will use it to send SMS messages.

Twilio is a paid platform, but initial sign up under the free Trial will give you credit of $15.50 to send and receive messages, which will cost less than a cent. Thereafter you can use a pay-as-you-go service to top up your credit.

## Create a Twilio Account
Head over to [twilio.com/try-twilio](https://www.twilio.com/try-twilio){:target="_blank"} to sign up for a free trial account. You will need to verify your email address and personal phone number for security measures. You will also see the pre-loaded balance in the Dashboard to test out some of Twilio’s functionality. You will not be charged for Twilio phone numbers until you upgrade your account.

Now to be able to send text message, you will need a register a phone number in your account. To do so, go to [twilio.com/console/phone-numbers/incoming](https://www.twilio.com/console/phone-numbers/incoming){:target="_blank"}.

## Install Twilio
To install Twilio on the Raspberry Pi simply open up a terminal window and type the following command:

```
sudo pip3 install twilio
```

## Using Twilio
Now to use Twilio, First get your account SID and Auth token from [twilio.com/console](https://www.twilio.com/console){:target="_blank"} and then open a new file:

```
nano sendsms.py
```

and add the following code:

```
from twilio.rest import Client

TWILIO_ACCOUNT_SID = 'XXXX' # replace with your Account SID
TWILIO_AUTH_TOKEN = 'YYYY' # replace with your Auth Token
TWILIO_PHONE_SENDER = "99999999" # replace with the phone number you registered in twilio
TWILIO_PHONE_RECIPIENT = "000000" # replace with your phone number

def send_text_alert(alert_str):
    """Sends an SMS text alert."""
    client = Client(TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN)
    message = client.messages.create(
        to=TWILIO_PHONE_RECIPIENT,
        from_=TWILIO_PHONE_SENDER,
        body="Your text message here")
    print(message.sid)
```

To exit press `ctrl+x`, then `y`, and `Enter`.

Note that messages sent in trial will begin with *Sent from a Twilio Trial Account*. I think this is fine for testing and perhaps does not matter for most use cases, but if you don't want this, simply get a paid account.

## Use hidden credentials
Using the above script we hardcode the credentials. This is fine to get started but not very safe. A much better option is to use environment variables to keep them secret before deploying to production.

Follow my general guide [here](../networking/raspberry-pi-security.html) and then adapt your Python script above to use the following code:

```
import os
TWILIO_ACCOUNT_SID = os.environ['TWILIO_ACCOUNT_SID']
TWILIO_AUTH_TOKEN = os.environ['TWILIO_AUTH_TOKEN']
```

That's it! Save your script and run it with `python sendsms.py` and you should receive your first text in seconds.
