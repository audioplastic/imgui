cmake_minimum_required(VERSION 3.13)
project(imgui)

SET (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake/")
find_package(SDL2 REQUIRED)

file(GLOB IMGUI_SRC
        "*.cpp"
        "examples/imgui_impl_sdl.cpp"
        "examples/imgui_impl_opengl3.cpp"
        "examples/libs/gl3w/GL/gl3w.c")

include_directories(${PROJECT_SOURCE_DIR})
include_directories(${PROJECT_SOURCE_DIR}/examples)
include_directories(${PROJECT_SOURCE_DIR}/examples/libs/gl3w)
include_directories(${SDL2_INCLUDE_DIR})

add_library(imgui ${IMGUI_SRC})
FIND_LIBRARY(OPENGL_LIBRARY OpenGL)
target_link_libraries(imgui ${OPENGL_LIBRARY} ${SDL2_LIBRARY})

if(APPLE)
    find_library(COREFOUNDATION_LIBRARY CoreFoundation)
    target_link_libraries(imgui ${COREFOUNDATION_LIBRARY})
endif(APPLE)

add_executable(imgui-demo "examples/example_sdl_opengl3/main.cpp")
target_link_libraries(imgui-demo imgui)

