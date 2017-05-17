# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(barrett_hand_common)

find_package(catkin REQUIRED COMPONENTS rtt_ros cmake_modules barrett_hand_controller_msgs eigen_conversions)

find_package(Eigen REQUIRED)
find_package(Boost COMPONENTS thread REQUIRED)
find_package(orocos_kdl REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES barrett_hand_tactile
  DEPENDS roscpp geometry_msgs visualization_msgs message_runtime Eigen orocos_kdl
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

target_link_libraries(barrett_hand_tactile ${catkin_LIBRARIES} ${USE_OROCOS_LIBRARIES} ${orocos_kdl_LIBRARIES} ${kdl_parser_LIBRARIES})
add_dependencies(barrett_hand_tactile ${PROJECT_NAME}_gencpp)

