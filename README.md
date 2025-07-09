# Multi-Map Navigation Project

## Overview

This project implements a multi-map navigation system in ROS Noetic using `map_server`, `amcl`, `move_base`, and a custom `multi_map_server` built with `actionlib`. It demonstrates:
- Multiple room maps (`room_A.yaml`, `room_B.yaml`) with overlapping wormhole regions.
- A SQLite database (`wormholes.db`) for storing wormhole coordinates.
- A modular C++ ROS node that switches maps dynamically.
- Full localization with AMCL and path planning with Move Base.

---

## Project Structure

multi_map_nav/
├── maps/
│ ├── room_A.yaml
│ ├── room_B.yaml
│ ├── room_A.pgm
│ ├── room_B.pgm
├── src/
│ ├── multi_map_server.cpp
│ └── ...
├── launch/
│ ├── multi_map_nav.launch
│ ├── static_tf.launch
├── wormholes.db
├── README.md


---

## Requirements

- Ubuntu 20.04
- ROS Noetic
- turtlebot3_gazebo (for simulation)
- SQLite3

---

## Setup Instructions

1. Clone the repository:
   git clone https://github.com/anshumaanvats/Multi-map-Navigation-ROS.git
   cd Multi-map-Navigation-ROS

2. Build your workspace:
cd ~/multi_map_ws
catkin_make
source devel/setup.bash

3. Set your TurtleBot3 model if using Gazebo:
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
source ~/.bashrc

---

## Running the System

Option A: Test with TurtleBot3 Gazebo

1. Launch TurtleBot3 in Gazebo:
Launch TurtleBot3 in Gazebo:

2. In a new terminal, launch the multi-map navigation stack:
source ~/multi_map_ws/devel/setup.bash
roslaunch multi_map_nav multi_map_nav.launch

3. In another terminal, start teleoperation:
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

4. Open RViz:
rviz

Option B: Test with a bag file

1. Start static transforms if needed:
roslaunch multi_map_nav static_tf.launch

2. Launch the multi-map nav stack:
roslaunch multi_map_nav multi_map_nav.launch

3. Replay your bag file with /scan and /tf:
rosbag play turtlebot3_scan.bag --loop

4. Open RViz and verify map, scan, and robot pose.

---
