# kinova_gen3_control_cpp
### Overview

PUTLunarTeam repository for ROS2 package controlling kinova gen3 robotic arm with 7 degrees of freedom

Package created and tested on ROS2 Humble

Project uses kinova Gen 3 robotic arm

### Dependencies

- [kinova_gen3_control_interfaces](https://github.com/ReQ1600/kinova_gen3_control_interfaces)
- [ros2_kortex](https://github.com/Kinovarobotics/ros2_kortex)
- [moveit2](https://github.com/ros-planning/moveit2)
- [moveit_resources](https://github.com/ros-planning/moveit_resources)

### Installing

Source your workspace and install ros2_kortex from Kinovarobotics.
~~~
  sudo apt install ros-$ROS_DISTRO-kortex-bringup
  sudo apt install ros-$ROS_DISTRO-kinova-gen3-7dof-robotiq-2f-85-moveit-config
  sudo apt install ros-$ROS_DISTRO-rmw-cyclonedds-cpp
  RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
~~~

Clone moveit_resources from https://github.com/ros-planning/moveit_resources.git

Source your workspace and make sure vcstool, rosdep and colcon are installed 
#### rosdep
~~~
  sudo apt install python3-rosdep
  sudo rosdep init
  rosdep update
  sudo apt update
  sudo apt dist-upgrade
~~~
#### Colcon with mixin
~~~
  sudo apt install python3-colcon-common-extensions
  sudo apt install python3-colcon-mixin
  colcon mixin add default https://raw.githubusercontent.com/colcon/colcon-mixin-repository/master/index.yaml
  colcon mixin update default
~~~
#### vcstool
~~~
  sudo apt install python3-vcstool
~~~

Then download moveit2:
~~~
  git clone https://github.com/ros-planning/moveit2.git -b $ROS_DISTRO
  for repo in moveit2/moveit2.repos $(f="moveit2/moveit2_$ROS_DISTRO.repos"; test -r $f && echo $f); do vcs import < "$repo"; done
  rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y
~~~

### Building

To build from source, clone the latest version from this and interfaces repository into your colcon workspace and build the package using:
~~~
  cd <your_workspace_name>/src
  git clone https://github.com/ReQ1600/kinova_gen3_control_interfaces.git
  git clone https://github.com/ReQ1600/kinova_gen3_control_cpp.git
  cd ..
  rosdep install --from-paths . --ignore-src
  colcon build --mixin release
~~~
I advise using "--executor sequential" flag for colcon build, but it's not necessary.

### Running

Launch the simulation with kortex's rviz
~~~
  ros2 launch kinova_gen3_7dof_robotiq_2f_85_moveit_config robot.launch.py \
    robot_ip:=yyy.yyy.yyy.yyy \
    use_fake_hardware:=true
~~~
Then ros run the node
~~~
  ros2 run kinova_gen3_control_cpp arm_move_to_point_server
~~~

Then you can move the robot with
~~~
  ros2 action send_goal /move_arm_effector kinova_gen3_control_interfaces/action/MoveArmEffector "{goal_point: {x: <float>, y: <float>, z: <float>}}"
~~~

### Result
~~~
  bool success
~~~

### Feedback
~~~
  string error
  geometry_msgs/Point current_effector_position
	float64 x
	float64 y
	float64 z
~~~

