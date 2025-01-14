cmake_minimum_required(VERSION 2.8.3)
project(regulated_pure_pursuit_controller)

add_compile_options(-std=c++17)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
        roscpp
        cmake_modules
        base_local_planner
        costmap_2d
        nav_core
        nav_msgs
        pluginlib
        ddynamic_reconfigure
        tf
        mbf_msgs
        mbf_costmap_core
)


include_directories(
        include
        SYSTEM
        ${catkin_INCLUDE_DIRS}
)

#link_directories(${catkin_LIBRARY_DIRS})

catkin_package(
        INCLUDE_DIRS include ${EXTERNAL_INCLUDE_DIRS}
        LIBRARIES regulated_pure_pursuit_controller ${EXTERNAL_LIBS}
        CATKIN_DEPENDS
        base_local_planner
        costmap_2d
	nav_core
	nav_msgs
        pluginlib
        roscpp
        ddynamic_reconfigure
        tf
)

add_library(regulated_pure_pursuit_controller
        src/regulated_pure_pursuit_controller.cpp)

target_link_libraries(regulated_pure_pursuit_controller 
                        ${catkin_LIBRARIES})
add_dependencies(regulated_pure_pursuit_controller nav_msgs_gencpp)

install(TARGETS regulated_pure_pursuit_controller
        #ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        )

install(FILES pure_pursuit_plugin.xml
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
        )

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
        PATTERN ".svn" EXCLUDE
        )