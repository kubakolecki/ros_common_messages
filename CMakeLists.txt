cmake_minimum_required(VERSION 3.20)
project(ros_common_messages)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/ImageBasedMappingData.msg"
  "msg/GeoreferencedStereoImage.msg"
  "msg/ObjectLocalizationInfo.msg"
  DEPENDENCIES std_msgs sensor_msgs geometry_msgs
)

ament_export_dependencies(rosidl_default_runtime)


#ament_target_dependencies(ros_common_messages
# std_msgs
# sensor_msgs
# geometry_msgs
#)

#install(TARGETS
#  ros_common_messages
#  DESTINATION lib/${PROJECT_NAME})

#rosidl_target_interfaces(ros_common_messages ${PROJECT_NAME} "rosidl_typesupport_cpp")

ament_package()
