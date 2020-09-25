cmake_minimum_required(VERSION 3.7)

project(msemu LANGUAGES C)

option(BUILD_DEPENDENCIES "Build dependency libraries" OFF)
if (CMAKE_SYSTEM_NAME STREQUAL "Windows")
    # Since windows doesn't have good package management,
    # it will always attempt to build dependencies.
    set (BUILD_DEPENDENCIES ON)
endif ()

if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Debug" CACHE STRING "Choose the type of build." FORCE)
    message(WARNING "No CMAKE_BUILD_TYPE value specified, defaulting to ${CMAKE_BUILD_TYPE}.")
else ()
    message(STATUS "The CMake build type is: ${CMAKE_BUILD_TYPE}")
endif ()

# Make sure all libs and binaries end up in the same place,
# instead of in their respective build directories.
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

if (BUILD_DEPENDENCIES)
    add_subdirectory(external)
endif ()

#add_subdirectory(src)
