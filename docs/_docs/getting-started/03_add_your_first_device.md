---
title: Add your first device
layout: single
permalink: /getting-started/add-your-first-device/
---

If you have a working [supported](/device-management/#supported-devices) device connected to internet you can create a 
device specific installer [here](https://teknoir.cloud/_/devices/new).

**Note:** This installer can only be used on one device or you will have multiple devices connecting with the same
credentials. That wont work!
{: .notice--warning}

1. Fill in the wanted name of the device and click **ADD**.
2. You will be redirected to the device page.
3. Scroll down to **Resources** and wait until the **Download** and **Copy** links become active, this should take no longer than 60 seconds.
4. Click the **Copy device-name's bootstrap string for the installer**, and the command is copied to your clipboard.
5. Open a secure shell to your device and paste the content and press enter.
6. Follow the instructions on the screen.

**Note:** You will be prompted at the end of the installer to add a user, `default: teknoir`, to your system. Be careful 
that it does not overwrite an existing user with keys or certificates!
{: .notice--danger}

Congratulations, the device will now try to connect to our platform and you will be able to manage it from there!

**Note:** Normally it takes no more than a couple of minutes for the device to connect but depending on the speed of 
your device, SD-card and internet connection it might take some minutes more. 
{: .notice--info}