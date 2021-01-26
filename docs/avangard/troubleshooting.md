---
layout: page
permalink: /avangard/troubleshooting/
---

[<- Table of Contents](index.md)

## Troubleshooting
_**Please note that this wiki is under construction (UC). We're working on getting the most fundamental parts ready as soon as possible. We appreciate your support and understanding in this regard.**_

![](/assets/divider.png)

##### No camera connection
###### Create ssh tunnel to device
Click on edit device
+Add tunnel
Fill in:
type: ssh
name: ssh
host: localhost
port: 22
###### Open terminal to device
To browse to ssh tunnel edit same device again
Click link to ssh tunnel
####### Run commands
Try to discover camera:
```bash
sudo apt-get install -y avahi-utils
avahi-browse -rt _axis-video._tcp
```
