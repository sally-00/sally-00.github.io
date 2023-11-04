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

Publish using command line
```bash
$ rostopic pub <name of the topic> <type of the topic> [args...]
# press TAB after rostopic pub <name of the topic> <type of the topic>, it auto fills the information needed
```

Download publisher and subscriber examples here:
``` bash
$ wget https://raw.github.com/ros/ros_tutorials/kinetic-devel/rospy_tutorials/001_talker_listener/talker.py
$ chmod +x talker.py
$ wget https://raw.github.com/ros/ros_tutorials/kinetic-devel/rospy_tutorials/001_talker_listener/listener.py
$ chmod +x listener.py
```
For the Service and Client samples in the tutorial, I got error: "ImportError: No module named beginner_tutorials.srv" when trying to run it, found [this link](https://answers.ros.org/question/114806/tutorial-116-importerror-no-module-named-beginner_tutorialssrv-with-catkin-system-build/) helpful.

Build the workspace:
```
$ cd ~/catkin_ws
$ catkin_make # need to do this everytime after changing the folder structure

# to build only one package
$ catkin_make [--only-pkg-with-deps]() <target_package>
```

Run the program:
```
# rosrun <package_name> <file_name>
$ rosrun beginner_tutorials talker.py
```


``` bash
# show all ros topic
$ rostopic list
# to check specific topic
$ rostopic list | grep <topic_name>
# show message type, subscriber, publisher
$ rostopic info <name of the topic>
# to measure the frequency of the image topic
$ rostopic hz <topic_name>
# show what is included in a topic
$ rosmsg show <a topic type>
# to display an image
$ rqt_image_view <topic_name>

# check ros launch logs (especially when there is an error), this shows the directory
$ roslaunch-logs
# to open the directory in GUI
$ nautilus <directory>
```