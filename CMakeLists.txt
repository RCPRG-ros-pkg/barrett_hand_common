cmake_minimum_required(VERSION 2.8)
project(barrett_hand_tactile)

find_package(catkin REQUIRED COMPONENTS rtt_ros cmake_modules barrett_hand_msgs eigen_conversions)

find_package(orocos_kdl REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES barrett_hand_tactile
  DEPENDS roscpp geometry_msgs visualization_msgs message_runtime orocos_kdl
  CATKIN_DEPENDS eigen_conversions
)

link_directories(
  ${orocos_kdl_LIBRARY_DIRS}
)

include_directories(include
  ${Boost_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
  ${Eigen_INCLUDE_DIR}
)

add_library(barrett_hand_tactile src/tactile.cpp)
target_link_libraries(barrett_hand_tactile ${catkin_LIBRARIES} ${orocos_kdl_LIBRARIES})

