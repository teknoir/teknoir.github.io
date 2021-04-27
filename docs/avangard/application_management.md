---
title: Application management
layout: page
permalink: /avangard/application-management/
---

[<- Table of Contents](index.md)

_**Please note that this wiki is under construction (UC). We're working on getting the most fundamental parts ready as soon as possible. We appreciate your support and understanding in this regard.**_

---
## Topics
* TBD

## Avangard Apps
The two main apps that does the edge computing is very different, one is based on the Teknoir Devstudio and the other one is
based on Darknet.

Lets first shortly define them.

### Devstudio
The Devstudio(called `darknet` in GUI) is a low-code programming environment, that can be used both in the cloud and on an edge device.
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

## Updating apps
> The process of updating the apps can be subject to change as we improve features of the Teknoir platform.

This example will show how to update the Darknet(sustayn) app, and most of it does apply for the Devstudio(devstudio)
app. Some of the differences will be touched in a separate section here on this page.

### Updating the Darknet (sustayn) app
The following is a step-by-step guide to updating the machine learning model for
detecting recyclable objects and deploying new versions of the Darknet (sustayn) app
to selected device(s) via the Teknoir Platform.

#### Updating the model and deploying a new version of the app
The Darknet App uses the base Yolo V3 weights, config, and objects files. To update the
app, we must train the model with updated weights, config, and objects files and then 
deploy a new version of the app to selected device(s).

Perform the following steps:
* Upload all the necessary files to Cloudstorage*
* Run a notebook to update the model
* Deploy a new version of the app to selected device(s)

> *Cloudstorage is the persistent object storage in the Teknoir Platform

#### To import new model files
1. Navigate to the [Notebook Servers](https://console.teknoir.cloud/_/jupyter/) section using the left side menu in the 
   Teknoir Console.
2. *Connect to Your Notebook Servers and browse to /cloudstorage/models
   <img src="/assets/avangard/navigate_to_cloudstorage.png" alt="image-status" style="zoom:100%;" />
   > *Navigating to cloudstorage is a bit slower than other file system operations, as it is a persistent object storage
3. Create a new folder inside /models with the name of the new version of the model, for example `0.0.1-alpha`.
   <img src="/assets/avangard/new_folder.png" alt="image-status" style="zoom:100%;" />
4. Open the newly created folder and upload the model.cfg, model.weights and obj.names files by dragging and dropping 
   the files into the folder view in your web browser or by using the upload button highlighted in green below.
   <img src="/assets/avangard/upload.png" alt="image-status" style="zoom:100%;" />
5. Watch the progress bar at the bottom of the page and wait for the upload to finish.
   > When the upload is finished, ensure the file sizes are correct and representative of your local file sizes to avoid
   > corrupt browser uploads. To do this, simply hover with the mouse pointer over the file name to show file information.

#### Run the notebook
1. Browse to root by clicking the folder icon to the left of the / in the path directory and open 
   build_sustayn_detect_recyclables_app.ipynb by double clicking it.
   <img src="/assets/avangard/root.png" alt="image-status" style="zoom:100%;" />
2. Before running the notebook, we need to update the VERSION variable to match the new model name (`0.0.1-alpha`), i.e., 
   the same name you gave the folder where you put the new files in.
   <img src="/assets/avangard/VERSION.png" alt="image-status" style="zoom:100%;" />
3. Run the notebook from the menu (Run -> Run All Cells).
   <img src="/assets/avangard/run.png" alt="image-status" style="zoom:100%;" />
4. At the very bottom of the notebook page, two links will appear. Click Run link here to monitor the pipeline progress.
   When all steps are cleared (green checkmarks), the run has completed without errors. The workflow pipeline is 
   interactive and you easily can see all the variables and important log entries to identify potential errors in the 
   flow, should they occur.
   
When the run has completed, the model has been updated with the new model.cfg, model.weights and obj.names files. Next, 
we want to run the updated model on selected device(s). To do this, we simply deploy a new version of the app to 
selected device(s),
   
#### Deploy a new version of the app
Deploying a new version of the app to selected device(s) is as simple as updating the image variable in the add 
sustayn app node to match the name of the updated version, i.e., the name of the folder we just 
created (`0.0.1-alpha`).

1. Navigate to the [DevStudio Servers](https://console.teknoir.cloud/_/devstudios/?ns=avangard-production) section using 
   the left side menu in the Teknoir Console.
2. Connect to Your DevStudio Server and make sure you're viewing the Device Config tab.
   <img src="/assets/avangard/device_config.png" alt="image-status" style="zoom:100%;" />
3. Double-click the add sustayn-detect-recyclables app node.
   <img src="/assets/avangard/select_app.png" alt="image-status" style="zoom:100%;" />
4. Change the image variable to match the name of the new app version (`0.0.1-alpha`) then click Done.
   <img src="/assets/avangard/edit_app_node.png" alt="image-status" style="zoom:150%;" />
5. Now, double-click the configure node to the far right in the flow.
6. Select which device(s) you want to deploy the new version of the app to using Name
   or Labels:
   **Select Devices By Name:**
   1. Select Mode: Select Devices By Name.
      <img src="/assets/avangard/select_device_by_name.png" alt="image-status" style="zoom:100%;" />
   2. Next, click to select device(s) in the list. Hold CTRL/COMMAND to select multiple devices in the list.
   3. Click Done.
   
   **Select Devices By Labels:**
   1. Select Mode: Select Devices By Labels.
      <img src="/assets/avangard/select_device_by_label.png" alt="image-status" style="zoom:100%;" />
   2. Next, click Add.
      <img src="/assets/avangard/select_device_by_label_2.png" alt="image-status" style="zoom:100%;" />
   3. This adds a combination of two input fields - Key (upper) and Value (under).
      <img src="/assets/avangard/select_device_by_label_3.png" alt="image-status" style="zoom:100%;" />
   4. Update the fields to match the labeling of the devices you want to add to the selection. You can add multiple label combinations by repeating step 2-3. Remove a label combination by clicking the tiny x to the right of the input fields.
   5. Click Done.
7. Lastly, click Deploy in the top right corner of the interface.
   
The new version of the app, with the updated model, is now running on selected device(s).

### Updating the Devstudio(devstudio) app
Please learn how to deploy the Darknet (sustayn) app above, and this process is very similar.

#### Updating the model and deploying a new version of the app
The Devstudio app use Node-Red, an open source framework for low-code programming. The `flows.json` file


Perform the following steps:
* Upload all the necessary files to Cloudstorage*
* Run a notebook to update the model
* Deploy a new version of the app to selected device(s)

> *Cloudstorage is the persistent object storage in the Teknoir Platform

#### To import new flow file