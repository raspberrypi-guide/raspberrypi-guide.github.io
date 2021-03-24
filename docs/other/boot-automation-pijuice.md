---
layout: default
title: Boot automation with the PiJuice
parent: Other
nav_order: 3
---

# Automate your Raspberry Pi with PiJuice
{: .no_toc }

The PiJuice is a power management HAT that brings a lot of helpful tools to your Raspberry Pi. Here I provide a guide to program your Raspberry Pi to turn on and off automatically, run a script, and write a logfile.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta .fs-4 .fw-300 }

1. TOC
{:toc}
---

## Power management
The Raspberry Pi has no native power management program that enables power supply monitoring and automatisation. This means that when the supplied DC power is too low, such as with unreliable power sources, or power drops completely, the Raspberry Pi will turn off abruptly, with the risk of losing data and corrupting the SD card.

[![PiJuice](/assets/images/pijuice-hat.jpg?style=centerimgmed)](/assets/images/pijuice-hat.jpg)

A number of HATs exist, such as the [PiJuice](https://uk.pi-supply.com/collections/pijuice), that provide power management tools for the Raspberry Pi. These HATs can augment the DC power supply from a battery such that fluctuating DC power sources, such as from a connected solar panel, can be utilised effectively. They can also help create an Uninterrupted Power Supply (UPS), such that in the case of a power outage it will automatically switch to battery input.

A key added benefit of power management HATs is that they tend to enable intelligent wake-up modes and the automated initiation of user-defined scripts, which, in combination with the true low power deep sleep state (< 1mA), can help to considerably reduce power consumption, which is our aim here.

## Project overview
For this particular example, we will use the PiJuice to automatically turn on the Raspberry Pi, run a script, write a statement to a status log, and turn off the Raspberry Pi again after three minutes. Furthermore, we want that, if the Raspberry Pi is battery-powered the Raspberry pi turns off directly. And that the Raspberry Pi automatically turns on every 10min.

## Add print statements at boot and shutdown
We want to log each time the raspberry pi boots and turns off. For this we will write simple Python scripts and then edit the startup and shutdown services. Follow the guide [here](http://) how to write the logfiles, and for this example we will use the file `/home/pi/pistatus.log` as an example.

## Set up the PiJuice
Next connect your PiJuice to the Raspberry Pi via the GPIO pins and download the PiJuice software:

```
sudo apt-get install pijuice-gui
```

[![PiJuice GUI](/assets/images/pijuice-GUI.jpg?style=centerimgmed)](/assets/images/pijuice-GUI.jpg).

A lot of detailed information on how to use the GUI can be found on the [PiJuice Github page](https://github.com/PiSupply/PiJuice/tree/master/Software). Here I focus on some of the most important functions.

## Turning the Raspberry Pi on and off automatically
With PiJuice we can easily schedule the Raspberry Pi to turn on automatically according to a time schedule. Go to `PiJuice Settings` > `Wakeup Alarm` and choose your desired schedule. As a test example, let's have the Raspberry Pi start every 10min.

Click the boxes next to `Every day` and `Every hour`, click `Minutes period` below and type in `10`. Now make sure `Wakeup enabled` is ticked, click `Set Alarm`, and finally click `Apply`.

[![PiJuice wakeup](/assets/images/pijuic-wakeup.jpg?style=centerimgmed)](/assets/images/pijuic-wakeup.jg
	g).

With PiJuice there is no option to turn off the Raspberry Pi automatically, but we can set a timer and run a (Python) script to turn off the Raspberry Pi automatically after a set time, for example 3 minutes. We  also want to keep the Raspberry Pi running when it is not on Battery power.

Let's create a new Python script:

```
nano /home/pi/runandturnoff.py
```

Now add the code:

```
#!/usr/bin/python3

import os
import logging
from time import sleep
from pijuice import PiJuice

logging.basicConfig(
	filename = '/home/pi/pistatus.log',
	level = logging.DEBUG,
	format = '%(asctime)s %(message)s',
	datefmt = '%d/%m/%Y %H:%M:%S')

pj = PiJuice(1,0x14)

pjOK = False
while pjOK == False:
   stat = pj.status.GetStatus()
   if stat['error'] == 'NO_ERROR':
      pjOK = True
   else:
      sleep(0.1)

# If on battery power, shut down after 3min
data = stat['data']
if data['powerInput'] == "NOT_PRESENT" and data['powerInput5vIo'] == 'NOT_PRESENT':

	# Write statement to log
	logging.info('Raspberry Pi on battery power. Turning off in 3min')

   # Keep Raspberry Pi running
   sleep(180)

   # Make sure wakeup_enabled and wakeup_on_charge have the correct values
   pj.rtcAlarm.SetWakeupEnabled(True)
   pj.power.SetWakeUpOnCharge(0)

   # Make sure power to the Raspberry Pi is stopped to not deplete
   # the battery
   pj.power.SetSystemPowerSwitch(0)
   pj.power.SetPowerOff(30)

   # Now turn off the system
   os.system("sudo shutdown -h now")

else:

	# Write statement to log
	logging.info('Raspberry Pi on mains power, not turned off automatically')
```

Now make the file executable:

```
chmod +x /home/pi/runandturnoff.py
```

and add it to the startup service:

```
sudo nano /etc/rc.local
```

and just before the line `exit 0` add the following:

```
python3 /home/pi/runandturnoff.py &
```

Let's test it! Turn off your Raspberry Pi. After 30sec its red light should turn off, indicating it does not receive any more power. After some time, it should automatically turn on again, at every 10min past the hour (e.g. 17:10, 17:20 etc), and then turn off again after 3min when only on battery power.

## Turn off Raspberry Pi when battery too low
When the Raspberry Pi is powered by a battery and the energy is running low, it is best to turn it off and save power. To do this, create a Python file called `myshutdown.py`:

```
nano /home/pi/myshutdown.py
```

And add the following code:

```
#!/usr/bin/python3

import os
import logging
from pijuice import PiJuice

logging.basicConfig(
	filename = '/home/pi/pistatus.log',
	level = logging.DEBUG,
	format = '%(asctime)s %(message)s',
	datefmt = '%d/%m/%Y %H:%M:%S')

pj = PiJuice(1,0x14)

# Set wakeup_enabled and wakeup_on_charge just to be sure
pj.rtcAlarm.SetWakeupEnabled(True)

# The Raspberry Pi should wake up even when there is no battery, i.e. a
# battery percentage of 0
pj.power.SetWakeUpOnCharge(0)

# Write statement to log
logging.info('Raspberry Pi battery running low')

# Show custom script is run by blinking the user LED red 10x
pj.status.SetLedBlink('D2', 10, [200,0,0], 50, [0, 0, 0], 50)

# Now shut down
os.system("sudo shutdown -h now")
```

Now make the file executable:

```
chmod +x /home/pi/myshutdown.py
```

Note that we added the line `pj.rtcAlarm.SetWakeupEnabled(True)` because when setting the Wakeup alarm for repeated wakeup, the Wakeup enabled capability is disabled due to the Raspbian RTC clock initialisation resetting the PiJuice firmware.

Also the Raspberry Pi should wake up even when there is no battery, therefore we added the line `pj.power.SetWakeUpOnCharge(0)`.

Finally, we also blink the LED to show what is happening using the command `pijuice.status.SetLedBlink('D2', 10, [200,0,0], 50, [0, 0, 0], 50)`.

Now go to `PiJuice Settings` > `System Task` and select `[x] Minimum charge` and choose a treshold, e.g. 10%. Now go to `System Events` and click the `Low charge` option and select `USER_FUNC1`. Now on the `User Scripts` tab, define `USER_FUNC1` as `/home/pi/myshutdown.py`.

Now when your battery drops below 10%, it will log this to our pistatus.log, blink the leds, and turn off automatically.

That's it!
