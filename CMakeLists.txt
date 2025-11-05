# Example CMake command line to create project build files:
#
# *** Windows ***
# cmake -G "Visual Studio 17 2022" -A Win32 -B Build -S .
#
# *** Linux ***
# cmake -G "Unix Makefiles" -B Build -S .

# Specify the minimum CMake version required
cmake_minimum_required(VERSION 3.10)

# Project name and language (C or C++)
project(C_StateMachine VERSION 1.0 LANGUAGES C CXX)

# Collect source files from specific directories only
set(SOURCES
    "${CMAKE_SOURCE_DIR}/main.c"
)

# Add source files from subdirectories
file(GLOB DYNAMIC_MEMORY_SOURCES 
    "${CMAKE_SOURCE_DIR}/dynamic_memory/*.c"
)

file(GLOB STATE_MACHINE_SOURCES 
    "${CMAKE_SOURCE_DIR}/StateMachine/*.c"
    "${CMAKE_SOURCE_DIR}/StateMachine/*.cpp"
)

file(GLOB EXAMPLE_SOURCES 
    "${CMAKE_SOURCE_DIR}/Example/*.c"
)

# Combine all sources
list(APPEND SOURCES 
    ${DYNAMIC_MEMORY_SOURCES}
    ${STATE_MACHINE_SOURCES}
    ${EXAMPLE_SOURCES}
)

# Filter out CMake internal files that might cause conflicts
list(FILTER SOURCES EXCLUDE REGEX "CMakeCCompilerId")
list(FILTER SOURCES EXCLUDE REGEX "CMakeCXXCompilerId")

# Add an executable target
add_executable(C_StateMachineApp ${SOURCES})

# Include directories for header files
target_include_directories(C_StateMachineApp PRIVATE 
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/data_common
    ${CMAKE_SOURCE_DIR}/dynamic_memory
    ${CMAKE_SOURCE_DIR}/StateMachine
    ${CMAKE_SOURCE_DIR}/Example
)