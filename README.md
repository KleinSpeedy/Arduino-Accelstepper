# Accelstepper Arduino library CMake wrapper

Simple CMake wrapper around `Accelstepper` library.

## Usage

```cmake
# Accelstepper library
set(ACCEL_WRAPPER_DIR path/to/lib CACHE STRING "")
set(ACCEL_WRAPPER_ARDUINO_INC_DIR path/to/include CACHE STRING "")
set(ACCEL_WRAPPER_PINOUT_HEADER path/to/pinout_h CACHE STRING "")
set(ACCEL_WRAPPER_DEFS ... CACHE STRING "")
set(ACCEL_WRAPPER_OPTS ... CACHE STRING "")

add_subdirectory(path/to/Arduino-Accelstepper)
```

## Miscellaneous

`Accelstepper` library is licensed under GPLv3, so we include a GPLv3 License
file as well.

