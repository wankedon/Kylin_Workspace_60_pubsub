cmake_minimum_required(VERSION 3.10)

project(DCTSMessageBus C CXX)
option(arm64 "This is a option for arm64" OFF)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Debug")#Release
endif()

#设置使用c++14标准
set(CMAKE_CXX_STANDARD 14)

#set toolchain
SET(CMAKE_SYSTEM_NAME Linux)
if(arm64)
 SET(CMAKE_SYSTEM_PROCESSOR aarch64)
 set(CMAKE_STAGING_PREFIX /home/forlinx/Workspace/grpc-stage)
 set(CMAKE_C_COMPILER /usr/bin/aarch64-linux-gnu-gcc-7)
 set(CMAKE_CXX_COMPILER /usr/bin/aarch64-linux-gnu-g++-7)
 message(STATUS "Build Arm-x64 Version Project")
else()
 message(STATUS "Build Linux-x64 Version Project")
endif()
set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_PACKAGE ONLY)

find_package(Threads REQUIRED)

# Find Protobuf
#if(arm64)
# set(Protobuf_DIR /home/forlinx/Workspace/grpc-stage/lib/cmake/protobuf) 
#else()
# set(Protobuf_DIR /usr/local/lib/cmake/protobuf) 
#endif()
#set(protobuf_MODULE_COMPATIBLE TRUE)
#find_package(Protobuf CONFIG REQUIRED)
#message(STATUS "Using protobuf ${Protobuf_VERSION}")
#set(_PROTOBUF_LIBPROTOBUF protobuf::libprotobuf)
#set(_REFLECTION gRPC::grpc++_reflection)
#if(CMAKE_CROSSCOMPILING)
#  find_program(_PROTOBUF_PROTOC protoc)
#else()
#  set(_PROTOBUF_PROTOC $<TARGET_FILE:protobuf::protoc>)
#endif()

#add definitions
add_definitions(-DZMQ_BUILD_DRAFT_API)
add_definitions(-DCZMQ_BUILD_DRAFT_API)
add_definitions(-DPUGIXML_WCHAR_MODE)

#project directory
#if(arm64)
#include_directories(/home/forlinx/Workspace/czmq/installed/include)#czmq
#include_directories(/home/forlinx/Workspace/vcpkg/installed/arm64-linux/include) #vcpkg
#else()
#include_directories(/usr/local/include)#czmq
#include_directories(/home/forlinx/Workspace/vcpkg/installed/x64-linux/include) #vcpkg
#endif()
include_directories(${PROJECT_SOURCE_DIR}/include) #vcpkg

include_directories(${PROJECT_SOURCE_DIR}/ConfigLoader)
include_directories(${PROJECT_SOURCE_DIR}/DistComm)
include_directories(${PROJECT_SOURCE_DIR}/PchHeader)
include_directories(${PROJECT_SOURCE_DIR}/Proto)

#link_directories
#if(arm64)
#LINK_DIRECTORIES(/home/forlinx/Workspace/czmq/installed/lib)#czmq
#LINK_DIRECTORIES(/home/forlinx/Workspace/vcpkg/installed/arm64-linux/lib)#vcpkg
#else()
#LINK_DIRECTORIES(/usr/local/lib)#czmq
#LINK_DIRECTORIES(/home/forlinx/Workspace/vcpkg/installed/x64-linux/lib)#vcpkg
#endif()
LINK_DIRECTORIES(${PROJECT_SOURCE_DIR}lib)#vcpkg

#LINK_DIRECTORIES(${PROJECT_SOURCE_DIR}/lib)
#LINK_DIRECTORIES(${PROJECT_BINARY_DIR}/lib)

#set ouput path
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

#add subdirectory
add_subdirectory(Src)
