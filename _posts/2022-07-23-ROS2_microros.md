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

### Install micro-ROS

Follow the microros install instruction on the [official microros website](https://micro.ros.org/docs/tutorials/core/first_application_linux/).

    Problems encountered during installation:
    1. When using `sudo apt update && rosdep update`, rosdep has not been installed at this point. Use `sudo apt install python3-rosdep2` to install before running the command.
    2. When using `colcon build`, colcon has not been installed at this point. Use `sudo apt install python3-colcon-common-extensions`to install before runing the command.

Tried out the ping-pong node with foxy and everything worked fine just as decribed on the website.

#### Unsolved
When using galactic (another ros2 distribution), ping-pong node still works. However, the node and topics generated cannot be detected by using `ros2 node list` or `ros2 topic list`. Foxy is recommended.

### eProsima Micro XRCE-DDS
For micro-ROS on a micro computer to communicate with other devices in ROS2, you need the Micro XRCE-DDS.
What is Micro XRCE-DDS? According to the website:
    _[eProsima Micro XRCE-DDS](https://micro-xrce-dds.docs.eprosima.com/en/latest/)_ is a software solution that allows communicating eXtremely Resource Constrained Environments (XRCEs) with an existing DDS network.
    The _eprosima Micro XRCE-DDS_ library implements a client-server protocol that enables resource-constrained devices (clients) to take part in DDS communications. The _eProsima Micro XRCE-DDS Agent_ (server) acts as a bridge to make this communication possible.


### micro-ROS porting to ESP32

Basically follow the instruction on the [website](https://micro.ros.org/blog/2020/08/27/esp32/). It requires a little knowledge of connection, so I'll list what I did below.

Install these if you are starting from zero.
```bash
$ sudo apt update && rosdep update
$ sudo apt install python3-colcon-common-extensions
$ sudo apt-get install python3-pip
```

Basically the same as the tutorial.
```bash
$ mkdir microros_ws
$ cd microros_ws
$ git clone -b foxy https://github.com/micro-ROS/micro_ros_setup.git src/micro_ros_setup
$ sudo apt update && rosdep update
$ rosdep install --from-paths src --ignore-src -y
$ colcon build
$ source install/local_setup.bash
```

Recall the four-step procedure: Create step, Configure step, Build step and Flash step. We are basically following these steps.
Firstly, for create step:
```bash
$ ros2 run micro_ros_setup create_firmware_ws.sh freertos esp32
# for agents on linux, just use host
```

Secondly, for configure step, it can be executed with the following command:
```bash
ros2 run micro_ros_setup configure_firmware.sh [APP] [OPTIONS]
# no need to configure when trying agents on linux
```
For example, when we use WiFi connection and want to execute the app int32_publisher (ping_pong is another popular tutorial app):
```bash
$ ros2 run micro_ros_setup configure_firmware.sh int32_publisher -t udp -i [your local machine IP] -p 8888
```
(-t for --transport, -p for --port)
To check your local machine IP, in ubuntu, open Settings->Network, click the configuration icon, copy the IPv4 Address.
Now we configure the WiFi setting:
```bash
$ ros2 run micro_ros_setup build_firmware.sh menuconfig
```
You should see a window appearing. Now go to the micro-ROS Transport Settings → WiFi Configuration menu and fill your WiFi SSID and password. Save your changes, exit the interactive menu.

For other connection method such as serial, use:
```bash
$ ros2 run micro_ros_setup configure_firmware.sh int32_publisher -t serial
```

Thirdly, for build step:
```bash
$ ros2 run micro_ros_setup build_firmware.sh
```
Finally, for flash step: connect your ESP32 to the computer with a micro-USB cable, and run:
```bash
$ ros2 run micro_ros_setup flash_firmware.sh
# no need when trying agents on linux
```
You might see error saying Permission denied. To do the flash step correctly, you need to give permission to write on the ESP32.
First, check which address is your ESP32 using:
``` bash
$ ls /dev/ttyUSB*
```
You are looking for something like  /dev/ttyUSB0. You can check by connecting and disconnecting the device to see which one is changing.

Then, give permission to write on your ESP32:
```bash
$ sudo chmod 666 [your esp32]
```
screen is a convinient command to moniter the device.
```bash
# start monitering
$ screen [your esp32] 115200
# to detach from screen use:
Ctrl-a + Ctrl-d
# to resume screen:
$ screen -r
# to kill screen:
Ctrl-a + d
```
Yes, now you should be ready for the flash step. Run:
```
$ ros2 run micro_ros_setup flash_firmware.sh
```
The micro-ROS app is now ready to be connected to a micro-ROS agent to start talking with the rest of the ROS 2 world. To do that, let’s first of all create a micro-ROS agent, build the agent packages and, when this is done, source the installation:
``` bash
# Download micro-ROS-Agent packages_  
$ ros2 run micro_ros_setup create_agent_ws.sh
# Build step_  
$ ros2 run micro_ros_setup build_agent.sh  
$ source install/local_setup.bash
```

Run the agent:
```bash
# Run a micro-ROS agent  if using WiFi:　-v6??
$ ros2 run micro_ros_agent micro_ros_agent udp4 --port 8888
# If using serial:
$ ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyUSB0
```

Run another agent:
```bash
$ source /opt/ros/$ROS_DISTRO/setup.bash
$ source install/local_setup.bash
# Use RMW Micro XRCE-DDS implementation
$ export RMW_IMPLEMENTATION=rmw_microxrcedds
# Run a micro-ROS node
$ ros2 run micro_ros_demos_rclc ping_pong
```



自分用メモ：s
[このように](https://qiita.com/MAEHARA_Keisuke/items/fb94a9bd61db7564a413)または[このように](https://medium.com/@SameerT009/connect-esp32-to-ros2-foxy-5f06e0cc64df)
WiFiの接続が確立し，ルーターからIPが配布され，セッションが確立するとagentでestablish_sessionが現れてtopicとかをチェックできるようになるはずだが．．．
こっちでは`screen`を使ってIPの配布を確認できても，establish_sessionが現れずtopicもチェックできない
これはgalacticでpingpongやるときと同じような現象が起きているのではないかと見ている．．agent二つにするとお互いpingpongできるけど，topic listに出ない

これに関連する参考記事
https://answers.ros.org/question/386323/micro-ros-not-publishing-or-subscribing-to-topics/
solution given: set export ROS_DOMAIN_ID=0 inbash or type in every terminal
https://github.com/micro-ROS/micro_ros_arduino/issues/21
solution given: clear export ROS_DOMAIN_ID=0.....

ESP32設定関連
https://github.com/micro-ROS/micro_ros_espidf_component


なぜか以下を含むようなエラーがずっと出ててflashもできないことがあった．しかし，次の日にまた同じことを試すとできた．
```bash
# serialでping_pongをすると
W (374) spi_flash: Detected size(4096K) larger than the size in the binary image header (2084k). Using the size in the binary image header.
```

serialで一回成功したかもしれない．establish_sessionとかmsgとか色々出てきて，ros2 node listにもちゃんと出てきた．しかしその後flashやagentをrunさせることもなぜかできなくなった．

To use esp32 tools:
https://docs.espressif.com/projects/esp-idf/en/v3.1.7/get-started-cmake/add-idf_path-to-profile.html
https://github.com/micro-ROS/micro_ros_espidf_component
https://github.com/espressif/esp-idf

Platformio関連
https://github.com/micro-ROS/micro_ros_platformio
https://github.com/micro-ROS/micro_ros_arduino#platformio
 
iniファイルの設定
https://github.com/espressif/arduino-esp32/issues/5436
https://github.com/espressif/arduino-esp32/issues/6566
