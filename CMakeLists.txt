cmake_minimum_required(VERSION 3.30)
project(vulkan_tutorial)

set(CMAKE_CXX_STANDARD 23)

add_executable(vulkan_tutorial main.cpp)

find_package(glm CONFIG REQUIRED)
target_link_libraries(vulkan_tutorial PRIVATE glm::glm)

find_package(glfw3 CONFIG REQUIRED)
target_link_libraries(vulkan_tutorial PRIVATE glfw)

find_package(glad CONFIG REQUIRED)
target_link_libraries(vulkan_tutorial PRIVATE glad::glad)