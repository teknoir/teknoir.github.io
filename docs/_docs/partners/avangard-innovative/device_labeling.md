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
|:----------|:----------------|
| hardware  | jetson-nano-b00 |
| camera    | axis            |
| city      | houston         |
| operation | test            |

Device #2:

| Key       | Value           |
|:----------|:----------------|
| hardware  | raspberry-pi    |
| camera    | bosch           |
| city      | austin          |
| operation | production      |


## Configuration management

In the `Configure device` node in the Devstudio, enable `Select Devices by Label` mode. 
<img src="/assets/avangard/select_device_by_label.png" alt="image-status" style="zoom:100%;" />
Then `+add` the labels it should match.
<img src="/assets/avangard/select_device_by_label_2.png" alt="image-status" style="zoom:100%;" />

## Patch level

We use Ansible to patch live devices, and to make sure we have successfully patched a device we write or update a label
on the device as the last step.

The Teknoir Ansible inventory use the device name, namespace and the labels to create a versatile set of device groups.
Please refer to the github repository: https://github.com/teknoir/ansible