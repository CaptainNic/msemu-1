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
    # If git is available and this is a git clone, we will restore
    # the submodules from git. If not, we assume the submodules already
    # exist where they're supposed to be.
    find_package(Git)
    if (GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
        option (GIT_SUBMODULE "Check submodules during build" ON)
        if (GIT_SUBMODULE)
            message(STATUS "Updating git submodules")
            execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                            RESULT_VARIABLE GIT_SUBMOD_RESULT)
            if (NOT GIT_SUBMOD_RESULT EQUAL "0")
                message(FATAL_ERROR "git submodule update failed with code ${GIT_SUBMOD_RESULT}")
            endif ()
        endif ()
    endif ()
endif ()

add_subdirectory(src)
add_subdirectory(external)
