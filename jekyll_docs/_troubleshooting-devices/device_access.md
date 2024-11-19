---
title: Device access
layout: single
toc: true
categories:
  - troubleshooting
tags:
  - troubleshooting-devices
  - troubleshooting
---

## Device access
If the device does not go green in the console there is not much we can do remotely.
Follow the guides below to do local assessment of the situation.

**Note:** This means that you must have physical access or at least a working local network connection to
the device.
{: .notice--warning}

### Login on offline device
If you need to login on an offline device.

**Get credentials**
1. Browse to [devices](https://teknoir.cloud/_/devices/)
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

### Login on online devices

#### SSH tunnel

**Create ssh tunnel to device**
1. Browse to [devices](https://teknoir.cloud/_/devices/)
2. Choose namespace
3. Click on the device name
4. Enable tunneling, and if there is no ssh tunnel already click `+ Add`, to add a ssh tunnel
5. Fill in:
    * type: ssh
    * name: ssh
    * target: localhost
    * port: 22

**Note:** Each time tunneling is enabled it can take up to 5 minutes for tunnels to be available. This 
is due to the security settings and certifictates being propagated to the different services.
{: .notice--info}

**Open web terminal to device**
1. To browse to ssh tunnel edit same device again
2. Click link to ssh tunnel
3. Run commands

Example:
```bash
sudo kubectl get pods
```

**Note:** On the device page you can see the username and password, the credentials, you need to use to elevate 
permissions in linux.
{: .notice--info}

### Escalating permissions
For some commands you need to be root, to become root:

```bash
sudo su
```

And then use the user password for the user you logged in with.
It can be found on the device page in our platform.