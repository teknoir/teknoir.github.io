---
title: "/dev/fd/63 No such file or directory"
layout: single
categories:
  - troubleshooting
tags:
  - troubleshooting-devices
  - troubleshooting
---

## "/dev/fd/63 No such file or directory"
If you get the message "/dev/fd/63 No such file or directory" when trying to run our installer with the "drop-in" script.
You have most likely run the command prefixed with sudo, ex: `sudo bash <(...)`. Process substitution, `<(...)`, use an 
anonymous pipe, `/dev/fd/63`, and that does not work under sudo. The solution is to run it without `sudo`.

**Solution:** Do to use `sudo` for the installer. Our installer, the "drop-in" script, already takes sudo into account. 
And if it is neededs it, it will ask for you to enter the sudo password.
{: .notice--info}