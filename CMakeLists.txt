
cmake_minimum_required(VERSION 3.16.3)

project("generated_code")

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_EXTENSIONS OFF)

# Find requirements
find_package(fastcdr REQUIRED)
find_package(fastrtps REQUIRED)


message(STATUS "Configuring Time...")
add_library(Time_lib Time.cxx)
target_link_libraries(Time_lib fastcdr fastrtps)

add_executable(Time TimePubSubTypes.cxx TimePublisher.cxx TimeSubscriber.cxx TimePubSubMain.cxx)
target_link_libraries(Time fastcdr fastrtps
        Time_lib )




message(STATUS "Configuring Quaternion...")
add_library(Quaternion_lib Quaternion.cxx)
target_link_libraries(Quaternion_lib fastcdr fastrtps)

add_executable(Quaternion QuaternionPubSubTypes.cxx QuaternionPublisher.cxx QuaternionSubscriber.cxx QuaternionPubSubMain.cxx)
target_link_libraries(Quaternion fastcdr fastrtps
        Quaternion_lib )




message(STATUS "Configuring Point...")
add_library(Point_lib Point.cxx)
target_link_libraries(Point_lib fastcdr fastrtps)

add_executable(Point PointPubSubTypes.cxx PointPublisher.cxx PointSubscriber.cxx PointPubSubMain.cxx)
target_link_libraries(Point fastcdr fastrtps
        Point_lib )




message(STATUS "Configuring Header...")
add_library(Header_lib Header.cxx)
target_link_libraries(Header_lib fastcdr fastrtps)

add_executable(Header HeaderPubSubTypes.cxx HeaderPublisher.cxx HeaderSubscriber.cxx HeaderPubSubMain.cxx)
target_link_libraries(Header fastcdr fastrtps
        Header_lib Time_lib)




message(STATUS "Configuring Pose...")
add_library(Pose_lib Pose.cxx)
target_link_libraries(Pose_lib fastcdr fastrtps)

add_executable(Pose PosePubSubTypes.cxx PosePublisher.cxx PoseSubscriber.cxx PosePubSubMain.cxx)
target_link_libraries(Pose fastcdr fastrtps
        Pose_lib Quaternion_lib Point_lib)




message(STATUS "Configuring PoseStamped...")
add_library(PoseStamped_lib PoseStamped.cxx)
target_link_libraries(PoseStamped_lib fastcdr fastrtps)

add_executable(PoseStamped PoseStampedPubSubTypes.cxx PoseStampedPublisher.cxx PoseStampedSubscriber.cxx PoseStampedPubSubMain.cxx)
target_link_libraries(PoseStamped fastcdr fastrtps
        PoseStamped_lib Header_lib Time_lib Pose_lib Quaternion_lib Point_lib)



