include(${CMAKE_ROOT}/Modules/ExternalProject.cmake)

ExternalProject_Add(
    sdl2
    PREFIX SDL2

    GIT_REPOSITORY "https://github.com/spurious/SDL-mirror/"
    GIT_TAG "release-2.0.12"
    GIT_SHALLOW ON

    UPDATE_COMMAND ""
    PATCH_COMMAND ""
    INSTALL_COMMAND cmake -E echo "Skipping install step."

    SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/sdl2"
)

# Build step here is windows specific, will need to add 
# a unix variant if we  need to build from source.
ExternalProject_Add(
    sdl2_ttf
    PREFIX SDL2

    GIT_REPOSITORY "https://github.com/davidsiaw/SDL2_ttf"
    GIT_TAG "master"
    GIT_SHALLOW ON

    UPDATE_COMMAND ""
    PATCH_COMMAND ""
    CONFIGURE_COMMAND ""
    INSTALL_COMMAND cmake -E echo "Skipping install step."

    SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/sdl2_ttf"
    BUILD_COMMAND ${CMAKE_MAKE_PROGRAM} "${CMAKE_CURRENT_SOURCE_DIR}/sdl2_ttf/VisualC/SDL_ttf.sln" /p:PlatformToolset=v142
)

ExternalProject_Add(
    z80ex
    PREFIX z80ex

    GIT_REPOSITORY "https://github.com/lipro/z80ex/"
    GIT_TAG "master"
    GIT_SHALLOW ON

    UPDATE_COMMAND ""
    PATCH_COMMAND ""
    INSTALL_COMMAND cmake -E echo "Skipping install step."

    SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/z80ex"
    CMAKE_ARGS -DRELEASE_TYPE=msemu
)