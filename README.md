# lunarteam-soft
### Overview

This is a repository created as a temporary repository for PUTLunarTeam software team. Everything is bound to change.

All packages are created and tested on ROS2 Humble
Project uses kinova Gen 3 robotic arm

### Dependencies

ros2_kortex
moveit2
moveit_resources
ros2_robotiq_gripper

### Installing
Install ros2_kortex from Kinovarobotics on github (https://github.com/Kinovarobotics/ros2_kortex) do what readme tells you to do.
Clone moveit_resources from https://github.com/ros-planning/moveit_resources.git
Clone ros2_robotiq_gripper from https://github.com/PickNikRobotics/ros2_robotiq_gripper.git
Download moveit2
~~~
  git clone https://github.com/ros-planning/moveit2.git -b $ROS_DISTRO
  for repo in moveit2/moveit2.repos $(f="moveit2/moveit2_$ROS_DISTRO.repos"; test -r $f && echo $f); do vcs import < "$repo"; done
  rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y
~~~

### Building

To build from source, clone the latest version from this repository into your colcon workspace and build the package using:
~~~
  cd <your_workspace_name>/src
  git clone https://github.com/ReQ1600/lunarteam-soft.git
  cd ..
  rosdep install --from-paths . --ignore-src
  colcon build
~~~

### Docker
To be added
