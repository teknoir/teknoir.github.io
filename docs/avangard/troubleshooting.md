---
title: Troubleshooting
layout: page
permalink: /avangard/troubleshooting/
---

[<- Table of Contents](index.md)

_**Please note that this wiki is under construction (UC). We're working on getting the most fundamental parts ready as soon as possible. We appreciate your support and understanding in this regard.**_

---
## Topics
* [Device is lost](#device-is-lost)
* [Missing SD-card](#missing-sd-card)
* [Camera issues](#camera-issues)
  * [Use Devstudio on the device](#use-devstudio-on-the-device)
  * [Check camera app logs](#check-camera-app-logs)
  * [Check camera IP with service discovery](#check-camera-ip-with-service-discovery)
  * [Change settings wia camera webgui](#change-settings-wia-camera-webgui)

## Device is lost
Normally the device have a self healing behavior. That means it will try to re-connect to the platform
by restarting different subsystems ontrolled by a self healing algorithm.

Reasons it might not connect:
* Data plan quota exceeded

Hardware sometimes break, and in that case it is easy to prepare and test an exchange unit.
Just note the name of the device, follow the steps in [Missing SD-card](#missing-sd-card) section.

## Missing SD-card
If a SD-card is missing it is easy to create a new.

1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Find the device that is missing its SD-card
4. Continue to follow the instructions [here](https://teknoir.github.io/add-new-device/#flash-the-image-to-an-sd-card)

## Camera issues
If you notice that there are no images being received from a device, there are ways to investigate this.

### Use Devstudio on the device
Connect to the Devstudio running on the device to see if images are picked up there.

**Create http tunnel to device**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on the device name
4. Enable tunneling, and if there is no devstudio tunnel already click `+ Add`, to add a devstudio tunnel
5. Fill in:
    * type: internal http
    * name: devstudio
    * target: devstudio
    * port: 1880

**Open Devstudio running on the device**
1. To browse to ssh tunnel edit same device again
2. Click link to devstudio tunnel
3. Debug data coming from camera

> If the camera is working, you should be abe to display images coming from the camera in the Devstudio.

### Check camera app logs
To see if the camera app works correctly you need to run some commands on the device.

**Create ssh tunnel to device**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on the device name
4. Enable tunneling, and if there is no ssh tunnel already click `+ Add`, to add a ssh tunnel
5. Fill in:
    * type: ssh
    * name: ssh
    * target: localhost
    * port: 22

**Open web terminal to device**
1. To browse to ssh tunnel edit same device again
2. Click link to ssh tunnel
3. Run commands

Check if the camera service is running:
```bash
sudo kubectl get pods
```

> If the camera app works STATUS should be Running.

Read the logs to see if you can se any issues there:
```bash
sudo kubectl logs -f $(sudo kubectl get pods -l app=camera -o name)
```

> There should not be any errors in the log and the camera app should publish messages each interval.

### Check camera IP with service discovery
I you think the camera might be missconfigured, you can try to see if it is discoverable.

**Create ssh tunnel to device**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on the device name
4. Enable tunneling, and if there is no ssh tunnel already click `+ Add`, to add a ssh tunnel
5. Fill in:
   * type: ssh
   * name: ssh
   * target: localhost
   * port: 22

**Open web terminal to device**
1. To browse to ssh tunnel edit same device again
2. Click link to ssh tunnel
3. Run commands

Install tools to discover camera:
```bash
sudo apt-get install -y avahi-utils
```

Try to discover camera:
```bash
avahi-browse -rt _axis-video._tcp
```

> If the camera is on the same network, and functional, you should se the IP address to the camera in the terminal.

### Change settings wia camera webgui
If you need to change settings on the camera, you can do that via an external tunnel via the device.

**Create http tunnel to camera**
1. Browse to [devices](https://console.teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on the device name
4. Enable tunneling, and if there is no camera tunnel already click `+ Add`, to add a camera tunnel
5. Fill in:
    * type: external http
    * name: camera
    * target: <IP to camera, default is 192.168.0.90>
    * port: 80

**Open the camera webgui**
1. To browse to http tunnel edit same device again
2. Click link to the **alternative** link to the camera tunnel
3. Default user/password is root/pass
4. Edit camera settings

> Remember you have to use the alternative tunnel link, the camera cannot handle X-Forwarded-* headers.

