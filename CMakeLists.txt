# Version 3.8 is required for c++17
cmake_minimum_required(VERSION 3.8)
project(OTTO VERSION 0.0.1 LANGUAGES CXX C)

set(CMAKE_CXX_EXTENSIONS OFF)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

option(OTTO_DEBUG_UI "Enable the imgui based debug ui" ON)
option(OTTO_BUILD_DOCS "Build documentation" OFF)
option(OTTO_USE_LIBCXX "Link towards libc++ instead of libstdc++. This is the default on OSX" ${APPLE})

if (OTTO_USE_LIBCXX)
  message("Using libc++ instead of libstdc++")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
endif()

if (OTTO_DEBUG_UI)
  add_definitions(-DOTTO_DEBUG_UI=1)
else()
  add_definitions(-DOTTO_DEBUG_UI=0)
endif()

include(external/external.cmake)

add_subdirectory(src)
add_subdirectory(test)
