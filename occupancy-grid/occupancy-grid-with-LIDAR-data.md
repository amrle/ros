## Occupancy Grid with LIDAR Data

The `hector-mapping` ROS package (Hector SLAM) allows for occupancy grid generation using solely lidar data (odometry is not required). To use this package successfully with the Ouster OS0 LIDAR, its data must be converted from the `pointcloud2` message type to the `laserscan` message type. This is done with the package `pointcloud-to-laserscan`.

### Usage

Install the required dependencies for ROS Noetic:
```bash
sudo apt install ros-noetic-pointcloud-to-lasercloud
sudo apt install ros-noetic-hector-mapping
```
If a rosbag with recorded lidar pointcloud data is being used, run the rosbag in the terminal:
```bash
rosbag play <rosbag> --clock

# To loop the rosbag infinitely, use -l
rosbag play <rosbag> -l --clock
```

Run the launch file:
```bash
roslaunch hector_slam_occupancy_grid.launch
```

Rviz should open automatically and a occupancy map should be generated.
![occupancy-map](https://github.com/amrle/ros/assets/88772825/166f96c4-2aec-4172-bfe9-8b7cf9823a0c)

If real time lidar data is being used, first run the lidar: 

### Troubleshooting Information

If an occupancy map does not appear in Rviz, try the following:

Run `rqt_graph` and check the ROS graph
```bash
rqt_graph
```
The graph should look similar to this:
![rqt-graph](https://github.com/amrle/ros/assets/88772825/9a2cd151-aca8-45e9-a944-ff3b20f9e646)


Check the tf tree with the following:
```bash
sudo apt install ros-noetic-tf2-tools
rosrun tf2_tools view_frames.py
firefox frames.pdf
```
The tf tree should look similar to this:
![tf-tree](https://github.com/amrle/ros/assets/88772825/ebeaea7f-9908-48d6-91fd-2747720ef24c)

If a rosbag is being used, make sure use_sim_time is set to true. 
```bash
rosparam set use_sim_time true
```

### Helpful Resources
- [Hector SLAM Documentation](http://wiki.ros.org/hector_slam)
- [Pointcloud to Laserscan Documentation](http://wiki.ros.org/pointcloud_to_laserscan)
- [Hector SLAM Implementation for the RPLidar](https://github.com/NickL77/RPLidar_Hector_SLAM)
- [Hector SLAM Quickstart](https://github.com/avs2805/hector_slam_quickstart)
