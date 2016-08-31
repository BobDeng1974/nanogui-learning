cmake_minimum_required(VERSION 2.6)
project(nanoplayer)

add_executable(nanoplayer main.cpp)

install(TARGETS nanoplayer RUNTIME DESTINATION bin)
