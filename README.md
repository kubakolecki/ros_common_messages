# ROS2 message definitions for visual SLAM - neural depth estimation fusion used in NEU-DEPTH project

This repository contains definitions of ROS2 messages that are used in NEU-DEPTH project. Messages defined here are required
to build following ROS2 packages:

[depth_map_optimizer](https://github.com/kubakolecki/depth_map_optimizer)

[slam_deep_mapper](https://github.com/kubakolecki/slam_deep_mapper)

## Requirements
Building and using of messages defined in this ROS2 package was tested with Linux, ROS2 Jazzy and CMake version >= 4.2

## Building
I assume you already have your ROS2 worksapce. In the workspace you should have your packages located in the `src` directory, which is a standard way to organize ROS2 workspace.
In the terminal go to the workspace main directory and follow the commands below:
```bash
cd src
git clone https://github.com/kubakolecki/ros_common_messages.git
cd ..
colcon build --packages-select ros_common_messages
```

## About the messages
If you want to try NEU-DEPTH with your own data some explanation of GeoreferencedStereoImage message might be needed.
The GeoreferencedStereoImage message is used as an input message in [slam_deep_mapper](https://github.com/kubakolecki/slam_deep_mapper). In NEU-DEPTH we use only left image and we
infer depth maps for left image. The ImageBasedMappingData message published by [slam_deep_mapper](https://github.com/kubakolecki/slam_deep_mapper) and subscribed by [depth_map_optimizer](https://github.com/kubakolecki/depth_map_optimizer)
Both messages contain `sensor_msgs/PointCloud sparse_depth_information` field which is used to provide sparse depth. The way the sparse depth is stored as a PointCloud is as follows:  
- x and y coordinates correspond to column/row pixel location of a map point in the left image  
- z coordinate corresponds to depth of a map point (in meters)
- the uncertainty of map points is written in a `channel[0]`

NEU-DEPTH does not require filling following fields:`pose` 
`camera_matrix_left`, `camera_matrix_right`, `right_to_left_transformation_matrix`. Those are used in some other tests.
The `pose` field is the pose of a stereo camera device estimated by SLAM algorithm. Currently not need for depth map fusion.
`camera_matrix_left` and `camera_matrix_right` are 3 x 3 camera matrices.
`right_to_left_transformation_matrix` is a 4 x 4 transformation matrix that describes extrinsics of a stereo camera system.
