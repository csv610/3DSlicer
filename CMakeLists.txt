cmake_minimum_required(VERSION 3.11)
project(3DSlicer LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenGL REQUIRED)

set(OPENCSG_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src/OpenCSG)
add_subdirectory(src/OpenCSG)

add_library(OpenCSG::OpenCSG ALIAS opencsg)

add_subdirectory(app)
