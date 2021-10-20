---
title: Apps
permalink: /partners/avangard-innovative/apps/
toc: true
tags:
   - avangard-innovative
sidebar:
   nav: "avangard-innovative"
---
 
The two main apps that does the edge computing is very different, one is based on the Teknoir Devstudio and the other one is
based on Darknet.

Lets first define the apps.

### Devstudio
The Devstudio(called `devstudio` in GUI) is a low-code programming environment, that can be used both in the cloud and on an edge device.
This Devstudio runs on the device.

The Devstudio has several functions in this setup.
* Simple gate/filters
   * SSIM - Structural Similarity Index Measurement of an image
   * Luminosity - perceived brightness of an image
* Add geographic location
* Object gate/filter
   * Object class
   * Position in image
* Post detections to endpoint
   * Format message
* Collect monitoring information

> Purpose: Consolidate data from multiple apps (microservices), minimise transmitted data by filtering out unwanted 
> results. Collect monitoring metrics.

### Darknet
The Darknet(called `sustayn` in GUI) is a vanilla C++ implementation with Nvidia GPU hardware support built in.

> Purpose: Efficiently run the custom, object detection, model. To detect recyclables.

### Other Apps
There are also other apps: camera, gps and hardware.

#### Camera
The camera app use the IP-camera API to take images and decide the image rate.

#### GPS
The GPS app extract the geographic location.
 
#### Hardware
The hardware app collect monitoring information about the device:
* CPU Usage
* CPU Temp
* GPU Usage
* GPU Temp
* Network traffic in/out
* Memory Usage
