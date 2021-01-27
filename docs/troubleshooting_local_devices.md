---
title: Troubleshooting Local Devices
layout: page
permalink: /troubleshooting-local-devices/
---

[<- Table of Contents](/)

_**Please note that this wiki is under construction (UC). We're working on getting the most fundamental parts ready as soon as possible. We appreciate your support and understanding in this regard.**_

---

## Topics
* [Device is offline](#device-is-offline)
  * [Login on offline device](#login-on-offline-device)
  * [Network connectivity](#network-connectivity)

## Device is offline
If the device does not go green in the console there is not much we can do remotely.
Follow the guides below to do local assessment of the situation.

### Login on offline device
If you need to login on an offline device.

**Get credentials**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on edit the device (the pen icon)

> On this page you can see username and password to your device.

**Connect through Wifi**
1. TBD

**Connect through Ethernet**
1. TBD

**Add keyboard and monitor**
1. TBD

### Network connectivity
If the device cannot connect to/through a network that is connected to internet it will work offline.
Offline mode and offline maintenance is not yet built out. For now this is not a mode we support.

If the device is supposed to be online please check the following.

**Ethernet**
1. Check cables
2. TBD

**Wifi**
1. TBD

**Other**<br>
If the device is connected with GSM, LTE, 5G or other method please make sure the Linux network interface is given a valid IP.
Try to verify internet connectivity with for example curl.

