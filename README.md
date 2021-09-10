# Ifollow_second_project
The gole of the project is to simplify the time consiption for the bigeners in ROS navigation 

 I have used ros noetic and turtlebot3 for the project
 
 for more information about the rules 
 
 1.Setup gazebo simulation
 2.turtlebot robot location
 3.Localization & Mapping
 4.Navigation
 5.python script to automate navigation
 
 1.setup gazebo simulation
 For my project i have set up turtlebot3 gazebo simulation
 Install simulation package 
 $ cd ~/catkin_ws/src/
 $ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
 $ cd ~/catkin_ws && catkin_make

TurtleBot3 World
 $ export TURTLEBOT3_MODEL=waffle
 $ roslaunch turtlebot3_gazebo turtlebot3_world.launch

To operate turtlebot3
 $ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

2.This is the way to create yous own locatization package 
 Turtlebot robot localition 
 for robot_localization
 cd catkin_ws/src
 catkin_create_pkg turtlebot3_localization
 cd robot_localization_turtlebot3
 mkdir config
 touch ekdf_localization.yaml
 mkdir launch
 touch start_filter.launch

 To configure Rviz.
 Launch
 $ roslaunch turtlebot3_gazebo turtlebot3_world.launch
 in other termenal 
 $ rosrun rviz rviz
 Add robot modal
 Add laser sensor
 Add odomantary and duplicate it chance first odom topic in to odom and second odom topic to filtred odom
 Add path planing and duplicate it rename in to globel planer and local planer an change the topic in to move base 
 Add map and duplicate it rename it in to globlcostmape and localcostmape and chance the topic in to globle for globlecostmape and change the topic int local to localcostmap
 and add the tf
 And save the config rviz
 
 
 cd catkin_ws
 catkin_make

to check your odomantere
 rostopic echo -n1 /odom
and to check the package
 roslaunch turtlebot3_localization start_filter.launch


3.Localization & Mapping

Run slam node
 $ roscore
 $ export TURTLEBOT3_MODEL=waffle
 $ roslaunch turtlebot3_slam turtlebot3_slam.launch

Run Teleoperation Node(to move your robot using keybord)
 $ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
map_update_intrerval
save the mape 
 $ rosrun map_server map_saver -f ~/map (f is the folder location)


4.Navigation
 $ roscore
 $ export TURTLEBOT3_MODEL=waffle
 $ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml

set navigation goal


 5.python script to automate navigation
 
 roscore
 cd catkin_ws
 
  $ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml

  $ rosrun nav paridi.py

Q1
move_base_flex is the backwards-compatible replacement for move_base.it can use existing plugins for move_base,and provides an enhanced version of the planner,controlling and recovering,providing detailed information of the current state and the plugin's feedback

Q2
It is depending up the environments if it is closed environments like room,warehouse it is posible is not posible in th open environments.
laser odometry algorithm is better than point to plane odometry

Q3
local planners provide collision avoidance however global planners do not ! also local planner works with the information it gets from the sensor and plans a path around a meter long .
In the global planning stage I try to find a collision free kinematically feasible path from start to goal while skipping the differential or dynamic constraints (so this is where obstacle avoidance should be happening) 
In the local planning stage, I use path smoothing to meet the differential/dynamic constraints



 




