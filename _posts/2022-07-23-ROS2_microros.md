---
layout: post
title: ROS2 and microros
date: 2022-07-18 17:39:00
description: project memo
tags: ROS2
---

### Background
Moving a multi-agent system from ROS to ROS2. For ROS2 to work on ESP32, use microros.

ubuntu: 20.04.3 (vmware fusion on Mac with intel chip)
ros2: foxy

### Install ROS2 foxy
Follow the foxy install instruction on the [official ros website](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html).
Configure environment following [here](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html).
It was pretty smooth, didn't encounter any problem.

### Install microros

Follow the microros install instruction on the [official microros website](https://micro.ros.org/docs/tutorials/core/first_application_linux/).
Problems encountered:
1. When using `sudo apt update && rosdep update`, rosdep has not been installed at this point. Use "sudo apt install python3-rosdep2" to install before running the command.
2. When using `colcon build`, colcon has not been installed at this point. Use "sudo apt install python3-colcon-common-extensions"to install before runing the command.

When running `ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888`, there was no problem. But after running `ros2 run micro_ros_demos_rclc ping_pong` in another terminal, ping_pong is aborted with warning in rcl_node_init and rclc_node_init_with_options. Error also apeared in micro_ros_agent saying `[RTPS Error] Calculated port number is too high. Probably the domainID is over 232 or portBase is too high. -> Function getMulticasePort`