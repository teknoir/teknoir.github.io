---
title: Add a new device
layout: page
permalink: /add-new-device/
---

[<- Table of Contents](index.md)

In this tutorial we will show you how to add a new device to a namespace using the Teknoir Console.

**Steps:**

1. Create a configured device image
2. Flash the image to an SD-card
3. Verify device status in the Teknoir Console

**Requirements:**

- [ ] Access to the Teknoir Console and a namespace (done through registration)
- [ ] An SD-card (Minimum 8GB, but certain hardware configurations might require more)
- [ ] [balenaEtcher](https://www.balena.io/etcher/) (Free)
- [ ] A supported device*

**We currently support Raspberry Pi (3-series, 4-series) and NVIDIA Jetson Nano*.

> *You also need a memory card reader to flash the image to the SD-card. If your computer doesn't have a memory card reader, you can [purchase an external one](https://www.amazon.com/s?k=Memory+Card+Readers) and connect it to your computer.*

## Create a configured device image

1. Access the Teknoir Console and navigate to the main dashboard using the left side menu option **Home**.
2. Click **Add a device** under the **Quick shortcuts** section:

<img src="/assets/add-a-device.png" alt="add-a-device" style="zoom:50%;" />  

3. Fill out the input fields:

    - **Name** (required)

        - Name: This will be the name of the device.
        - Namespace: This indicates which namespace the device will belong to. To create a device under another namespace, please select namespace in the top bar prior to creating a new device.

    - **Hardware** (required)

        - Hardware: Select type of device or device architecture.

    - **User** (required)

        - User Name: This will be the username of the account used to access the device operating system.
        - Password: Set a password for the account. The password needs to be at least 8 characters long, and also contain at least: one uppercase, one lowercase and one number.
        - *SSH Authorized Public Key: Upcoming feature, not available yet.*

    - **WiFi*** (optional)

        - SSID: Enter the name of the network you wish to grant the device access to.
        - Password: Enter the password for the network.
        - Country Code: Enter the country code for the network.  A full list of country codes can be found [here](https://github.com/recalbox/recalbox-os/wiki/Wifi-country-code-(EN)).

    - **Metadata** (optional)

        - Add Label: Use this button to add an additional row of *key* and *value*.
        - Key: Enter keyword for the metadata (example: *city*).
        - Value: Enter value for the corresponding keyword metadata (example: *new york*).

4. Click **Add** to create the device image.

> **Adding WiFi credentials to the device configuration will allow the device to automatically connect to that nearby WiFi when booting up.*

## Flash the image to an SD-card

When the device image is being created you are automatically transfered to the **Device** list, which can also be accessed via the left side menu.

> *Please note that it can take anywhere from 15 to 45 minutes for the image to be created. The is highly dependent on the hardware configuration. Take a break and refresh the **Device** page when you're back. The **Download Image** icon will confirm when the image is ready for download.*

<img src="/assets/image-status.png" alt="image-status" style="zoom:50%;" />

1. When ready, click the **Download Image** icon to download the device image to your computer.

<img src="/assets/download-image.png" alt="download-image" style="zoom:50%;" />

2. Unzip the downloaded file ***image.zip*** to reveal the ***image.img*** device image file.
3. Insert an SD-card into your memory card reader. The minimum requirement is a 8GB SD-card.
4. Open **balenaEtcher**.
5. Click **Flash from file** and browse to the file location of your device image (***image.img***). Select the file ***image.img*** and click **Open**.

<img src="/assets/balena-Etcher-1.png" alt="balenaEtcher-1" style="zoom:50%;" />

6. Next, click **Select target**.

<img src="/assets/balena-Etcher-2.png" alt="balenaEtcher-2" style="zoom:50%;" />

7. Select your ***SD Card Reader Media*** target, then click **Select (1)**.

<img src="/assets/balena-Etcher-3.png" alt="balenaEtcher-3" style="zoom:50%;" />

8. Next, click **Flash!** to begin flashing the device image to the SD-card.

<img src="/assets/balena-Etcher-4.png" alt="balenaEtcher-4" style="zoom:50%;" />

9. When the flash and validation process is completed you have a device ready image on the SD-card. Insert the SD-card into your device and connect it to a power source to boot up the device and complete the installation.

## Verify device status in the Teknoir Console

1. To verify that the device is working and is connected to your account/namespace, simply visit the **Device** page in the Teknoir Console and refresh the list using the **Update** button.

> *It takes a couple of minutes for the device to boot up and connect depending on the hardware configuration.*

<img src="/assets/update-device-list.png" alt="update-device-list" style="zoom:50%;" />

2. When the device is connected, status will change from ***Never Seen*** to ***Alive!***.

<img src="/assets/device-connected.png" alt="device-connected" style="zoom:50%;" />

This concludes the tutorial on how to add a new device to your namespace.

## Having problems?

Maybe [this](troubleshooting.md) troubleshooting guide can be of help.