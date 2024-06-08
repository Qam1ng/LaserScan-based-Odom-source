# LaserScan-based-Odom-source
We are discussing if LaserScan based Odom source can replace IMU based odom, rf2o_laser_odometery and laser_scan_matcher are discussed here

# USING 2024 UW Engine Capstone Project Autonomous Self-Driving Wheelchair(Sponsored by Cyberworks Robotics) as an example to test this possibility

ASDW Map and Navigation documentation 


Abnormal Occupancy Grid Map ROS package installation: 

On the engine pc, clone the repo to project directory (under /src folder): git clone https://github.com/AirOllie/OGMD-ROS.git 

Create the ROS package: catkin_create_pkg ogmd rospy std_msgs sensor_msgs 

Copy the files from the repository to the package. Make sure that models and best_acc_ckpt.pth are in the same directory as the test_map_quality.py file. 

Make sure that models and best_acc_ckpt.pth are in the same directory as the test_map_quality.py file: chmod +x test_map_quality.py 

Build the package: cd ~/catkin_ws; catkin_make 

Make sure roscore is running: roscore 

Run map quality detection node: Before running the code, either publish the occupancy grid map to the topic /occupancy_map or save it to occupancy_map.pgm in the same directory as the test_map_quality.py file, then run: rosrun ogmd test_map_quality.py. The detected map quality, either Normal or Abnormal, will be published to /map_quality topic 

SLAM Navigation Setup: 

Locate the catkin_2023 workspace, find the nav_pkg 

We are using move_base to do the SLAM navigation, the launch file nav_movebase.launch in the nav_pkg is the corresponding launch file 

To edit move_base’s costmap, planner or recovery behavior, please check the configs folder inside the nav_pkg 

To edit move_base’s map file, we have put our maps in the /catkin_2023/src/slam_pkg/maps folder 

Before launching navigation launch file, you need to setup the LiDAR 

 
Mapping Setup: 

Locate the catkin_2023 workspace, find the slam_pkg 

We are using slam_toolbox to do the mapping, for its parameters meaning or more detailed information, please see slam_toolbox ros wiki 

We are using rf2o_laser_odometery and laser_scan matcher as our odom source, it requires /scan data input, for more information please see these two packages’ ros wiki. We recommend you to use rf2o according to our test results, and you can try to upgrade it to srf_laser_odometery if you want 

Both rf2o and LSM packages are located in the catkin_2023 folder 

rf2o (https://github.com/MAPIRlab/rf2o_laser_odometry.git)
LSM (https://github.com/NKU-MobFly-Robotics/laser_scan_matcher.git)

The current mapping launch file we use is the buildmap_lidar.launch 

To do test between different odom sources and compare their fluency, use evo_traj package, also located in catkin_2023 (https://github.com/MichaelGrupp/evo/wiki/evo_traj)

 

LiDAR Setup: 

Open terminal, type “sudo ifconfig enp112s0 192.168.198.1 netmask 255.255.255.0” 

For more LiDAR support, you can leave a message on Richbeam;s official website, their customer support will soon contact you, if you have a WeChat; The model is Lakibeam LiDAR 1L Richbeam 

To adjust LiDAR parameters, we have the lakibeam ros package located in the catkin_2023 folder, you can use that as a reference. 

 

P.S. 

Odom source parameters:  

#PARAMTERS FOR map0522rooms_rf2o.txt 

#PARAMTERS FOR map0522rooms_laserscanmatcher.txt 
