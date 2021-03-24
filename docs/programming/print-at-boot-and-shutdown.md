---
layout: page
title: Print at boot/shutdown
parent: Programming
nav_order: 4
permalink: /programming/print-at-boot-and-shutdown
---

# Print statements at boot and shut-down
{: .no_toc }

For some use cases it may be very handy to have a concise log file with all the times when your Raspberry Pi booted up and shut down. Here we will write two simple Python scripts and run them using boot and shutdown services.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Add print statement at boot
Create the file `printatboot.py` with the following code:

```
#!/usr/bin/python3

import logging

logging.basicConfig(
	filename = '/home/pi/pistatus.log',
	level = logging.DEBUG,
	format = '%(asctime)s %(message)s',
	datefmt = '%d/%m/%Y %H:%M:%S')

logging.info('Raspberry Pi power on')
```

Now make the file run automatically at boot:

```
sudo nano /etc/rc.local
```

Add the following just before the `exit 0` statement:

```
python3 /home/pi/printatboot.py &
```

## Add print statement at shutdown
Now similarly for shutdown, create the file `printatshutdown.py`:

```
#!/usr/bin/python3

import logging

logging.basicConfig(
	filename = '/home/pi/pistatus.log',
	level = logging.DEBUG,
	format = '%(asctime)s %(message)s',
	datefmt = '%d/%m/%Y %H:%M:%S')

logging.info('Raspberry Pi power off')
```

We now have to create a system shutdown service as there doesn't exist one yet like the startup service of rc.local:

```
sudo nano /etc/systemd/system/rcshutdown.service
```

Add the text:

```
[Unit]
Description=/etc/rc.shutdown
Before=shutdown.target

[Service]
ExecStart=/bin/true
ExecStop=/etc/rc.shutdown
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Now enable the service:

```
sudo systemctl enable rcshutdown.service
```

and create the file `/etc/rc.shutdown`, which will be similar like the `/etc/rc.local` file:

```
sudo nano /etc/rc.shutdown
```

Add the following text:

```
#!/bin/bash
#
# rc.shutdown
#

python3 /home/pi/printatshutdown.py

exit 0
```

Now make the script executable:

```
sudo chmod a+x /etc/rc.shutdown
```

## Testing
Ttart the shutdown service for the first boot (it should run automatically from next boot):

```
sudo systemctl start rcshut.service
```

and reboot your Raspberry Pi:

```
sudo shutdown -r now
```

After booting up, check the status log:

```
nano /home/pi/pistatus.log
```

It should look like the following:

```
10/02/2021 11:13:19 Raspberry Pi power on
10/02/2021 11:13:49 Raspberry Pi power off
```
