---
title: Device networking
layout: single
toc: true
categories:
  - troubleshooting
tags:
  - troubleshooting-devices
  - troubleshooting
---

## Device networking
If the device cannot connect to/through a network that is connected to internet it will work offline, but it cannot 
connect to the Tenknoir platform.

You can check if the device has internet connection with the command ping:

```bash
ping 1.1.1.1
```

If the device has a working internet connection it should say something like this and continue until you press ctrl+c.
```bash
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=56 time=11.5 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=56 time=6.60 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=56 time=6.42 ms
...
```

**Note:** Offline mode and offline maintenance is not yet built out. For now this is not a mode we support.
{: .notice--info}

If the device is supposed to be online please check the following.

#### Ethernet
Check the ethernet cables! Check if eth0 interface exists and has an IP address:

```bash
ifconfig
```

Check status by running the network manager command line interface(nmcli) command:

```bash
nmcli dev show eth0
```

#### Wifi
Check that SSID and credentials match

Check if wlan0 interface exists and has an IP address:

```bash
ifconfig
```

Or check if wifi is up, run:

```bash
nmcli dev
```

If the wifi seems up and connected run:

```bash
nmcli dev wifi show-password
```

If wifi is down, run:

```bash
grep ssid= /etc/NetworkManager/system-connections/*
/etc/NetworkManager/system-connections/wifi.nmconnection:ssid=<check the SSID here>
grep psk= /etc/NetworkManager/system-connections/*
/etc/NetworkManager/system-connections/wifi.nmconnection:psk=<check the password here>
```

More wificommands can be found [here](https://connectwww.com/nmcli-view-your-network-wifi-details-and-control-your-networkmanager/61731/)


#### Modem
If the device is connected with GSM, LTE, 5G or other method please make sure the Linux network interface is given a valid IP.
Try to verify internet connectivity with for example curl.

Check if wwan0(in most cases but it could be different for your modem) interface exists and has an IP address:

```bash
ifconfig
```

To check modem status, run the modem manager command line interface(mmcli) command:

```bash
mmcli -m 0
```

Set verbose loggin on modem status (see log section on how to read logs):

```bash
mmcli --set-logging=INFO
```


Check modem LTE / cellular signal quality

To activate signal retrieval:

```bash
mmcli -m 0 --signal-setup=5
```

To see current signal quality RSSI:

```bash
mmcli -m 0 --signal-get
```

Example output:

```bash
 ---------------------- 
Signal | refresh rate: 5 seconds
----------------------
LTE   |        rssi: -81.00 dBm
      |        rsrq: -10.00 dB
      |        rsrp: -107.00 dBm
      |        s/n: 10.00 dB
```

**Note:** RSSI measures the strength of a radio signal. Any RSSI value lower than -80 dBm is considered poor signal 
strength. Based on the client implementation some clients consider -75 dBm as poor strength as well, and will start 
roaming to a better Access Point, so values in the range -70 to -80 dBm are client dependent.
{: .notice--info}

#### Caveat
Multiple interfaces with internet(WAN) connection does not work in all Linux dists.

If the device has multiple interfaces with connection out to internet, some Linux systems seems to be confused. 
Sometimes containerd fails to pull images due to TLS validation timeouts etc...
