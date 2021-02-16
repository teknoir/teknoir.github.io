---
title: Device management
layout: page
permalink: /avangard/device-management/
---

[<- Table of Contents](index.md)

_**Please note that this wiki is under construction (UC). We're working on getting the most fundamental parts ready as soon as possible. We appreciate your support and understanding in this regard.**_

---
## Topics
* TBD

## What to do before site installation
What to do prior on site install of a Sustayn device

### Insert SD card
Describe how device is identified, how to choose correct SD card, markings etc
How to open, and where to put it in
What to think about when closing it up again

### Insert SIM?
How to open, and where to put it in
What to think about when closing it up again

### Power up
Sequence or wiring etc to power up the Sustayn device

#### Set up maintenance Wifi
The device can start up on the SIM-cards data plan but to minimize the usage a maintenance Wifi can be set up before it
is powered up.

> The devices use the same Wifi credentials.

**Find Wifi credentials**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on edit the device (the pen icon)
4. The credentials can be found in the Wifi section

> Please refer to the Wifi router documentation on how to set up WPA2 PSK Wifi.

> Due to technical limitations at the time of creation the first 81 devices does not have this feature.

The device will not automatically jump to the maintenance Wifi, it will only connect to it if restarted/rebooted.

### Login to the Teknoir Console
http://console.teknoir.cloud

#### Choose namespace
Has to match the SD card / device
avangard-production

#### Verify uplink
Browse to the device list and wait for the device to connect to the platform
Max 5 minutes
If rotating, it has never connected - double check name/marking of device/sd-card
If red hover to see when device was last seen + error
Green ok

#### Create tunnel to camera
To be able to see where the camera is pointing, picture quality and edit settings, a tunnel can be created.

**Create http tunnel to camera**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on edit the device (the pen icon)
4. Enable tunneling, and if there is no camera tunnel already click `+ Add`, to add a camera tunnel
5. Fill in:
    * type: external
    * name: camera
    * host: <IP to camera, default is 192.168.0.90>
    * port: 80

> Remember, that if the camera is on LTE data plan, you might have to be quick about it. The camera streaming video
> will consume a lot of data.

> Consider creating a maintenance Wifi before doing this.

#### Browse camera settings via tunnel
To browse to tunnel edit same device again
Click alternative link to camera tunnel

> Credentials for camera is username: **root** and password: **pass**

##### Edit camera settings
What do we need to change from default settings?
IR-auto -> disable?
Focus settings?

## Device naming scheme
What designates the device name

ccssXXXXX

cc - city short
ss - state short
XXXXX - incremental number

## Labelling scheme
Labels in the form "key: value"

hardware
customer
city
state
production/dev/test
beta-program