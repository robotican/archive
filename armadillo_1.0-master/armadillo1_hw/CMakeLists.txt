cmake_minimum_required(VERSION 2.8.3)
project(armadillo1_hw)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

find_package(
    catkin REQUIRED COMPONENTS
    roscpp
    rospy
    controller_manager
    dxl_interface
    ric_interface
    roboteq_control
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES armadillo1_hw
  CATKIN_DEPENDS
        dxl_interface
        roboteq_control
        ric_interface
DEPENDS
    Boost
#  DEPENDS system_lib
)

include_directories(
 include
 ${catkin_INCLUDE_DIRS} ${yaml-cpp_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS}
)

 add_executable(${PROJECT_NAME}_node
                src/armadillo1_hw.cpp
                include/armadillo1_hw.h
         src/armadillo1_hw_node.cpp
         src/dxl_motors_builder.cpp
         include/dxl_motors_builder.h
         src/ricboard_pub.cpp
         include/ricboard_pub.h
         src/roboteq_diff_drive.cpp
         include/roboteq_diff_drive.h)

add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
 target_link_libraries(
         ${PROJECT_NAME}_node
        ${catkin_LIBRARIES}
 )