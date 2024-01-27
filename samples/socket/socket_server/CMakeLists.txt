cmake_minimum_required( VERSION 3.22.1 )
project( comms-lib
  LANGUAGES CXX
  VERSION 0.0.1
  DESCRIPTION "A library for standard communications - Samples"
  )

#############################
# Set General Variables
#############################

set( TEST_NAME socket_server )

set( TEST_SRC 
  ${COMMSLIB_SRC_FILES}
  ${TEST_NAME}.cpp 
  )

# Output Directory
if(NOT COMMSLIB_TEST_LED_OUTPUT_DIR )
  set( COMMSLIB_TEST_LED_OUTPUT_DIR ${CMAKE_CURRENT_SOURCE_DIR} )
endif()

#############################
# Make Target
#############################
add_executable( ${TEST_NAME} ${TEST_SRC} ) 

# Set Library Properties
set_target_properties( ${TEST_NAME} PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY ${COMMSLIB_TEST_LED_OUTPUT_DIR}
  )

#############################
# Link Library
#############################

# Specify compiler definitions
#target_compile_definitions( ${TEST_NAME} PUBLIC
#  ${COMMSLIB_COMPILE_DEFS}
#  )
#
#target_compile_options( ${TEST_NAME} 
#  PRIVATE
#  ${COMMSLIB_FLAGS}
#  )
#
#target_include_directories( ${TEST_NAME}
#  PUBLIC
#  ${COMMSLIB_INC_DIRS}
#  )
#
#target_link_libraries( ${TEST_NAME} 
#  PUBLIC 
#  ${COMMSLIB_LIBS}
#  )

#target_link_options( ${TEST_NAME}
#  PRIVATE
#  -T${COMMSLIB_LINKER_SCRIPT}
#  ${CPU_FLAGS}
#  -Wl,-Map=${CMAKE_PROJECT_NAME}.map
#  --specs=nosys.specs
#  )

##############################
# Toolchain Commands 
##############################
#add_custom_command( TARGET ${TEST_NAME} 
#  POST_BUILD
#  COMMAND ${CMAKE_SIZE} $<TARGET_FILE:${TEST_NAME}>
#  COMMAND ${CMAKE_OBJCOPY} -O ihex $<TARGET_FILE:${TEST_NAME}> '${COMMSLIB_TEST_LED_OUTPUT_DIR}/${TEST_NAME}.hex'
#  COMMAND ${CMAKE_OBJCOPY} -O binary $<TARGET_FILE:${TEST_NAME}> '${COMMSLIB_TEST_LED_OUTPUT_DIR}/${TEST_NAME}.bin'
#  )
