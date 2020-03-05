cmake_minimum_required(VERSION 2.8.3)
project(object_search_project)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  frontier_exploration
  grid_map_core
  grid_map_msgs
  grid_map_ros
  nav_msgs
  roscpp
  sensor_msgs
  tf
)

find_package( OpenCV REQUIRED )

catkin_package()

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)


add_executable(search_controller_node src/search_controller.cpp)
add_executable(search_manager src/search_manager_node.cpp src/SearchManager.cpp)


target_link_libraries(search_controller_node
  ${catkin_LIBRARIES}
)

target_link_libraries(search_manager
  ${catkin_LIBRARIES}
)


install(DIRECTORY launch
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(DIRECTORY image_rec
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)


install(DIRECTORY include
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(DIRECTORY rviz
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(DIRECTORY config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(TARGETS search_controller_node search_manager 
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
