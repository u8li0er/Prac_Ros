cmake_minimum_required(VERSION 2.8.3)
project(actionlib_tutorials)

find_package(catkin REQUIRED COMPONENTS roscpp actionlib actionlib_msgs)
find_package(Boost REQUIRED COMPONENTS system)

add_action_files(
  DIRECTORY action
  FILES Task.action
)

generate_messages(
  DEPENDENCIES actionlib_msgs std_msgs
)

catkin_package(
  CATKIN_DEPENDS actionlib_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

add_executable(task_server src/task_server_node.cpp)

target_link_libraries(
  task_server
  ${catkin_LIBRARIES}
)

add_dependencies(
  task_server
  ${actionlib_tutorials_EXPORTED_TARGETS}
)


add_executable(task_client src/task_client_node.cpp)

target_link_libraries(
  task_client
  ${catkin_LIBRARIES}
)

add_dependencies(
  task_client
  ${actionlib_tutorials_EXPORTED_TARGETS}
)
