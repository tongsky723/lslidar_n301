# lslidar_n301

# version track
Author: Yutong

## Ver2.0 Yutong
 - Add use_gps_ts param to use GPS timestamp for LaserScan message
 - Add skip_num param to skip certain points, it can actually minimize LaserScan data
 - Add truncated_mode param to select using which method to truncate laser data, cut off specific angle ranges or certain radius range


# Description
The `lslidar_n301` package is a linux ROS driver for lslidar n301.
The package is tested on Ubuntu 14.04 with ROS indigo.
The package is tested on Ubuntu 16.04 with ROS kinetic.

# Compling
This is a Catkin package. Make sure the package is on `ROS_PACKAGE_PATH` after cloning the package to your workspace. And the normal procedure for compling a catkin package will work.

```
cd your_work_space
catkin_make 
```

# Example Usage
`roslaunch lslidar_n301_decoder lslidar_n301.launch --screen`

# ROS 
## lslidar_n301_driver

### Parameters

- `device_ip` (`string`, `default: 192.168.1.222`)
	By default, the IP address of the device is 192.168.1.200.

- `frame_id` (`string`, `default: laser`)
	The frame ID entry for the sent messages.

### Published Topics

- `lslidar_packets` (`lslidar_n301_msgs/Lslidarn301Packet`)
	Each message corresponds to a lslidar packet sent by the device through the Ethernet.


## lslidar_n301_decoder

### Parameters 

- `min_range` (`double`, `0.15`)

- `max_range` (`double`, `150.0`)
	Points outside this range will be removed.

- `frequency` (`frequency`, `10.0`)
	Note that the driver does not change the frequency of the sensor. 

- `publish_point_cloud` (`bool`, `true`)
	If set to true, the decoder will additionally send out a local point cloud consisting of the points in each revolution.

- `point_num` (`int`, `2000`)
	Points number of one scan

- `skip_num` (`int`, `0`)
	Skip numbers in LaseScan ranges data

- `angle_disable_min` (`int`, `0`)
	Set ranges data to 0 when its corresponding angle less than this value 

- `angle_disable_max` (`int`, `0`)
	Set ranges data to 0 when its corresponding angle larger than this value 

- `truncated_mode` (`int`, '0') 
	Using which method to truncate laser data, 0 is cut off specific angle ranges ; 1 is cut off certain radius range

- `invalid_radius` (`double`, `0.0`)
	Useful when setting truncated_mode to 1. All ranges data within this radius will set to infinity

- `disable_min` (`list`, `[]`)
	Useful when setting truncated_mode to 0. All ranges data between disable_min and disable_max will set to infinity

- `disable_min` (`list`, `[]`)
	Useful when setting truncated_mode to 0. All ranges data between disable_min and disable_max will set to infinity

- `disable_tolerance` (`int`, `5`)
	Useful when setting truncated_mode to 0. disable_min and disable_max can be expand with this tolerance

### Published Topics

- `lslidar_sweep` (`lslidar_N301_msgs/LslidarN301Sweep`)
	The message arranges the points within each sweep based on its scan index and azimuth.

- `lslidar_point_cloud` (`sensor_msgs/PointCloud2`)
	This is only published when the `publish_point_cloud` is set to `true` in the launch file.

- `scan` (`sensor_msgs/LaserScan`)
	Standard LaserScan message type with topic name scan








