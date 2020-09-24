if (CMAKE_SYSTEM_NAME STREQUAL "Windows")
	set (PLATFORM_SOURCES
		platform/windows/getopt.c
		platform/windows/strndup.c
	)
endif ()

add_executable(msemu
	${PLATFORM_SOURCES}
	debug.c
	flashops.c
	main.c
	msemu.c
	ui.c
)

target_include_directories(
	msemu PRIVATE
	${CMAKE_BINARY_DIR}/include
)

target_link_libraries(msemu
	SDL2
	SDL2main
	#SDL2_ttf
	z80ex
	z80ex_dasm
)

file(COPY ${CMAKE_SOURCE_DIR}/src/fonts DESTINATION ${CMAKE_BINARY_DIR})
