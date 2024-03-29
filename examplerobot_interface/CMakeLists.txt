cmake_minimum_required(VERSION 3.0.2)
project(examplerobot_interface)
#cmake_minimum_required(VERSION 3.1.3)
#project(moveit_tutorials)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(catkin REQUIRED
  COMPONENTS
    interactive_markers
    moveit_core
    moveit_ros_planning
    moveit_ros_planning_interface
    moveit_ros_perception
    moveit_visual_tools
    moveit_servo
    rviz_visual_tools
    pluginlib
    geometric_shapes
   #pcl_ros
   #pcl_conversions
    rosbag
    tf2_ros
    tf2_eigen
    tf2_geometry_msgs
)

find_package(Eigen3 REQUIRED)
find_package(Boost REQUIRED system filesystem date_time thread)

set(THIS_PACKAGE_INCLUDE_DIRS
  doc/interactivity/include
)

catkin_package(
  LIBRARIES
  INCLUDE_DIRS
  CATKIN_DEPENDS
    moveit_core
    moveit_visual_tools
    moveit_ros_planning_interface
    interactive_markers
    tf2_geometry_msgs
  DEPENDS
    EIGEN3
)

###########
## Build ##
###########

include_directories(${THIS_PACKAGE_INCLUDE_DIRS})
include_directories(SYSTEM ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIR} ${EIGEN3_INCLUDE_DIRS})

#############
## Compile ##
#############

add_executable(examplerobot_interface_ompl src/examplerobot_interface_ompl.cpp)
target_link_libraries(examplerobot_interface_ompl ${catkin_LIBRARIES} ${Boost_LIBRARIES})
install(TARGETS examplerobot_interface_ompl DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

add_executable(examplerobot_interface_servo src/examplerobot_interface_servo.cpp)
target_link_libraries(examplerobot_interface_servo ${catkin_LIBRARIES} ${Boost_LIBRARIES})
install(TARGETS examplerobot_interface_servo DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})