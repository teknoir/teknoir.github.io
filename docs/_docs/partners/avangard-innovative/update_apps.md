---
title: Update apps
permalink: /partners/avangard-innovative/update-apps/
toc: true
sidebar:
  nav: "avangard-innovative"
tags:
   - avangard-innovative
---

This example will show how to update the Darknet(sustayn) app, and most of it does apply for the Devstudio(devstudio)
app. Some of the differences will be touched in a separate section here on this page.

This process is meant to be automated fully and the node starting the pipeline should be triggred by another pipeline 
node that trains the new model. **This is a description of the manual steps!**

> The process of updating the apps can be subject to change as we improve features of the Teknoir platform.

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
* Run a pipeline to update the Darknet (sustayn) app
* Deploy a new version of the app to selected device(s)

> *Cloudstorage is the persistent object storage in the Teknoir Platform

#### To import new model files
1. Navigate to the [Artifact Browser](https://teknoir.cloud/_/avangard-production/artifact-browser?ns=avangard-production) 
   section using the left side menu in the Teknoir Console menu.
2. In the Artifact Browser you can find the /models folder. Double click the /models folder, and see the different 
   versions of the models in version-named folders.
3. Create a new folder inside /models with the name of the new version of the model, for example `0.0.1-alpha`, using 
   the action menu.
   <img src="/assets/avangard/new_folder.png" alt="image-status" style="zoom:100%;" />
4. Open the newly created folder and upload the model.cfg, model.weights and obj.names files using the action menu again.
5. Watch the progress bar and wait for the upload to finish.
   > When the upload is finished, ensure the file sizes are correct and representative of your local file sizes to avoid
   > corrupt browser uploads.

#### Run the pipeline
1. Browse to the [ml-ops](https://teknoir.cloud/_/devstudio/avangard-production/ml-ops/) Devstudio. Navigate in the 
   Teknoir Console menu to Devstudios and ther find the `ml-ops` Devstudio and click CONNECT.
2. Before running the pipeline, we need to update the version of the model, for the pipeline to pick up the correct one 
   and give the new app a proper name. Double-click  the `Build new versions of Sustayn Darknet App` node and set the 
   new `model_name` ex. `0.0.1-alpha` the same name you gave the folder where you put the new model files in.
   <img src="/assets/avangard/VERSION.png" alt="image-status" style="zoom:100%;" />
3. Click `Done`.
4. Click `Deploy`.
5. Click `Click here to start` and see the `Build new versions of Sustayn Darknet App` node get a new status.
6. Now you can find the new pipeline run, in the Teknoir Console menu, under Workflow -> Runs.
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

> Image name for arm based machines:
> us-central1-docker.pkg.dev/teknoir/avangard-production/sustayn_darknet:<version>

> Image name for  arm64v8(Texgra/Jetson family) based with NVIDIA GPU acceleration:
> us-central1-docker.pkg.dev/teknoir/avangard-production/sustayn_darknet-nv:<version>

1. Navigate to the [DevStudio Servers](https://teknoir.cloud/_/devstudios/?ns=avangard-production) section using 
   the left side menu in the Teknoir Console.
2. Connect to Your DevStudio Server and make sure you're viewing the Device Config tab.
   <img src="/assets/avangard/device_config.png" alt="image-status" style="zoom:100%;" />
3. Double-click the add `sustayn` app node.
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
   4. Update the fields to match the labeling of the devices you want to add to the selection. You can add multiple 
      label combinations by repeating step 2-3. Remove a label combination by clicking the tiny x to the right of the input fields.
   5. Click Done.
7. Lastly, click Deploy in the top right corner of the interface.
   
The new version of the app, with the updated model, is now running on selected device(s).

### Updating the Devstudio (devstudio) app
Please learn how to deploy the Darknet (sustayn) app above, this process is very similar.

#### Updating the model and deploying a new version of the app
The Devstudio app use Node-Red, an open source framework, for low-code programming. The `flows.json` file
holds the configuration of the Devstudio app.

Perform the following steps:
* Upload the `flows.json` file to a version named folder using [Artifact Browser](https://teknoir.cloud/_/avangard-production/artifact-browser?ns=avangard-production)
* Browse to the [ml-ops](https://teknoir.cloud/_/devstudio/avangard-production/ml-ops/) Devstudio, update the `flows_name`
  field in the `Build new versions of Sustayn Event Processing app` and press `Done`, then `Deploy` and start the pipeline.
* Deploy a new version of the app to selected device(s)

#### TLDR;
1. Navigate to the [Artifact Browser](https://teknoir.cloud/_/avangard-production/artifact-browser?ns=avangard-production)
2. Create a new folder inside /flows with the name of the new version, for example `0.0.1-alpha`
3. Open the newly created folder and upload the `flows.json` file
4. Browse to the [ml-ops](https://teknoir.cloud/_/devstudio/avangard-production/ml-ops/) Devstudio
5. Before running the pipeline, update the `flows_name` field in the `Build new versions of Sustayn Event Processing app` node
6. Press `Done`
7. Press`Deploy`
8. Start the pipeline and see the downstream node change status
10. Now you can find the new pipeline run, in the Teknoir Console menu, under Workflow -> Runs
11. Navigate to the [configure-devices](https://teknoir.cloud/_/devstudio/avangard-production/configure-devices/) Devstudio
13. Double-click the `add devstudio` app node you want to update
14. Change the image name to match the name of the new app version then click Done
15. Now, double-click the configure node to the far right in the flow
16. Select which device(s) you want to deploy the new version of the app
17. Deploy in the top right corner of the interface

> Image name for arm based machines:
> us-central1-docker.pkg.dev/teknoir/avangard-production/sustayn-event-processing:<version>