if (NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/sdl2/CMakeLists.txt")
    message(FATAL_ERROR "submodule sdl2 is not initialized!")
endif ()
add_subdirectory(sdl2)

if (NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/z80ex/CMakeLists.txt")
    message(FATAL_ERROR "submodule z80ex is not initialized!")
endif ()
add_subdirectory(z80ex)