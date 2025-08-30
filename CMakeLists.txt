cmake_minimum_required(VERSION 3.30)

project(wren VERSION 0.4.0 LANGUAGES C)

include(GNUInstallDirs)

set(CMAKE_C_STANDARD 99)

add_subdirectory("src")
add_subdirectory("test")
