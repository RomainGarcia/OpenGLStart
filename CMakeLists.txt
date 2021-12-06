cmake_minimum_required(VERSION 3.20)
project(OpenGLStart)

set(CMAKE_CXX_STANDARD 20)

add_executable(OpenGLStart WIN32 main.cpp)

if(MSVC)
    SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /ENTRY:mainCRTStartup")
endif()

# glfw and legacy OpenGL
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})
add_subdirectory(external/glfw EXCLUDE_FROM_ALL)
target_link_libraries(OpenGLStart PRIVATE ${OPENGL_LIBRARIES} glfw)

# glew
add_definitions(-DGLEW_STATIC)
add_subdirectory(external/glew EXCLUDE_FROM_ALL)
target_link_libraries(OpenGLStart PRIVATE libglew_static)

