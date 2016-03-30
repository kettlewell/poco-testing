#   http://stackoverflow.com/questions/8304190/cmake-with-include-and-source-paths-basic-setup
#
include_directories( ${CMAKE_CURRENT_SOURCE_DIR}../inc)
add_library(poco ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
