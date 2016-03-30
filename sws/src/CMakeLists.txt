#cmake_minimum_required (VERSION 2.8)
#project (Simple-Web-Server)

if(SANDBOX_DBG)
 message(STATUS "MSG --- CMAKE_BUILD_TYPE: " ${CMAKE_BUILD_TYPE})
 message(STATUS "MSG --- CMAKE_CXX_FLAGS: " ${CMAKE_CXX_FLAGS})
 message(STATUS "MSG --- SANDBOX_SOURCE_DIR: " ${SANDBOX_SOURCE_DIR})
 message(STATUS "MSG --- SANDBOX_BINARY_DIR: " ${SANDBOX_BINARY_DIR})
 message(STATUS "MSG --- CMAKE_CURRENT_SOURCE_DIR: " ${CMAKE_CURRENT_SOURCE_DIR})
endif(SANDBOX_DBG)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/inc)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -g -Wall")

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    if (CMAKE_CXX_COMPILER_VERSION VERSION_LESS 4.8)
        message(FATAL_ERROR "GCC version >=4.8 required.")
    endif()
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    if (CMAKE_CXX_COMPILER_VERSION VERSION_LESS 3.3)
        message(FATAL_ERROR "Clang version >=3.3 required.")
    endif()
elseif (MSVC14) #TODO: What about other MSVC versions?
else()
    message(WARNING "Your compiler (${CMAKE_CXX_COMPILER_ID}) has not been tested on this project. Only Clang and GCC has been tested. Please report any problems at the project page on GitHub.")
endif()


include_directories(.)

find_package(Threads REQUIRED)

# SET(BOOST_ROOT "/usr")
#message(STATUS "MSG --- BOOST_ROOT is: " ${BOOST_ROOT})

#find_package(Boost 1.53.0 COMPONENTS regex system thread coroutine context filesystem date_time REQUIRED)
#include_directories(${Boost_INCLUDE_DIR})

#   https://cmake.org/cmake/help/v3.5/module/FindBoost.html
set(Boost_DEBUG ON)
set(Boost_DETAILED_FAILURE_MSG)
find_package(Boost 1.53.0 REQUIRED)
if(Boost_FOUND)
  message(STATUS "MSG --- BOOST FOUND!")
else()
  message(STATUS "MSG --- BOOST not FOUND!")
endif()

if(APPLE)
    set(OPENSSL_ROOT_DIR "/usr/local/opt/openssl")
endif()

#TODO: add requirement for version 1.0.1g (can it be done in one line?)
find_package(OpenSSL)

if(OPENSSL_FOUND)
    include_directories(${OPENSSL_INCLUDE_DIR})

    add_executable(https_examples https_examples.cpp)
    target_link_libraries(https_examples ${Boost_LIBRARIES})
    target_link_libraries(https_examples ${OPENSSL_LIBRARIES})
    target_link_libraries(https_examples ${CMAKE_THREAD_LIBS_INIT})
endif()

add_executable(http_examples http_examples.cpp)
target_link_libraries(http_examples ${Boost_LIBRARIES})
target_link_libraries(http_examples ${CMAKE_THREAD_LIBS_INIT})

if(MSYS) #TODO: Is MSYS true when MSVC is true?
    target_link_libraries(http_examples ws2_32 wsock32)
    target_link_libraries(https_examples ws2_32 wsock32)
endif()

