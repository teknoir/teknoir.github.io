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

Labels in the form "key:value" where the key is 1-128 long, starts with a letter and contain only alphanumeric 
characters and ._+~%. The value is a string, max 32KB.

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
<img src="/assets/avangard/select_device_by_label_3.png" alt="image-status" style="zoom:100%;" />
All devices matching the set of labels will be configured with the apps linked to it.

### Example

Setting the following labels:

| Key       | Value           |
|:----------|:----------------|
| camera    | bosch           |
| operation | production      |

Will match Device #2.

## Patch level

We use Ansible to patch live devices, and to make sure we have successfully patched a device we write or update a label
on the device as the last step.

The Teknoir Ansible inventory use the device name, namespace and the labels to create a versatile set of device groups.
Please refer to the github repository: https://github.com/teknoir/ansible