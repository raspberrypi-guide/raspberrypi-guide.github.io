---
layout: page
title: Send slack notifications
parent: Programming
nav_order: 7
permalink: /programming/send-slack-notifications
comments: true
---

# Send notifications to slack
{: .no_toc }

Slack is a great messaging tool that is increasingly used by research groups and can  be used to send messages automatically from your Raspberry Pi, such as to send warnings based on sensor readings.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Setting-up Slack Webhooks
Incoming Webhooks are a great yet simple way to post messages from external sources to Slack using JSON payload. To do so, first make sure you have a slack workspace. Then in your workspace click on the `Apps +` icon to add a new application and search for `incoming webhook`. Click on `add`.

[![Slack](/assets/images/slack.jpg?style=centerimgmed)](/assets/images/slack.jpg)

You will now be redirected to the app directory page. Click here on the `Add to Slack` button to add the incoming WebHooks functionality. On the next page you have to provide a new configuration.

First select the channel from the dropdown where you wish to push the notification or click on `create a new channel`. In this example I chose to create a new channel called `#warnings`. Now click on `add incoming webhook integration` and copy the Webhook url provided.

## Sending a simple notification via Python
The most simple message would just contain a `text` property for the JSON payload. For example:

```
slack_message ={
"text": "Warning!.\nThe latest temperature reading in the lab was above treshold."}
```

Now to be able to send it via Python you can use the following simple script. Make sure you have the requests library installed (`pip3 install requests`).

```
import json
import requests

slack_webhook = '<yourwebhookurl'
slack_message = {
    "text": "Warning!.\nThe latest temperature reading in the lab was above treshold."
}
response = requests.post(
    slack_webhook, data=json.dumps(slack_message),
    headers={'Content-Type': 'application/json'}
)

if response.status_code != 200:
    raise ValueError(
        'Request to slack returned an error %s, the response is:\n%s'
        % (response.status_code, response.text)
    )
```

## Using a Python function to send slack notifications
It is better to write a separate function to send slack messages that asks for the webhook url. We can then also integrate a statement that integrates an function input value, such as the type of sensor for which there is an error.

To further improve the formatting of the message we add it as an attachment and create a bold title with an emoji. For more options, such as text formatting or to mention specific users or channels, see the [documentation](https://api.slack.com/reference/surfaces/formatting){:target="_blank"}.

[![slack message](/assets/images/slack-message.png?style=centerimgmed)](/assets/images/slack-message.png)

With the above additions our slack function becomes:

```
def SlackAlert(slack_webhook, sensortype):
    alert_title = ':bulb: *Lab warning!*'
    alert_message = '{} was outside the user-specified range!'.format(sensortype)
    alert_attachment = [
		{
			'color': 'danger',
            'fallback': alert_message,
			'text': alert_message,
		}
	]
    slack_message = {
        'username': 'fishpi',
        'icon_emoji': ':fish:',
        'channel': '#warnings',
        'text': alert_title,
        'attachments': alert_attachment
	}

    response = requests.post(
        slack_webhook, data=json.dumps(slack_message),
        headers={'Content-Type': 'application/json'}
    )

    if response.status_code != 200:
        raise ValueError(
            'Request to slack returned an error %s, the response is:\n%s'
            % (response.status_code, response.text)
        )
```
