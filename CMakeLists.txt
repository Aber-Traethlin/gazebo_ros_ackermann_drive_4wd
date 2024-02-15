cmake_minimum_required(VERSION 3.5)
project(gazebo_ros_ackermann_drive_4wd VERSION 0.1)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(nav_msgs REQUIRED)

## Find gazebo
if(POLICY CMP0054)
  cmake_policy(SET CMP0054 NEW)
endif()
find_package(gazebo_dev REQUIRED)

## Find Boost
#find_package(Boost REQUIRED COMPONENTS thread)


include_directories(
  ${GAZEBO_INCLUDE_DIRS}
#  ${Boost_INCLUDE_DIRS}
  include
  )
link_directories(${GAZEBO_LIBRARY_DIRS})

add_library(gazebo_ros_ackermann_drive_4wd SHARED
            src/gazebo_ros_ackermann_drive_4wd.cpp)
ament_target_dependencies(gazebo_ros_ackermann_drive_4wd
  rclcpp
  tf2
  tf2_ros
  tf2_geometry_msgs
  geometry_msgs
  nav_msgs
  )
ament_export_libraries(gazebo_ros_ackermann_drive_4wd)


target_link_libraries(gazebo_ros_ackermann_drive_4wd
#  ${Boost_LIBRARIES}
  ${GAZEBO_LIBRARIES}
  )


install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)

install(TARGETS
  gazebo_ros_ackermann_drive_4wd
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

ament_export_dependencies(std_msgs tf)
ament_export_include_directories(include)
ament_export_libraries(gazebo_ros_ackermann_drive_4wd)

ament_package()
