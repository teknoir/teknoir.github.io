---
title: Device Management
toc: true
permalink: /device-management/
---

## Requirements

- [ ] Access to the Teknoir Console and a namespace (done through registration)
- [ ] An SD-card (Minimum 8GB, but certain hardware configurations might require more)
- [ ] [balenaEtcher](https://www.balena.io/etcher/) (Free)
- [ ] A supported device*

**Note:** You also need a memory card reader to flash the image to the SD-card. If your computer doesn't have a memory
card reader, you can [purchase an external one](https://www.amazon.com/s?k=Memory+Card+Readers) and connect it to your
computer.
{: .notice--info}

## Supported devices

**Note:** *We currently support Raspberry Pi (3-series, 4-series) and NVIDIA Jetson Nano for building custom Teknoir OS 
images. But any AMD64, ARM32 or ARM64 based device running a recent Debian or Ubuntu Linux distribution should work with 
our installer.
{: .notice--warning}

## Adding a device

First of all you need to decide if you will use our configured OS image for a device of if you need to maintain your own
operating system for your device.

To help you decide, here are some differences.

The installer is a drop-in bootstrap script that installs the software and certificates needed to communicate securely
with the Teknoir platform. It prompts at the end and asks if it can install a user and keys for secure remote access
through tunneling in the Teknoir platform. The installer is run with a single command copied directly from the
device´s page and pasted in the terminal shell of the device.

**Note:** The installer will **not** modify any network settings on the device.
{: .notice--warning}

The generated operating system is installed to an SD-card or EMMC on a device. The image is usually self expanding to 
use the full SD card and contain both network settings and the software needed to securely communicate with the platform.
This can be useful for larger roll outs where devices has to have the same settings to work predictably, with minimum
manual intervention.

### Configure the device

**Note:** To generate an OS image for a device can take up to 1h depending on hardware.
{: .notice--warning}

1. Browse to [devices](https://teknoir.cloud/_/devices/).
2. Choose namespace.
3. Click **+ NEW DEVICE** button.
4. Fill out the input fields, descriptions below.
5. Click **Add** to create the device.

#### Name (required)

This will be the name of the device.

#### Namespace (not editable)

This indicates which namespace the device will belong to. To create a device under another namespace, please select namespace in the top bar prior to creating a new device.

#### Hardware (optional)

Select type of device or device architecture. Choose `generic` to skip OS image creation and only rely on the installer.

#### User (optional)

Modes:
- Generated user authentication: User name will be `teknoir` with a generated password.
- Username and password: You can specify user name and password yourself.

Fields:
- User Name: This will be the username of the account used to access the device operating system.
- Password: Set a password for the account. The password needs to be at least 8 characters long, and also contain at least: one uppercase, one lowercase and one number.
- SSH Authorized Public Key: Copy your own public ssh key here for convenience when connecting to the device on a local network.

**Note:** The SSH Authorized Public Key will be provisioned to the users `authorized_keys`. This enables password less ssh login for that user if you have the matching private key. 
{: .notice--info}

#### Ethernet (optional)

**Note:** This is not available for `generic` hardware option.
{: .notice--info}

Modes:
- Dynamically assign IP: You acquire IP address automatically with DHCP client.
- Static IP: You configure a static IP address and subnet mask.
- Static IP + DHCP Server: You configure a static IP address and subnet mask and start a DHCP server to let peripherals acquire IP addresses on the same subnet.

Fields:
- IP Address: The static IP address.
- Subnet: Specify subnet mask in CIDR format.

#### Wifi (optional)

**Note:** This is not available for `generic` hardware option.
{: .notice--info}

Modes:
- No Wifi: Do not configure any Wifi
- Connect to Wifi: Specify credentials for the Wifi network to connect to.
- Create Access Point: Create a Wifi with credentials that peripherals can connect to.

Fields:
- SSID: Enter the name of the network you wish to grant the device access to.
- Password: Enter the password for the network.
- Country Code: Enter the country code for the network. A full list of country codes can be found [here](https://github.com/recalbox/recalbox-os/wiki/Wifi-country-code-(EN)).

**Note:** Adding WiFi credentials to the device configuration will allow the device to automatically connect to that nearby WiFi when booting up.
{: .notice--info}

#### Metadata (optional)
Add and remove metadata/labels that later can be used for managing devices at scale and annotate data.

- Add Label: Use this button to add an additional row of *key* and *value*.
- Key: Enter keyword for the metadata (example: *city*).
- Value: Enter value for the corresponding keyword metadata (example: *new york*).

### Create a "drop-in" installer script

The installer is created for all types of devices, but if the `generic` hardware option is chosen it is the only thing to
be generated for that device. The process usually takes less than 30 seconds.

1. Browse to [devices](https://teknoir.cloud/_/devices/).
2. Choose namespace.
3. Click the device name.
4. Scroll down to **Resources** and wait until the **Download** and **Copy** links for the installer become active, this should take no longer than 60 seconds.

#### Run the installer on the device

1. When ready, click the **Copy device-name's bootstrap string for the installer** link, and the command is copied to your clipboard. {% include figure image_path="/assets/download-image.png" alt="download-image" %} 
2. Open a secure shell to your device and paste the content and press enter. 
3. Follow the instructions on the screen.

**Note:** You will be prompted at the end of the installer to add a user, `default: teknoir`, to your system. Be careful
that it does not overwrite an existing user with keys or certificates!
{: .notice--danger}

Congratulations, the device will now try to connect to our platform and you will be able to manage it from there!

**Note:** Normally it takes no more than a couple of minutes for the device to connect but depending on the speed of
your device, SD-card and internet connection it might take some minutes more.
{: .notice--info}

### Configure and create an OS image

If you do not choose `generic` in the hardware dropdown a Teknoir Operating System (OS) image that can SD-card image will be created.

#### Flash the image to an SD-card

When the device is being created you are automatically directed to the **Device** page, which can also be accessed via the device list by clicking the device name.

**Note:** Please note that it can take anywhere from 15 to 45 minutes for the image to be created. The is highly dependent on 
the hardware configuration. Take a break and refresh the **Device** page when you're back. The **Download OS image...** link 
will activate when the image is ready for download.
{: .notice--warning}

1. When ready, click the **Download OS image...** link to download the device image to your computer. {% include figure image_path="/assets/download-image.png" alt="download-image" %}
2. Unzip the downloaded file ***image.zip*** to reveal the ***image.img*** device image file.
3. Insert an SD-card into your memory card reader. The minimum requirement is a 8GB SD-card.
4. Open **balenaEtcher**.
5. Click **Flash from file** and browse to the file location of your device image (***image.img***). Select the file ***image.img*** and click **Open**. {% include figure image_path="/assets/balena-Etcher-1.png" alt="balenaEtcher-1" %}
6. Next, click **Select target**. {% include figure image_path="/assets/balena-Etcher-2.png" alt="balenaEtcher-2" %}
7. Select your ***SD Card Reader Media*** target, then click **Select (1)**. {% include figure image_path="/assets/balena-Etcher-3.png" alt="balenaEtcher-3" %}
8. Next, click **Flash!** to begin flashing the device image to the SD-card. {% include figure image_path="/assets/balena-Etcher-4.png" alt="balenaEtcher-4" %}
9. When the flash and validation process is completed you have a device ready image on the SD-card. Insert the SD-card into your device and connect it to a power source to boot up the device and complete the installation.

### Verify device status in the Teknoir Console

**Note:** It takes a couple of minutes for the device to boot up and connect depending on the hardware configuration.
{: .notice--warning}

1. To verify that the device is working and is connected to your account/namespace, simply visit the **Device** page and wait for the device to appear. {% include figure image_path="/assets/device-list.png" alt="device-list" %}
2. When the device is connected, **last seen** will change from ***never*** to how long time it was since it communicated with the platform.


## Editing a device

TBD


## Removing a device

TBD

