
cmake_minimum_required(VERSION 3.16.3)

project(msgs_idl)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)

# Find requirements
find_package(fastcdr REQUIRED)
find_package(fastrtps REQUIRED)

set(IDL_MSG_DIR ${CMAKE_CURRENT_SOURCE_DIR})

file(GLOB DDS_TYPES_SOURCES_CXX 
    "${IDL_MSG_DIR}/builtin_interfaces/msg/*.cxx"
    "${IDL_MSG_DIR}/geometry_msgs/msg/*.cxx"
    "${IDL_MSG_DIR}/std_msgs/msg/*.cxx"
    "${IDL_MSG_DIR}/custom_msgs/msg/*.cxx")

add_library(${PROJECT_NAME} ${DDS_TYPES_SOURCES_CXX})
target_include_directories(${PROJECT_NAME} PUBLIC ${IDL_MSG_DIR})
target_link_libraries(${PROJECT_NAME} 
        fastcdr 
        fastrtps 
        fastdds::optionparser
)