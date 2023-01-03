cmake_minimum_required(VERSION 3.5)

project(OpenGL LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(src/)

add_executable(${PROJECT_NAME} main.cpp vertices.vert)

#Add GLFW as a library
find_package(glfw3 REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE glfw)

#Add GLAD as a library
if(WIN32)
    find_package(glad CONFIG REQUIRED)
    target_link_libraries(${PROJECT_NAME} PRIVATE glad::glad)
elseif(UNIX)
    add_subdirectory(glad/)
    target_link_libraries(${PROJECT_NAME} PRIVATE glad)
endif()
