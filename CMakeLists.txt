cmake_minimum_required(VERSION 3.30)
project(vulkan_tutorial)

set(CMAKE_CXX_STANDARD 23)

set(VULKAN_SDK "/Users/phakel/.local/share/vulkansdk/1.4.313.0")

set($ENV{VK_ICD_FILENAMES} ${VULKAN_SDK}/macOS/share/vulkan/icd.d/MoltenVK_icd.json)
set($ENV{VK_LAYER_PATH} ${VULKAN_SDK}/macOS/share/vulkan/explicit_layer.d)

include_directories(${VULKAN_SDK}/macOS/include)
link_directories(${VULKAN_SDK}/macOS/lib)

add_executable(vulkan_tutorial main.cpp)

find_package(glm CONFIG REQUIRED)
target_link_libraries(vulkan_tutorial PRIVATE glm::glm)

find_package(glfw3 CONFIG REQUIRED)
target_link_libraries(vulkan_tutorial PRIVATE glfw)

add_library(vulkan SHARED IMPORTED)
set_target_properties(vulkan PROPERTIES
        IMPORTED_LOCATION ${VULKAN_SDK}/macOS/lib/libvulkan.1.dylib
        INTERFACE_INCLUDE_DIRECTORIES ${VULKAN_SDK}/macOS/include
)
set_target_properties(vulkan PROPERTIES
        IMPORTED_LOCATION ${VULKAN_SDK}/macOS/lib/libvulkan.1.4.313.dylib
        INTERFACE_INCLUDE_DIRECTORIES ${VULKAN_SDK}/macOS/include
)
target_link_libraries(vulkan_tutorial PRIVATE vulkan)
