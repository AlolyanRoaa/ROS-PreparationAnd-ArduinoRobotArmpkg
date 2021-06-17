

# ROS Preparation and Arduino_Robot_Arm pkg

documentation of preparing ROS with arduino_robot_arm package


## Outline:

- Installing & Preparing ROS melodic
- Installing the package **arduino_robot_arm**
- Using Arduino with ROS
- simulation & Controlling the motors `joint_state_publisher`
- Creating the manipulation with MoveIt

  
## 1-Installing & Preparing ROS melodic

Using Ubuntu 18.04 OS run these commands in the terminal: 



#### Installing:

To setup the machine to accept packages.ros.org
```bash
  $ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
Set up the keys.
```bash
  $ curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```
make sure the Debian package index is updated using `sudo apt update`. Then install the Desktop-Full packages.
```bash
  $ sudo apt install ros-melodic-desktop-full
```
To setup the environment 
```bash
   $ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc source ~/.bashrc
```
install dependencies for building packages
```bash
   $ sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
and for initialize rosdep to use ROS tools 
```bash
  $ sudo apt install python-rosdep
  $ sudo rosdep init
  $ rosdep update
```


#### Preparing:

To start using ROS properly we have to create a workspace for catkin.

Start by Installing the prebuilt Package catkin and resolve the dependencies on Ubuntu.

```bash
   $ sudo apt-get install ros-melodic-catkin
   $ sudo apt-get install cmake python-catkin-pkg python-empy python-nose python-setuptools libgtest-dev build-essential
```
sourced your environment the create and build a catkin workspace
```bash
$ source /opt/ros/melodic/setup.bash

$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
```
To make sure that the workspace is properly working with bashrc
```bash
    $ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```


## 2-Installing the package **arduino_robot_arm**
 Add the **arduino_robot_arm** package to “src” folder in the catkin workspace
 ```bash
    $ cd ~/catkin_ws/src
    $ sudo apt install git
    $ git clone https://github.com/smart-methods/arduino_robot_arm 
```
Install all the dependencies of the package
```bash
        $ cd ~/catkin_ws
	$ rosdep install --from-paths src --ignore-src -r -y
	$ sudo apt-get install ros-melodic-moveit
	$ sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
	$ sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
	$ sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
```
To compile the package
```bash
    $ catkin_make
```


## 3-Using Arduino with ROS
*Note: for not having a physical arduino all parts that have to initialize the USP port has not been done*

Start by downloading Arduino IDE 1.8.15 from: <https://www.arduino.cc/en/software>.

install rosserial for Arduino
```bash
    $ sudo apt-get install ros-kinetic-rosserial-arduino
    $ sudo apt-get install ros-kinetic-rosserial
```
install ros_lib library
```bash
    $ cd <sketchbook>/libraries
    $ rm -rf ros_lib
    $ rosrun rosserial_arduino make_libraries.py . 
```
## 4-simulation & Controlling the motors `joint_state_publisher`
To run robot_arm_pkg with RViz use 


![robot_arm_pkg with RViz](https://github.com/AlolyanRoaa/ROS-PreparingWith-ArduinoRobotArmpkg/blob/main/4-simulation%20%26%20Controlling%20the%20motors%20joint_state_publisher/1-%20controlling%20the%20motors%20with%20RViz.PNG)
```bash
	$ roslaunch robot_arm_pkg check_motors.launch
```
and to run robot_arm_pkg with Gazebo use 


![robot_arm_pkg with gazebo](https://github.com/AlolyanRoaa/ROS-PreparingWith-ArduinoRobotArmpkg/blob/main/4-simulation%20%26%20Controlling%20the%20motors%20joint_state_publisher/2-run%20on%20the%20gazebo.PNG)
```bash
	$ roslaunch robot_arm_pkg check_motors_gazebo.launch
```
now to interact with each joint of the robot while RViz and Gazebo is running in the background


https://user-images.githubusercontent.com/85321139/122163031-375ce200-ce7d-11eb-8e5b-4505823455c9.mp4




```bash
	$ rosrun robot_arm_pkg joint_states_to_gazebo.py
```
*Note: to change the permission*
```bash
	$ cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
	$ sudo chmod +x joint_states_to_gazebo.py
```

to visualize the ROS graph of application components use `rqt_graph` command

![rqt_graph command](https://github.com/AlolyanRoaa/ROS-PreparingWith-ArduinoRobotArmpkg/blob/main/4-simulation%20%26%20Controlling%20the%20motors%20joint_state_publisher/4-rqt_qraph.PNG)




## 5-Creating the manipulation with MoveIt

start by loading the moveit assistant 
```bash
	$ roslaunch moveit_setup_assistant setup_assistant.launch
```
a dialog will appears, create manipulation and define the virtual frame.
the run moveit_pkg in Rviz and Gazebo
```bash
	$ roslaunch moveit_pkg demo.launch
	$ roslaunch moveit_pkg demo_gazebo.launch
```

![moveit_pkg in Rviz and Gazebo](https://github.com/AlolyanRoaa/ROS-PreparingWith-ArduinoRobotArmpkg/blob/main/5-Creating%20the%20manipulation%20with%20MoveIt/5-gazebo%20and%20moveit.PNG)

