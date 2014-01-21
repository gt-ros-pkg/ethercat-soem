cmake_minimum_required(VERSION 2.8.3)
project(ethercat_soem)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

#######################################
## Declare ROS messages and services ##
#######################################

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs  # Or other packages containing msgs
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
 INCLUDE_DIRS include
 LIBRARIES ethercat_soem
#  CATKIN_DEPENDS other_catkin_pkg
 DEPENDS pthread rt
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(include)

add_library(ethercat_soem
  include/ethercat_soem/osal.h
  include/ethercat_soem/oshw.h
  include/ethercat_soem/nicdrv.h
  include/ethercat_soem/ethercattype.h
  include/ethercat_soem/ethercatsoe.h
  include/ethercat_soem/ethercatprint.h
  include/ethercat_soem/ethercatmain.h
  include/ethercat_soem/ethercatfoe.h
  include/ethercat_soem/ethercatdc.h
  include/ethercat_soem/ethercatconfiglist.h
  include/ethercat_soem/ethercatconfig.h
  include/ethercat_soem/ethercatcoe.h
  include/ethercat_soem/ethercatbase.h
  src/osal.c
  src/oshw.c
  src/nicdrv.c
  src/ethercatsoe.c
  src/ethercatprint.c
  src/ethercatmain.c
  src/ethercatfoe.c
  src/ethercatdc.c
  src/ethercatconfig.c
  src/ethercatcoe.c
  src/ethercatbase.c
)

target_link_libraries(ethercat_soem pthread rt)

add_executable(simple_test scripts/simple_test.c)
add_executable(red_test scripts/red_test.c)
add_executable(firm_update scripts/firm_update.c)
add_executable(eepromtool scripts/eepromtool.c)
add_executable(ebox scripts/ebox.c)
add_executable(aliastool scripts/aliastool.c)
add_executable(slaveinfo scripts/slaveinfo.c)

target_link_libraries(simple_test ethercat_soem)
target_link_libraries(red_test ethercat_soem)
target_link_libraries(firm_update ethercat_soem)
target_link_libraries(eepromtool ethercat_soem)
target_link_libraries(ebox ethercat_soem)
target_link_libraries(aliastool ethercat_soem)
target_link_libraries(slaveinfo ethercat_soem)

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS ethercat_soem ethercat_soem_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_ethercat_soem.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
