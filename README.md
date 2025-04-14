# bot_description

This repository contains the **bot_description** package, developed using ROS2 Humble in a Catkin-like workspace environment. This package is part of my submission for Ogmen Robotics and demonstrates my ability to build and test robot description and simulation packages. In this package, I created a robot model based on a provided mechanical engineering drawing, set up multiple launch files for visualization, simulation, and teleoperation, and integrated various sensors and drive systems.

---

## Overview of Tasks

- **Workspace & Package Creation:**  
  I started by creating a new workspace named `gowtham_ws`, following the familiar Catkin structure used in ROS1. Within this workspace, I generated a package called **bot_description** inside the `src` directory using the ROS2 command-line tools.

- **Building the Robot Description (URDF/Xacro):**  
  Using the mechanical engineering drawing provided, I developed a complete URDF of the robot.  
  - The URDF was written using XACRO for modularity and ease of parameterization.
  - It defines the robot as a differential drive system, featuring left and right wheel joints.
  - The model includes a Lidar sensor and an RGB camera, each integrated with appropriate Gazebo plugins to simulate sensor behavior.

- **RViz Visualization Launch File:**  
  In the **bot_description/launch** directory, I created `rviz.launch.py`. This launch file processes the XACRO file, launches the `robot_state_publisher` to broadcast the robot description, and opens RViz (with a preset configuration that sets the Fixed Frame to `base_link` and displays the robot model based on the `robot_description` topic).

- **Gazebo Spawn Launch File:**  
  I developed another launch file named `spawn.launch.py` within the same **launch** folder. This launch file:
  - Includes the RViz launch file to allow simultaneous visualization.
  - Launches Gazebo with a custom world (located in `worlds/hospital.world`).
  - Uses a TimerAction to delay the spawning of the robot (allowing Gazebo’s plugins to initialize) and then spawns the robot into the simulation using the `spawn_entity.py` node.

- **Differential Drive, Lidar, and RGB Camera Integration:**  
  The URDF reflects the robot’s capabilities:
  - It is designed as a differential drive system, with proper joint definitions for independent wheel control.
  - A Lidar sensor and an RGB camera have been added as separate links, with corresponding Gazebo plugins specified for simulating sensor output.

- **Teleoperation Launch File:**  
  Finally, to enable control via keyboard commands, I created a launch file named `control.launch.py` in **bot_description/launch**. This file:
  - Launches the GUI version of the joint state publisher (`joint_state_publisher_gui`), allowing interactive joint visualization.
  - Launches the `teleop_twist_keyboard` node (using an xterm window so that keyboard input is captured properly), enabling the user to control the robot via keyboard commands.

---

## How to Test the Packages

### Prerequisites

Ensure the following are installed:
- **ROS2 Humble**
- Required ROS2 packages:
  - `gazebo_ros`
  - `rviz2`
  - `robot_state_publisher`
  - `joint_state_publisher_gui`
  - `teleop_twist_keyboard`


**Build the Workspace:**

   ```bash
   cd ~/gowtham_ws
   colcon build --symlink-install
