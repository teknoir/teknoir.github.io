---
title: Device labeling
permalink: /partners/avangard-innovative/device-labeling/
sidebar:
  nav: "avangard-innovative"
tags:
  - avangard-innovative
---
  
Device labels is a way of adding extra information to a device, we call it metadata. Labels can be used to describe 
features of the device, for example hardware, if it is a Raspberry Pi or Jetson Nano device or what type of camera it has.
Labels can also be used for configuration management, if there is some reason to have different apps on different devices.
We also use it to denominate "patch level", to keep track of Operating System patches.

## Format
Labels in the form "key:value"

### Examples

Device #1:

| Key       | Value           |
|:----------|----------------:|
| hardware  | jetson-nano-b00 |
| camera    | axis            |
| city      | houston         |
| operation | test            |

Device #2:

| Key       | Value           |
|:----------|----------------:|
| hardware  | raspberry-pi    |
| camera    | bosch           |
| city      | austin          |
| operation | production      |


## Configuration management
TBD

## Patch level
TBD