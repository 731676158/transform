cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

set(CMAKE_CXX_STANDARD 14)
add_compile_options(-std=c++11)

project(concatenate_clouds)

find_package(PCL 1.2 REQUIRED)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

add_executable (concatenate_clouds concatenate_clouds.cpp)
target_link_libraries (concatenate_clouds ${PCL_LIBRARIES})