cmake_minimum_required(VERSION 3.11.0 FATAL_ERROR)
project(simple-svg VERSION 0.1.0 LANGUAGES C CXX)

option(BUILD_SHARED_LIBS "Build Shared Libraries" ON)

include(GNUInstallDirs)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR})

file(GLOB_RECURSE _simple_svg_headers
        ${CMAKE_CURRENT_SOURCE_DIR}/include/**.h
        )
file(GLOB_RECURSE _simple_svg_sources
        ${CMAKE_CURRENT_SOURCE_DIR}/src/**.cpp
        )

add_library(simple-svg STATIC
        ${_simple_svg_headers}
        ${_simple_svg_sources}
        )
target_include_directories(simple-svg PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        )
target_link_libraries(simple-svg PUBLIC
        bx
        )

source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}/include" PREFIX "" FILES ${_simple_svg_headers})
source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}/src" PREFIX "" FILES ${_simple_svg_sources})
