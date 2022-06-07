---
title: Device management
permalink: /partners/avangard-innovative/device-management/
toc: true
sidebar:
  nav: "avangard-innovative"
tags:
  - avangard-innovative
---

## What to do before site installation
What to do prior on site install of a Sustayn device. A sort of QA testing before putting it in the field.

### Insert SD card
Describe how device is identified, how to choose correct SD card, markings etc
How to open, and where to put it in
What to think about when closing it up again

### Insert SIM?
How to open, and where to put it in
What to think about when closing it up again

### Power up
Sequence or wiring etc to power up the Sustayn device

Before actually powering it up please reed this full section, to make sure you are ready to power up the device.

#### Set up maintenance Wifi
The device can start up on the SIM-cards data plan but to minimize the usage a maintenance Wifi can be set up before it
is powered up.

**Note:** All devices use the same Wifi credentials.
{: .notice--info}

**Find Wifi credentials**
1. Browse to [devices](https://teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on edit the device (the pen icon)
4. The credentials can be found in the Wifi section

> Please refer to the Wifi router documentation on how to set up WPA2 PSK Wifi.

**Note:** Due to technical limitations at the time of device creation some of the first 81 devices does not have this feature.

The device will not automatically jump to the maintenance Wifi, it will only connect to it if restarted/rebooted.

### Login to the Teknoir Console
http://teknoir.cloud

#### Choose namespace
Has to match the SD card / device
avangard-production

#### Verify uplink
Browse to the device list and wait for the device to connect to the platform
Max 5 minutes
If rotating, it has never connected - double check name/marking of device/sd-card
If red hover to see when device was last seen + error
Green ok

**Note:** A good idea is, once done with configuration, turn off the maintenance Wifi and perform this uplink 
verification again, just to make sure the LTE setup is ok
{: .notice--warning}

#### Create tunnel to camera
To be able to see where the camera is pointing, picture quality and edit settings, a tunnel can be created.

**Create http tunnel to camera**
1. Browse to [devices](https://teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on edit the device (the pen icon)
4. Enable tunneling, and if there is no camera tunnel already click `+ Add`, to add a camera tunnel
5. Fill in:
    * type: external
    * name: camera
    * host: <IP to camera, default is 192.168.0.90>
    * port: 80

**Note:** Remember, that if the camera is on LTE data plan, you might have to be quick about it. The camera streaming video
will consume a lot of data. Consider creating a maintenance Wifi before doing this.
{: .notice--warning}

#### Browse camera settings via tunnel
To browse to tunnel edit same device again
Click alternative link to camera tunnel

**Note:** Default credentials for Axis camera is username: **root** and password: **pass**, the Bosch camera will make 
you set it first time.
{: .notice--info}
