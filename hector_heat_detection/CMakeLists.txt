# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
project(hector_heat_detection)
# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS roscpp rospy image_transport camera_info_manager hector_worldmodel_msgs sensor_msgs cv_bridge std_msgs image_transport dynamic_reconfigure argo_vision_msgs nodelet)

#find_package(OpenCV REQUIRED)
include_directories(include ${catkin_INCLUDE_DIRS})
# CATKIN_MIGRATION: removed during catkin migration
# cmake_minimum_required(VERSION 2.4.6)

# CATKIN_MIGRATION: removed during catkin migration
# include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE Debug)


# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_init()

#set the default path for built executables to the "bin" directory
#set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
#set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#add_message_files(
#  FILES
  # TODO: List your msg files here
#)
#uncomment if you have defined services
#add_service_files(
#  FILES
  # TODO: List your msg files here
#)

#common commands for building c++ executables and libraries
#add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)

#
# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_add_boost_directories()
#find_package(Boost REQUIRED COMPONENTS thread)
#include_directories(${Boost_INCLUDE_DIRS})
#target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES})
#add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})

#add dynamic reconfigure api
#rosbuild_find_ros_package(dynamic_reconfigure)
#include(${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake)
#gencfg()

generate_dynamic_reconfigure_options(cfg/HeatDetection.cfg)

add_library(heat_detection src/heat_detection.cpp)
add_dependencies(heat_detection ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(heat_detection ${catkin_LIBRARIES})

add_executable(heat_detection_node src/heat_detection_node.cpp)
target_link_libraries(heat_detection_node heat_detection)

add_library(heat_detection_nodelet src/heat_detection_nodelet.cpp)
target_link_libraries(heat_detection_nodelet heat_detection)


#TODO: Define non-absolute include path
#Teporary includes of opencv with sse3 disabled
#target_link_libraries(${PROJECT_NAME} /home/konstantin/opencv/opencv2.3_bin/lib/libopencv_highgui.so)
#target_link_libraries(${PROJECT_NAME} /home/konstantin/opencv/opencv2.3_bin/lib/libopencv_imgproc.so)
#target_link_libraries(${PROJECT_NAME} /home/konstantin/opencv/opencv2.3_bin/lib/libopencv_features2d.so)
## Generate added messages and services with any dependencies listed here
#generate_messages(
    #TODO DEPENDENCIES geometry_msgs std_msgs
#)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS roscpp rospy image_transport camera_info_manager hector_worldmodel_msgs sensor_msgs cv_bridge std_msgs image_transport dynamic_reconfigure argo_vision_msgs
    CATKIN_DEPENDS # TODO
    INCLUDE_DIRS # TODO include
    LIBRARIES # TODO
)
