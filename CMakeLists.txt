cmake_minimum_required(VERSION 3.16)

project(accelstepper-wrapper
        LANGUAGES
        C CXX)

# Directory paths

if(NOT DEFINED ACCEL_WRAPPER_DIR)
    set(ACCEL_WRAPPER_DIR ${CMAKE_CURRENT_SOURCE_DIR})
endif()

if(NOT DEFINED ACCEL_WRAPPER_ARDUINO_INC_DIR)
    message(SEND_ERROR "You need to specify Arduino include files")
endif()

if(NOT DEFINED ACCEL_WRAPPER_PINOUT_HEADER)
    message(SEND_ERROR "You need to specify Arduino pinout header file")
endif()

#
# Compile definitions
#
if(NOT DEFINED ACCEL_WRAPPER_DEFS)
set(ACCEL_WRAPPER_DEFS
    "-DF_CPU=16000000UL"
)
endif()


#
# Compile options
#
if(NOT DEFINED ACCEL_WRAPPER_DEFS)
set(ACCEL_WRAPPER_OPTS
    "-mmcu=atmega328p"
)
endif()

# Source dir and sources

set(ACCEL_WRAPPER_SRC_DIR ${ACCEL_WRAPPER_DIR}/AccelStepper)

set(accel-wrapper_SRCS
    ${ACCEL_WRAPPER_SRC_DIR}/MultiStepper.cpp
    ${ACCEL_WRAPPER_SRC_DIR}/AccelStepper.cpp
)

# Target

add_library(${PROJECT_NAME} STATIC ${accel-wrapper_SRCS})

target_include_directories(${PROJECT_NAME} PRIVATE 
    ${ACCEL_WRAPPER_SRC_DIR}
    ${ACCEL_WRAPPER_ARDUINO_INC_DIR}
)

# We always set ARDUINO define to 100, because we always include Arduino.h
target_compile_definitions(${PROJECT_NAME} PRIVATE ${ACCEL_WRAPPER_DEFS} "-DARDUINO=100")
target_compile_options(${PROJECT_NAME} PRIVATE ${ACCEL_WRAPPER_OPTS})
target_include_directories(${PROJECT_NAME} PRIVATE 
    ${ACCEL_WRAPPER_ARDUINO_INC_DIR}
    ${ACCEL_WRAPPER_PINOUT_HEADER}
)
