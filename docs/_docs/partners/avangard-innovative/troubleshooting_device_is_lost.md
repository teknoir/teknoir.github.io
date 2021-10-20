---
title: Device is lost
permalink: /partners/avangard-innovative/troubleshooting-device-is-lost/
toc: true
sidebar:
  nav: "avangard-innovative"
tags:
  - avangard-innovative
---

Normally the device have a self healing behavior. That means it will try to re-connect to the platform
by restarting different subsystems controlled by a self healing algorithm.

Reasons it might not connect:
* Data plan quota exceeded
* Bad or flaky LTE connection

Hardware sometimes break, and in that case it is easy to prepare and test an exchange unit.
Just note the name of the device, follow the steps in [Missing SD-card](#missing-sd-card) section.

### Monitoring

There are custom monitoring built for Avangard-Innovative.

#### A single device dashboard
[Avangard Device](https://console.teknoir.cloud/_/avangard-production/grafana/d/avangarddevices/avangard-device)

Pick one device at the time from the dropdown at the top to view detailed info about this device. 

#### An aggregated view of devices
[Avangard All Devices](https://console.teknoir.cloud/_/avangard-production/grafana/d/avangarddevices/avangard-all-devices)

This dashboard show an aggregated view of the devices.

#### Devices coming back from being lost
[Devices coming back from the dead](https://console.teknoir.cloud/_/avangard-production/grafana/d/backfromdead/devices-coming-back-from-the-dead)

This dashboard list information about when and how long devices has been lost.