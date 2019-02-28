cmake_minimum_required(VERSION 3.9)
PROJECT("TravisTest")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0 -Wall -Wno-unused-function -Wno-unused-parameter -Wextra -Wpedantic")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE}")

list(APPEND CORE_LIBS stdc++fs)

file(GLOB CPP_FILES main.cpp)

set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)

message("OpenGL: ${OpenGL_OpenGL_FOUND}")
message("EGL Lib: ${OPENGL_egl_LIBRARY}")

if(OpenGL_OpenGL_FOUND)
    list(APPEND CORE_LIBS OpenGL::OpenGL OpenGL::GLX)
else()
    list(APPEND CORE_LIBS OpenGL::GL)
endif()

add_library(TravisTest ${CPP_FILES})
set_property(TARGET TravisTest PROPERTY CXX_STANDARD 17)
target_include_directories(TravisTest PUBLIC .)
target_link_libraries(TravisTest ${CORE_LIBS})
