cmake_minimum_required(VERSION 3.5)
project(txt2pcd)
 
find_package(PCL 1.2 REQUIRED)
 
# 加入Boost setting
find_package(Boost COMPONENTS program_options REQUIRED )
include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIRS})
 
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
 
add_executable(txt2pcd txt2pcd.cpp)
 
target_link_libraries (txt2pcd ${PCL_LIBRARIES} ${Boost_LIBRARIES}) #此处也有修改

