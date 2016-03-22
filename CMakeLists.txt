cmake_minimum_required(VERSION 3.5)
project(POCO_TESTING)

option(POCO_TESTING_DBG "Turn debuggin on/off (default ON)" ON)
if(POCO_TESTING_DBG)
 message(STATUS "MSG --- POCO_TESTING_DEBUG is ON: " ${POCO_TESTING_DBG})
endif(POCO_TESTING_DBG)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

if(POCO_TESTING_DBG)
 message(STATUS "MSG --- CMAKE_BUILD_TYPE: " ${CMAKE_BUILD_TYPE})
 message(STATUS "MSG --- CMAKE_CXX_FLAGS: " ${CMAKE_CXX_FLAGS})
endif(POCO_TESTING_DBG)

## Where to find the sources of your aplication
set(APPLICATION_BASE_DIR /opt/git/poco-testing)
if(POCO_TESTING_DBG)
message(STATUS "MSG --- APPLICATION_BASE_DIR: " ${APPLICATION_BASE_DIR})
message(STATUS "MSG --- POCO_TESTING_SOURCE_DIR: " ${POCO_TESTING_SOURCE_DIR})
message(STATUS "MSG --- POCO_TESTING_BINARY_DIR: " ${POCO_TESTING_BINARY_DIR})
message(STATUS "MSG --- CMAKE_CURRENT_SOURCE_DIR: " ${CMAKE_CURRENT_SOURCE_DIR})
endif(POCO_TESTING_DBG)

## Target
set(POCO_TESTING_SRCS main.cpp application_server.cpp)
add_executable(appsrv ${POCO_TESTING_SRCS} )
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

## Link libraries
find_library(POCO_FOUNDATION PocoFoundation PATHS /usr/local/lib)
find_library(POCO_UTIL PocoUtil)
find_library(POCO_NET PocoNet)
target_link_libraries(appsrv ${POCO_FOUNDATION} ${POCO_UTIL} ${POCO_NET})


##########################################################
# Function to handle C++ server pages code generation
# It basically calls the cpspc tool from the Poco libraries and generates
# the corresponding .cpp and .h file in the build directory
# Adapted from http://www.cmake.org/pipermail/cmake/2010-June/037733.html

#find_program(CPSPC_EXECUTABLE cpspc)
#function(preprocess_cpsp out_var)
#  set(result)
#  foreach(file ${ARGN})
#    get_filename_component(basename ${file} NAME_WE)
#    set(cpsp "${CMAKE_CURRENT_SOURCE_DIR}/${file}")
#    set(cpp  "${CMAKE_CURRENT_BINARY_DIR}/${basename}.cpp")
#    set(h    "${CMAKE_CURRENT_BINARY_DIR}/${basename}.h")
#    add_custom_command(OUTPUT ${cpp} ${h}
#      COMMAND ${CPSPC_EXECUTABLE} -o ${CMAKE_CURRENT_BINARY_DIR} ${cpsp}
#      DEPENDS ${cpsp}
#      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
#      COMMENT "Preprocessing ${file}"
#      VERBATIM
#      )
#    set_source_files_properties(${cpp} PROPERTIES GENERATED 1)
#    set_source_files_properties(${h}   PROPERTIES GENERATED 1)
#    list(APPEND result ${cpp} ${h})
#  endforeach()
#  set(${out_var} "${result}" PARENT_SCOPE)
#endfunction()

## Compile .cpsp files to .cpp
# file(GLOB PAGES_IN RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "${APPLICATION_BASE_DIR}/viewcontroller/*.cpsp")
# preprocess_cpsp(PAGES_OUT ${PAGES_IN})

## Compile model
# file(GLOB APP_SRC RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "${APPLICATION_BASE_DIR}/model/*.cpp")

# add_executable(appsrv ${POCO_APPSERVER_SRCS} ${PAGES_OUT} ${APP_SRC})
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/${APPLICATION_BASE_DIR})

#find_package(Threads REQUIRED)
#target_link_libraries(appsrv ${CMAKE_THREAD_LIBS_INIT})
