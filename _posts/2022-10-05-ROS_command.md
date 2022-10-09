---
layout: post
title: useful ROS command memo
date: 2022-10-05 17:39:00
description: project memo
tags: ROS
---

Create a package:
```bash
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
$ catkin_create_pkg pkg_name std_msgs rospy roscpp
```
Package dependencies are stored in package.xml
Navigate to the package directory:
``` bash
# roscd <package_name>e
$ roscd pkg_name
```
Copy files from other package:
``` bash
$ roscp [package_name] [file_to_copy_path] [copy_from_this_path]
```

Download publisher and subscriber examples here:
``` bash
$ wget https://raw.github.com/ros/ros_tutorials/kinetic-devel/rospy_tutorials/001_talker_listener/talker.py
$ chmod +x talker.py
$ wget https://raw.github.com/ros/ros_tutorials/kinetic-devel/rospy_tutorials/001_talker_listener/listener.py
$ chmod +x listener.py
```

Build the workspace:
```
$ cd ~/catkin_ws
$ catkin_make
# to build only one package
$ catkin_make [--only-pkg-with-deps]() <target_package>
```

Run the program:
```
# rosrun <package_name> <file_name>
$ rosrun beginner_tutorials talker.py
```

During the Service and Client tutorials, I got error: "ImportError: No module named beginner_tutorials.srv", found [this link](https://answers.ros.org/question/114806/tutorial-116-importerror-no-module-named-beginner_tutorialssrv-with-catkin-system-build/) helpful.


Service and Client:
Is server like a function and client can call it to get some kind of result?