##############################
# Begin Project 
##############################
cmake_minimum_required( VERSION 3.22.1 )
project( Comms-lib
  LANGUAGES C
  VERSION 0.0.1
  DESCRIPTION "A library for standard communications"
  )

# Language
enable_language( C CXX )
set( CMAKE_C_STANDARD 14 )
set( CMAKE_C_STANDARD_REQUIRED ON )
set( CMAKE_C_EXTENSIONS ON )
set( CMAKE_CXX_STANDARD 14 )
set( CMAKE_CXX_STANDARD_REQUIRED ON )
set( CMAKE_CXX_EXTENSIONS ON )

##############################
# OPTIONS
##############################
option(CL_LINK_STATIC                    "Build static library"     OFF  )   
option(CL_BUILD_LIBRARY                  "Build Guardian library"   OFF  ) 
option(CL_DEBUG                          "Debug Mode"               OFF  )
option(CL_DEBUG_ENABLE_LOG               "Enable Logging"           OFF  )

# Modules
option(CL_BUILD_MODULES                  "Build Modules"            OFF )
option(CL_BUILD_MODULE_SERIAL            "Build Serial"             OFF )
option(CL_BUILD_MODULE_SOCKET            "Build Sockets"            OFF )

# Devices
option(CL_BUILD_DEVICES                  "Build Devices"            OFF )

# Samples
option(CL_BUILD_SAMPLES                 "Build Samples"             ON )
option(CL_BUILD_SAMPLE_SOCKET           "Build Samples"             ON )

# Tests
option(CL_BUILD_TESTS                    "Build tests"              OFF  )

##############################
# OUTPUT FILE
##############################

#if( CL_OUTPUT_TO_FILE )
#  string( TIMESTAMP DATE [%Y_%m_%d] [UTC] )
#  set( OUTPUT_FILENAME ${CMAKE_CURRENT_SOURCE_DIR}/build/${DATE}_build_log.txt )

##############################
# VARIABLES
##############################

# Linkage
if( CL_LINK_STATIC )
  set( LINK_TYPE STATIC )
else()
  set( LINK_TYPE SHARED )
endif()

if( CL_DEBUG )
  set( COMMSLIB_COMPILE_DEFS "CL_DEBUG" )
endif()

if( CL_DEBUG_ENABLE_LOG )
  set( COMMSLIB_COMPILE_DEFS "CL_DEBUG_ENABLE_LOG" )
endif()

##############################
# Set External Libraries
##############################

if( CL_BUILD_MODULES )
  add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/modules )
endif()

if( CL_BUILD_DEVICES )
  add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/devices )
endif()

##############################
# COMPILER FLAGS
##############################

# Optimization Flags
set( OPT_FLAGS
  )

# Warning Flags
set( WARN_FLAGS
  -Wall
  )

# Debug Flags
set( DEBUG_FLAGS
  -g
  -gdwarf-2
  )

# Dependency Flags
set( DEP_FLAGS
  -u_printf_float
  )

# Combine Flags
set( CL_FLAGS 
  ${OPT_FLAGS}
  ${WARN_FLAGS}
  ${DEBUG_FLAGS}
  ${DEP_FLAGS}
  )

##############################
# Set Library Dependencies
##############################

set( COMMSLIB_LIBS
  )

##############################
# Set Files and Directories
##############################

set( COMMSLIB_SRC_FILES
  ${COMMSLIB_MODULE_SRC_FILES}
  ${COMMSLIB_DEVICE_SRC_FILES}
  )

set( COMMSLIB_INC_DIRS
  ${CMAKE_CURRENT_SOURCE_DIR} 
  ${CMAKE_CURRENT_SOURCE_DIR}/inc 
  ${COMMSLIB_MODULE_INC_DIRS}
  ${COMMSLIB_DEVICE_INC_DIRS}
  )

list( APPEND COMMSLIB_COMPILE_DEFS
  ${COMMSLIB_MODULE_COMPILE_DEFS}
  )

##############################
# Make Targets
##############################

if( CL_BUILD_LIBRARY )
  add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/lib )
endif()

if( CL_BUILD_MODULES )
  add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/modules )
endif()

if( CL_BUILD_SAMPLES )
  add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/samples )
endif()

if( CL_BUILD_TESTS )
  add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/tests )
endif()
