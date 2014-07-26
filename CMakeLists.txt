cmake_minimum_required(VERSION 2.8.4)

project(lodepng)

set(lodepng_version_major 1)
set(lodepng_version_minor 1)

if(MINGW OR UNIX)
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-attributes")
endif()

if(MSVC)
	foreach(OUTPUTCONFIG ${CMAKE_CONFIGURATION_TYPES})
		string(TOUPPER ${OUTPUTCONFIG} OUTPUTCONFIG)
		set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_BINARY_DIR}/bin)
		set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_BINARY_DIR}/lib)
		set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${OUTPUTCONFIG} ${CMAKE_BINARY_DIR}/lib)
	endforeach(OUTPUTCONFIG CMAKE_CONFIGURATION_TYPES)
endif()

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

list(APPEND public_hdr_loc "${CMAKE_CURRENT_SOURCE_DIR}/include")
list(APPEND public_hdrs
	include/lodepng/lodepng.h)

set(src
	src/lodepng.c)

add_library(liblodepng ${src} ${public_hdrs})
set_target_properties(liblodepng PROPERTIES
	INCLUDE_DIRECTORIES "${public_hdr_loc}"
	INTERFACE_INCLUDE_DIRECTORIES "${public_hdr_loc}"
	COMPILE_DEFINITIONS "${definitions_public};${definitions_private}"
	INTERFACE_COMPILE_DEFINITIONS "${definitions_public}"
	PREFIX ""
	SOVERSION ${lodepng_version_major}
	PUBLIC_HEADER "${public_hdrs}")

install(TARGETS liblodepng
	RUNTIME DESTINATION bin COMPONENT runtime
	LIBRARY DESTINATION lib COMPONENT dev
	ARCHIVE DESTINATION lib COMPONENT dev
	PUBLIC_HEADER DESTINATION include/lodepng COMPONENT dev)
