
# ROS Preparing With arduino_robot_arm package

documentation of preparing ROS with arduino_robot_arm package


## Outline:

- Installing & Preparing ROS melodic
- Installing the package **arduino_robot_arm**
- Using Arduino with ROS
- simulation & Controlling the motors `joint_state_publisher`
- Creating the manipulation with MoveIt

  
## 1-Installing & Preparing ROS melodic

Using Ubuntu 18.04 OS run these commands in the terminal:



To setup the machine to accept packages.ros.org
```bash
  sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
Set up the keys.
```bash
  curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```
make sure the Debian package index is updated using `sudo apt update`. Then install the Desktop-Full packages.
```bash
  sudo apt install ros-melodic-desktop-full
```
To setup the environment 
```bash
    echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc source ~/.bashrc
```
install dependencies for building packages
```bash
    sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
and for initialize rosdep to use ROS tools 
```bash
   sudo apt install python-rosdep
   sudo rosdep init
   rosdep update
```




  
