# Thymar project

## Requirements

- `thymio_description` package (already intalled on the VM):
  1. `cd catkin_ws/src/`
  2. `git clone https://github.com/jeguzzi/ros-aseba.git`
  3. **Important: in `base.urdf.xarco` inside the Thymar package replace the line `<odometrySource>encoder</odometrySource>` with `<odometrySource>world</odometrySource>`**
  
- `velodyne` plugin (to be installed):
  1. `cd catkin_ws/src/`
  2. `git clone https://bitbucket.org/DataspeedInc/velodyne_simulator.git`
  
- `ros_pcl` (to be installed):
  1. `cd catkin_ws/src/`
  2. `git clone https://github.com/ros-perception/perception_pcl.git`
  
  

## How to Install

To install the Thymar package, after the requirements have been satisfied:
1. `cd catkin_ws/src/`
2. `git clone https://github.com/seandi/thymar.git`
3. `catkin build`
4. `re.`



## Overview

The repo contains the ROS packages for the Thymar robot. Inside the project folder there are two packages: 
1. the `thymar_description` package contains all the models and launch files for simulating the robot in Gazebo
1. the `thymar_lidar` package performs LIDAR computations and publishes the rostopics to be shown in RViz
2. the `thymar` package contains the scripts for controlling the robot, see [readme](thymar/README.md)



### How to run

The Gazebo simulation of the Thymar robot can be launched as follows (with or without the GUI):  
`roslaunch thymar_description thymar_gazebo_bringup.launch name:=thymar gui:=false world:=indoor_1`  

Launch the main script that actually controls the robot movements:  
`rosrun thymar Thymar.py _name:=thymar`

Finally, launch the node processing the LIDAR Point Cloud, which will automatically also starts RViz for visualizing the result:  
`roslaunch thymar_lidar lidar_processor.launch name:=thymar`  

### Lidar configurations
Two configurations for the lidar have been found to provide good performance
1. Faster terrain coverage: set `hz="0.33" lasers="80"` in `~/catkin_ws/src/thymar/thymar_description/urf/'
2. Faster pointcloud update: set `hz="0.50" lasers="64"` in `~/catkin_ws/src/thymar/thymar_description/urf/'





## Worlds

This is a list of currently available worlds:
- empty
- arena
- easy_1
- easy_2
- easy_3
- indoor_1
- indoor_2
- indoor_3
- outdoor_1
- outdoor_2
- outdoor_3

In `thymar_description/launch/models`, some useful models can be found for creating custom worlds. In order to work properly, the project needs a world which maximum size is 20x20 and that is completely closed (so the robot cannot exit from the world and keep going infinitely).

The image shows some of the worlds listed above.
![Available worlds](https://i.imgur.com/v3mFKZF.png)
