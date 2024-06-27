# Autonomous-navigation-and-gmapping-using-gazebo-and-ROS
## Note
  This repository uses ROS-Noetic and gazebo 11.11.0

## Basic Information
This repository aims to perform SLAM on the AWS hospital world using turtlebot3

## Table of Contents
-[Installation](#installation)
- [Instructions](#instructions)
  - [Running The Hospital World in Gazebo](#running-slam)
  - [Teleoperate your bot](#teleoperation)
  - [SLAM and Saving the Map](#saving-the-map)
  - [Loading the Map and autonomous navigation](#loading-the-map)
- [Repository-Usage](#Usage)
- [Repository Structure](#directory-structure)

## Instructions
1. **Clone the repository:-**
   ```
   cd ~/your_ros_workspace/src
   git clone https://github.com/nishant-1-5/Autonoumous-navigation-using-gazebo-and-ROS.git
   ```

3. **Install the dependencies:-**
   Refer to the quick-start of TurtleBot3 Emanuel [here](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/), 
   along with gazebo installation tutorial [Here](https://classic.gazebosim.org/tutorials?cat=guided_b&tut=guided_b1).

4. **Build the workspace**
   ```
   cd ~/your_ros_workspace/src
   catkin_make
   ```

## General Way
_Note:- Make sure to source the workspace and export the turtlebot3 model in each of the terminals by running the following commands:-
  source devel/setup.bash
  export TURTLEBOT3_MODEL=..._
### Running-Slam
To start the Hospital world in gazebo run the following command:
```
roslaunch turtlebot3_gazebo hospital_world.launch
```
Make sure to set the Gazebo enviroment variables for the model and world path, i suggest to manually move the models to the gazebo models directory which is by default
```
~/.gazebo/models
```

### Teleoperation
Run the teleop node
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```
### SLAM and saving the map
With gazebo and tele-op nodes running launch the turtlebot3 slam node with the following command
```
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_method:=gmapping
```
Now the rviz window should open

Move the bot with keyboard and create a map, after finishing creating the map save the map by running the following command
```
rosrun map_server map_saver -f {path}

```
### Loading the saved map and autonomous navigation
1. Run the gazebo world
2. Run the turtlebot3 navigation with
   ```
   roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:={path to your map}
   ```
3. Now select the init and final points of the navigation

## Usage
1. The navigation launch file has been edited to launch the hospital world by default so no need to specify the file path.
2. There are 2 already maps provided in the maps folder by the name of hospital(preffered) and my_world(very scuffed), the hospital map was mapped using [this repo](https://github.com/marinaKollmitz/gazebo_ros_2Dmap_plugin), so navigation can be directly performed with mapping first.
3. Instead of relying on the robot_description parameter being set externally,the URDF of turtlebot3 has been directly embed in the launch file.

## Repository Structure
### Some important files are present in this repository as at following paths
1. The hospital.world file and the models are present at
```
Dataset-of-Gazebo-Worlds-Models-and-Maps/worlds/hospital
```
2. The saved maps are present at
```
turtlebot3/turtlebot3_navigation/maps
```
3. hospital_world.launch
```
turtlebot3_simulations/turtlebot3_gazebo/launch
```


