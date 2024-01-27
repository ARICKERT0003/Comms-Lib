##############################
# Begin Project 
##############################
cmake_minimum_required( VERSION 3.22.1 )
project( comms-lib
  LANGUAGES C
  VERSION 0.0.1
  DESCRIPTION "A library for standard communications - Samples"
  )

##############################
# Recurse into samples
##############################

add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/socket_client )
add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/socket_server )
