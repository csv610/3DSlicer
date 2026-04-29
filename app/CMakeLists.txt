cmake_minimum_required(VERSION 3.11)
project(AppTargets LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(GLUT REQUIRED)
find_package(assimp REQUIRED)

set(OPENCSG_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../src/OpenCSG)
set(OPENCSG_INCLUDE_DIR ${OPENCSG_DIR}/include)
set(OPENCSG_EXAMPLE_INCLUDE ${OPENCSG_DIR}/example)

# Target 1: GLUT-based viewer
add_executable(meshslicer main.cpp
    ${OPENCSG_EXAMPLE_INCLUDE}/displaylistPrimitive.cpp
)

target_include_directories(meshslicer PRIVATE
    ${GLEW_INCLUDE_DIRS}
    ${OPENCSG_INCLUDE_DIR}
    ${OPENCSG_EXAMPLE_INCLUDE}
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_libraries(meshslicer PRIVATE
    opencsg
    assimp::assimp
    GLEW::GLEW
    GLUT::GLUT
    OpenGL::GL
)

# Target 2: Qt/QGLViewer-based viewer (commented out if dependencies are missing)
# For now, let's keep it but it might need Qt and QGLViewer packages.
# find_package(Qt6 COMPONENTS Widgets Core Gui REQUIRED)
# add_executable(MeshSliceViewer MeshSliceViewer.cpp)
# ...
