---
layout: post
title: ubuntu boot into black screen after installing Nvidia GPU driver
date: 2023-10-30 17:39:00
description: 
tags: linux
---

There were issues installing Nvidia's GPU driver and resulted in booting into black screen.
This is to avoid me from panicking the next time something with GPU driver goes wrong.

So long story short, the solution is to 
1. modify boot setting to boot into a text console
2. purge nvidia driver
3. reboot -> it will get back to the default ubuntu GPU driver

### To boot into text console 

Do not just press enter key to select ubuntu to boot in.
Instead, press 'e' button to enter a boot setting editor.
Remove "quiet splash vt.handoff" and replace with " --- 3". 
What that will do is boot to text console rcmode 3 (multi-user).

You will need to Login with your userid and password.

### purge nvidia

Run the following command to remove nvidia driver.

``` bash
sudo apt remove --purge '^nvidia-.*'
sudo apt autoremove
sudo reboot
```

