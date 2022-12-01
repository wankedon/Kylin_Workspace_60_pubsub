cmake_minimum_required(VERSION 3.10)

project(ZCZHSubcriber_test C CXX)

#set toolchain
SET(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_PACKAGE ONLY)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()

#设置使用c++14标准
set(CMAKE_CXX_STANDARD 14)

#include_directories(/home/forlinx/Workspace/60_sub/Src)
#LINK_DIRECTORIES(/home/forlinx/Workspace/60_sub/build/lib)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
message(STATUS ${PROJECT_BINARY_DIR})

aux_source_directory(. SRC_LIST)

#file(GLOB LIB_CZMQ_LIST "/usr/local/lib/lib*.a*")#czmq
#file(GLOB LIB_LIST "/home/forlinx/Workspace/vcpkg/installed/x64-linux/lib/lib*.a*")#vcpkg

#add_executable(ZCZHSubcriber_test ${SRC_LIST} ${LIB_CZMQ_LIST} ${LIB_LIST})
#target_link_libraries(ZCZHSubcriber_test ZCZHSubcriber ${LIB_CZMQ_LIST} ${LIB_LIST} pthread dl)

file(GLOB LIB_LIST "${PROJECT_SOURCE_DIR}/lib/lib*.a*")
add_executable(ZCZHSubcriber_test ${SRC_LIST} ${LIB_LIST})
target_link_libraries(ZCZHSubcriber_test ${LIB_LIST} pthread dl)



