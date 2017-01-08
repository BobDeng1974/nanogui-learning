cmake_minimum_required(VERSION 2.6)
project(nanoplayer)

set(APP_NAME "nanoplayer")
#set(APP_LIB_NAME "libcutils")

#include(CheckCXXCompilerFlag)
#if (CMAKE_CXX_COMPILER_ID MATCHES "^(GNU|Clang|Intel)$")
#  CHECK_CXX_COMPILER_FLAG("-std=c++14" HAS_CPP14_FLAG)
#  CHECK_CXX_COMPILER_FLAG("-std=c++11" HAS_CPP11_FLAG)
#
#  if (HAS_CPP14_FLAG)
#    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")
#  elseif (HAS_CPP11_FLAG)
#    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#  else()
#    message(FATAL_ERROR "Unsupported compiler -- pybind11 requires C++11 support!")
#  endif()
#endif()


# Run simple C converter to put font files into the data segment
#add_executable(bin2c ext/nanogui/resources/bin2c.c)
#set(bin2c_cmdline nanogui_resources.cpp nanogui_resources.h)
#file(GLOB resources "${CMAKE_CURRENT_SOURCE_DIR}/ext/nanogui/resources/*.ttf")
#foreach(file ${resources})
#  list(APPEND bin2c_cmdline ${file})
#endforeach()

# Run bin2c on resource files
#add_custom_command(
#  OUTPUT nanogui_resources.cpp nanogui_resources.h
#  COMMAND bin2c ARGS ${bin2c_cmdline}
#  DEPENDS bin2c ${resources}
#  COMMENT "Running bin2c"
#  PRE_BUILD VERBATIM)

#SET(GCC_COVERAGE_COMPILE_FLAGS "-fprofile-arcs -ftest-coverage")
#SET(GCC_COVERAGE_LINK_FLAGS    "-Wl,rpath ./ -L./")
set(CMAKE_LD_FLAGS  "${CMAKE_LD_FLAGS} -Wl,rpath ./ -L./" )
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions")

set(USE_SYSTEM_CURL ON CACHE BOOL "Use system curl" FORCE)
set(BUILD_CPR_TESTS OFF CACHE BOOL "Not build test" FORCE)
option(USE_SYSTEM_CURL "" ON)
option(BUILD_CPR_TESTS "" OFF)

add_definitions(-D_GLIBCXX_USE_CXX11_ABI=1)
include_directories(ext ext/nanogui/ext/nanovg/src ext/nanogui/ext/eigen ext/nanogui/include ext/aeon_streams/include ext/cpr/include)
#add_executable(nanoplayer main.cpp)
#target_link_libraries(nanoplayer pthread m)
#install(TARGETS nanoplayer RUNTIME DESTINATION bin)
add_subdirectory(ext/nanogui)
add_subdirectory(ext/aeon_streams)
add_subdirectory(ext/cpr)
add_subdirectory(ext/tinyxml2)
add_subdirectory(src)

#add_executable(nanoplayer src/main.cpp)
#target_link_libraries(nanoplayer pthread m)
