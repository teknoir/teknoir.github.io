---
layout: page
permalink: /avangard/device-management/
---

[<- Table of Contents](index.md)

## Device management

_**Please note that this wiki is under construction (UC). We're working on getting the most fundamental parts ready as soon as possible. We appreciate your support and understanding in this regard.**_

![](/assets/divider.png)

##### Device naming scheme
What designates the device name

ccssXXXXX

cc - city short
ss - state short
XXXXX - incremental number

##### Labelling scheme
Labels in the form "key: value"

hardware
customer
city
state
production/dev/test
beta-program

##### QA Tasks - what to do before site installation
What to do prior on site install of a Sustayn device
Tasks before site installation

###### Insert SD card
Describe how device is identified, how to choose correct SD card, markings etc
How to open, and where to put it in
What to think about when closing it up again

###### Insert SIM?
How to open, and where to put it in
What to think about when closing it up again

###### Power up
Sequence or wiring etc to power up the Sustayn device

###### Login to the Teknoir Console
http://console.teknoir.cloud

###### Choose namespace
Has to match the SD card / device
avangard-production

###### Verify uplink
Browse to the device list and wait for the device to connect to the platform
Max 5 minutes
If rotating, it has never connected - double check name/marking of device/sd-card
If red hover to see when device was last seen + error
Green ok

###### Create tunnel to camera
Click on edit device
+Add tunnel
Fill in:
type: external
name: camera
host: 192.168.0.90
port: 80

###### Browse camera settings via tunnel
To browse to tunnel edit same device again
Click alternative link to camera tunnel

Credentials for camera:
username: root
password: pass

###### Edit camera settings
What do we need to change from default settings?
IR-auto -> disable?