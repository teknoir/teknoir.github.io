---
title: Device is offline
layout: single
toc: true
categories:
  - troubleshooting
tags:
  - troubleshooting-devices
  - troubleshooting
---

## Device is offline
If the device does not go green in the console there is not much we can do remotely.
Follow the guides below to do local assessment of the situation.

**Note:** This means that you must have physical access or at least a working local network connection to
the device.
{: .notice--warning}

### Login on offline device
If you need to login on an offline device.

**Get credentials**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on the device name

**Note:** On this page you can see the username and password, the credentials, you need to use to connect or login to 
your device.
{: .notice--info}

#### Add keyboard and monitor
The by far most robust way is to add keyboard and monitor to the device and you should be able to login with the device
credentials.

#### Use secure shell (ssh)
The next step is to connect to the device with secure shell(ssh).

```bash
ssh <username>@<device name>.local
```

**Note:** First of all, this command only works if you have a *nix environment. Second the device has to be on your 
local network and mDNS has to work on that network.
{: .notice--info}

### Network connectivity
If the device cannot connect to/through a network that is connected to internet it will work offline.
Offline mode and offline maintenance is not yet built out. For now this is not a mode we support.

If the device is supposed to be online please check the following.

#### Ethernet
1. Check cables
2. TBD

#### Wifi
1. Check that SSID and credentials match
2. TBD

#### Other
If the device is connected with GSM, LTE, 5G or other method please make sure the Linux network interface is given a valid IP.
Try to verify internet connectivity with for example curl.

