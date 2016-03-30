cmake_minimum_required(VERSION 3.5)
project(SANDBOX)

option(SANDBOX_DBG "Turn debuggin on/off (default ON)" ON)

if(SANDBOX_DBG)
 message(STATUS "MSG --- SANDBOX_DEBUG is ON: " ${SANDBOX_DBG})
 set(CMAKE_BUILD_TYPE Debug)
else()
 message(STATUS "MSG --- SANDBOX_DEBUG is OFF: " ${SANDBOX_DBG})
 set(CMAKE_BUILD_TYPE Release)
endif(SANDBOX_DBG)

# Global output binary directory locations
if(SANDBOX_DBG)
  set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/dbg/lib)
  set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/dbg/lib)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/dbg/bin)
else()
  set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
  set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
endif(SANDBOX_DBG)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

if(SANDBOX_DBG)
 message(STATUS "MSG --- CMAKE_BUILD_TYPE: " ${CMAKE_BUILD_TYPE})
 message(STATUS "MSG --- CMAKE_CXX_FLAGS: " ${CMAKE_CXX_FLAGS})
 message(STATUS "MSG --- SANDBOX_SOURCE_DIR: " ${SANDBOX_SOURCE_DIR})
 message(STATUS "MSG --- SANDBOX_BINARY_DIR: " ${SANDBOX_BINARY_DIR})
 message(STATUS "MSG --- CMAKE_CURRENT_SOURCE_DIR: " ${CMAKE_CURRENT_SOURCE_DIR})
endif(SANDBOX_DBG)

# include project sub directories
add_subdirectory(sws)
add_subdirectory(pocotest)
