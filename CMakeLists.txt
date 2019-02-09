cmake_minimum_required(VERSION 3.1)

project(udp_broadcast)


set(CMAKE_CXX_FLAGS "${CAMKE_CXX_FLAGS} -std=c++11")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
  std_msgs
  message_generation
)

find_package(Boost REQUIRED COMPONENTS system thread regex)

catkin_package(CATKIN_DEPENDS 
  roscpp 
  sensor_msgs 
  std_msgs 
  message_runtime
)

if(boost_found)
    include_directories(${Boost_INCLUDE_DIRS})
    link_directories(${Boost_LIBRARIES})
endif()
include_directories(
    ${catkin_INCLUDE_DIRS}
    include
    )

add_executable(udp_server src/server_node.cpp)
add_executable(udp_client src/client_node.cpp)

target_link_libraries(udp_server 
    ${Boost_SYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY} ${Boost_REGEX_LIBRARY} ${catkin_LIBRARIES} )

target_link_libraries(udp_client 
    ${Boost_SYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY} ${Boost_REGEX_LIBRARY} ${catkin_LIBRARIES} )
