cmake_minimum_required(VERSION 3.5.1)
project(bluefox_mpu9250_ros)
set(CMAKE_BUILD_TYPE Release) # Release, RelWithDebInfo
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -pthread -pg -O2")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}) 
find_package(catkin REQUIRED cmake_modules)
find_package(Eigen REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)

catkin_package(
  DEPENDS Eigen
  CATKIN_DEPENDS roscpp
  INCLUDE_DIRS include
)

set(SRC ${SRC} 
    src/timer.cpp
)

set(includeDirs ${includeDirs} ${CMAKE_CURRENT_BINARY_DIR})
set(includeDirs ${includeDirs} include)

include_directories( ${includeDirs} )
include_directories( ${catkin_INCLUDE_DIRS} )
include_directories( ${Eigen_INCLUDE_DIRS} )

# executables
add_executable(mpu9250_node src/main_mpu9250.cpp ${SRC})
target_link_libraries (mpu9250_node ${catkin_LIBRARIES} ${Eigen_LIBRARIES})