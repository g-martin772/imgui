cmake_minimum_required(VERSION 3.10)
project(ImGui)

set(IMGUI_SRC
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_vulkan.cpp
)

add_library(imgui STATIC ${IMGUI_SRC})

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
    ${CMAKE_SOURCE_DIR}/dependencies/glfw/include
)

find_package(Vulkan REQUIRED)
target_include_directories(imgui PRIVATE ${Vulkan_INCLUDE_DIRS})
target_link_libraries(imgui PRIVATE Vulkan::Vulkan)

set_target_properties(imgui PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED ON
)
