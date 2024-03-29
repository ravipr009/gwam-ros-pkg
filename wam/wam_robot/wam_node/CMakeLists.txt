cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

find_package(Barrett REQUIRED)
link_directories(${BARRETT_LIB_DIRS})
include_directories(${BARRETT_INCLUDE_DIRS})
add_definitions(${BARRETT_DEFINITIONS})
rosbuild_add_executable(wam_node_guardian src/wam_node_guardian.cpp)
rosbuild_add_executable(wam_node_standalone src/wam_node_standalone.cpp)
target_link_libraries(wam_node_guardian ${BARRETT_LIBRARIES})
target_link_libraries(wam_node_standalone ${BARRETT_LIBRARIES})
