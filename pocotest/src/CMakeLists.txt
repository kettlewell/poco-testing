#   http://stackoverflow.com/questions/8304190/cmake-with-include-and-source-paths-basic-setup
#

if(SANDBOX_DBG)
 message(STATUS "MSG --- CMAKE_BUILD_TYPE: " ${CMAKE_BUILD_TYPE})
 message(STATUS "MSG --- CMAKE_CXX_FLAGS: " ${CMAKE_CXX_FLAGS})
 message(STATUS "MSG --- SANDBOX_SOURCE_DIR: " ${SANDBOX_SOURCE_DIR})
 message(STATUS "MSG --- SANDBOX_BINARY_DIR: " ${SANDBOX_BINARY_DIR})
 message(STATUS "MSG --- CMAKE_CURRENT_SOURCE_DIR: " ${CMAKE_CURRENT_SOURCE_DIR})
endif(SANDBOX_DBG)


include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../inc)

set(HEADER_FILES 
  "${CMAKE_CURRENT_SOURCE_DIR}/../inc/application_server.h"

)

set(SOURCE_FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/application_server.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/http_get.cpp"
)

# I assume you want to use LibProject as a library in MainProject.
# include_directories(${MyProject_SOURCE_DIR}/LibProject/inc)
# link_directories(${MyProject_SOURCE_DIR}/LibProject/src)


add_executable(pocotest ${SOURCE_FILES} ${HEADER_FILES})

# target_link_libraries(MainProject LibProject)
# target_link_libraries(pocotest)

