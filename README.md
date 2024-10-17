# Virtual Obstacle Lane Navigation with Autonomous Mapping
This repository features a custom ROS package, slam_lane_tracking_pkg, designed to enable Turtlebot3 to autonomously navigate an autorace environment by tracking lanes and simultaneously mapping the surroundings. The package equips Turtlebot3 with the ability to follow lanes using camera sensor data, utilizing the cv_bridge package to process images and detect yellow and white lines.

Once the map is created, the robot’s pose data is used to designate the detected lanes as virtual obstacles, ensuring they are avoided during autonomous navigation. 
For more information on "lane tracking" and "how the robot pose data is generated", please refer to the following repository: [autonomous lane tracking.](https://github.com/EhtishamAshraf/turtlebot3_lane_tracking.git)


### Demo Video
You can watch the demo video of Mapping by clicking on the below image
[![Watch the video](https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation/blob/main/src/slam_lane_tracking_pkg/Image/video_image.png)](https://youtu.be/-JGLHBf8EOU)

You can watch the demo video of Navigation by clicking on the below image
[![Watch the video](https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation/blob/main/src/slam_lane_tracking_pkg/Image/navigation.png)](https://youtu.be/vERA8F4Mlvc)

## Gazebo World
Below image shows the Gazebo world used in this project. The world contains white and yellow lines.

![Gazebo World](https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation/blob/main/src/slam_lane_tracking_pkg/Image/simulation_environment.png)

### Note 
1.  Details about cloning the repository are given at the end of this **readme file**

## Lane Tracking Logic & Robot's Movement Control using PD Controller
The logic behind lane tracking algorithm and Robot movement control is explained in detail in the following repo: [autonomous lane tracking.](https://github.com/EhtishamAshraf/turtlebot3_lane_tracking.git)

![Camera Output](https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation/blob/main/src/slam_lane_tracking_pkg/Image/camera_output.png)

## Robot's Pose data
While the robot is tracking a lane, its position and orientation data are continuously recorded in a .txt file. This stored data is later utilized to mark the lanes as virtual obstacles for Autonomous Navigation. The Robot pose data is stored and saved in the previous repo.

## Map Processing
The map created with the Gmapping node doesn't mark lines as obstacles so during the pre-processing the lane is marked as virtual obstacle with the help of the code "map_processing.py"
The original map:
![Original Map](https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation/blob/main/src/slam_lane_tracking_pkg/maps/my_map.pgm)


## Running the Simulation
To run the simulation, there are two options:
A. In order to do the mapping using SLAM, launch the slam_lane_tracking launch file.
B. In order to do the navigation, launch the navigation launch file.
Navigate inside the workspace and then, use either of the following command:

### 1. Mapping
```bash
roslaunch slam_lane_tracking_pkg slam_lane_tracking.launch
```
![Gazebo World](https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation/blob/main/src/slam_lane_tracking_pkg/Image/rviz_output.png)

### 2. Navigation
```bash
roslaunch slam_lane_tracking_pkg navigation.launch
```

### Note: 
I have used cv_bridge, turtlebot3_gazebo, gazebo_ros, gmapping, move_base packages, so plesae download all necessary packages before cloning the repository.

# Clone the repository
```bash
sudo apt-get update
```
```bash
sudo apt-get install git
```
```bash
git clone https://github.com/EhtishamAshraf/virtual_obstacle_lane_navigation.git
```
```bash
cd virtual_obstacle_lane_navigation
```
Run the below commands in root folder of the workspace
```bash
catkin_make 
```
```bash
source devel/setup.bash 
```
Navigate to the Scripts folder inside the package and make the Python files executable by running the following command:
```bash
chmod +x *.py
```

This script is responsible for tracking the lane without saving the robot's pose data.
```bash
lane_tracking.py
```

Now navigate to the launch folder inside the package
```bash
roslaunch slam_lane_tracking.launch
```
or

```bash
roslaunch navigation.launch 
```

## Limitations
- **Narrow Lane Width:** The current implementation of navigation within the lane performs well for short distances and straight paths. However, during turns, the robot may struggle to maneuver effectively due to the limited width of the lane. This constraint can lead to difficulties in maintaining proper alignment and orientation, impacting the overall navigation performance.
  
