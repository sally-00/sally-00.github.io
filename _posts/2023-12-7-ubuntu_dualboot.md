---
layout: post
title: dual boot Windows with Ubuntu
date: 2023-12-7 17:39:00
description: 
tags: linux
---

I followed [windows ubuntu dual boot](https://www.freecodecamp.org/news/how-to-dual-boot-windows-10-and-ubuntu-linux-dual-booting-tutorial/).

#### Note on disk partition

Partitions that say recovery disk on it, it's better not to remove them. It can be useful when you have issues with operation system.

When assigning partitions for ubuntu install, it is recommanded to have a `/swap` mount (besides `/` where the majority of your space go to, used for ubuntu installation and files storage) which should be about the memory of your computer size. Refer [here](https://www.dell.com/support/kbdoc/en-uk/000131391/how-to-install-ubuntu-with-multiple-custom-partitions-on-your-dell-pc).

If you have two instances of Ubuntu installed, the same `/swap` can be used for both systems. Refer [here](https://askubuntu.com/questions/1169424/how-do-i-put-two-ubuntu-oses-on-the-same-hard-drive#:~:text=Each%20instance%20of%20Ubuntu%20or,just%20not%20the%20same%20partition.) about installing two ubuntu system on the same computer.


#### changing the size of installed ubuntu partition

Open application called `Disks` and resize the ubuntu partition there.

It will not work if you try to resize the currently operating ubuntu system's partition. But, you can run from live system. I runed `try ubuntu` from a usb that has ubuntu iso burned to it, and used `Disks` application to resize the ubuntu installed on my computer.


#### WiFi not working on installed Ubuntu

- Option 1: get a WiFi adaptor USB. Instant Wifi without any fix!

- Option 2: 

I had an AX211 wifi card and ubuntu 20.04, [this post](https://askubuntu.com/questions/1402766/no-hope-for-ax211-wifi-working-on-ubuntu-20-04) was perfect for me.
I installed backport-iwlwifi-dkms package from [here](https://launchpad.net/ubuntu/+source/backport-iwlwifi-dkms)

If you have boardcom card, someone posted a very detailed instruction [here](https://askubuntu.com/questions/55868/installing-broadcom-wireless-drivers), but it's a quite old post.


#### using GPU on Ubuntu

In `Software & Updates` application, select the NVIDIA driver you want to install and click `Apply changes`.
If you just want to use the GPU, probably no need for Server and open kernel. Just install the `NVIDIA driver metapackage from nvidia-driver-<version> (proprietary)`.

Reboot to check if you installed GPU correctly. You might boot into black screen if something went wrong. Don't panic. You can refer to my post `ubuntu boot into black screen after installing Nvidia GPU driver` to purge nvidia driver and reboot. It will switch back to the default open source GPU driver and you should be able to see the screen again.

#### using GPU for machine learning, pytorch package

You will need to install CUDA, then pytorch package based on your CUDA version.

1. Follow the Pre-installation action on [CUDA installation guide linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)
2. google `CUDA Toolkit <verision> downloads`. For example [here](https://developer.nvidia.com/cuda-downloads?) is the website for installing toolkit for a certain version. Choose your target platform and the commands you need will appear.

Check [CUDA Compatibility](https://docs.nvidia.com/deploy/cuda-compatibility/) with Nvidia driver version. You might need older CUDA if you have a lower nvidia driver versi