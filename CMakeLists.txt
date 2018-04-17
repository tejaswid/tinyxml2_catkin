cmake_minimum_required(VERSION 2.8.3)
project(tinyxml2_catkin)

################################
# set lib version here

set(GENERIC_LIB_VERSION "6.2.0")
set(GENERIC_LIB_SOVERSION "6")

################################
find_package(catkin REQUIRED COMPONENTS)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS
  LIBRARIES tinyxml2_catkin
)

include_directories(include ${catkin_INCLUDE_DIRS})


add_library(tinyxml2_catkin SHARED src/tinyxml2.cpp)

set_target_properties(tinyxml2_catkin PROPERTIES
	VERSION "${GENERIC_LIB_VERSION}"
	SOVERSION "${GENERIC_LIB_SOVERSION}")

if(DEFINED CMAKE_VERSION AND NOT "${CMAKE_VERSION}" VERSION_LESS "2.8.11")
    target_include_directories(tinyxml2_catkin PUBLIC 
                          $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
                          $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include>)
else()
    include_directories(${PROJECT_SOURCE_DIR})
endif()
