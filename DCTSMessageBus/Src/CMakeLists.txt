##############aux_source_directory(. SRC_LIST)
option(arm64 "This is a option for arm64" OFF)

include_directories(./)
include_directories(${PROJECT_SOURCE_DIR}/Utility)
include_directories(${PROJECT_SOURCE_DIR}/PchHeader)
include_directories(${PROJECT_SOURCE_DIR}/ConfigLoader)
include_directories(${PROJECT_SOURCE_DIR}/Proto)
include_directories(${PROJECT_SOURCE_DIR}/DistComm)

file(GLOB_RECURSE SRC_LIST "*.c*")
file(GLOB_RECURSE CONFIG_LIST ${PROJECT_SOURCE_DIR}/ConfigLoader/*.cpp)
file(GLOB_RECURSE DISTCOMM_LIST ${PROJECT_SOURCE_DIR}/DistComm/*.cpp)
file(GLOB_RECURSE HEADER_LIST ${PROJECT_SOURCE_DIR}/PchHeader/*.cpp)
file(GLOB_RECURSE PROTO_LIST ${PROJECT_SOURCE_DIR}/Proto/*.cc)
file(GLOB_RECURSE UTILITY_LIST ${PROJECT_SOURCE_DIR}/Utility/*.cpp)

#if(arm64)
#file(GLOB LIB_CZMQ_LIST "/home/forlinx/Workspace/czmq/installed/lib/lib*.a*")#czmq
#file(GLOB LIB_LIST "/home/forlinx/Workspace/vcpkg/installed/arm64-linux/lib/lib*.a*")#vcpkg
#else()
#file(GLOB LIB_CZMQ_LIST "/usr/local/lib/lib*.a*")#czmq
#file(GLOB LIB_LIST "/home/forlinx/Workspace/vcpkg/installed/x64-linux/lib/lib*.a*")#vcpkg
#endif()
file(GLOB LIB_LIST "${PROJECT_SOURCE_DIR}/lib/lib*.a*")#vcpkg

add_executable(DCTSMessageBus ${SRC_LIST} ${PROTO_LIST} ${DISTCOMM_LIST} ${UTILITY_LIST} ${HEADER_LIST} ${CONFIG_LIST})
#target_link_libraries(DCTSMessageBus ${LIB_CZMQ_LIST} ${LIB_LIST} ${_PROTOBUF_LIBPROTOBUF} dl)
target_link_libraries(DCTSMessageBus ${LIB_LIST} dl pthread)  
