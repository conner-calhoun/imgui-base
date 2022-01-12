cmake_minimum_required(VERSION 3.10)
project(ImguiBase VERSION 0.0.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(OpenGL REQUIRED)

# GLFW STUFF
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/deps/glfw)

set(SRCS
    src/main.cpp)

set(DEP_SRCS
    # IMGUI
    deps/imgui/imgui_demo.cpp
    deps/imgui/imgui_draw.cpp
    deps/imgui/imgui_tables.cpp
    deps/imgui/imgui_widgets.cpp
    deps/imgui/imgui.cpp
    deps/imgui/backends/imgui_impl_glfw.cpp
    deps/imgui/backends/imgui_impl_opengl3.cpp

    # GLAD
    deps/glad/src/glad.c)

add_executable(${PROJECT_NAME} ${SRCS} ${DEP_SRCS} ${IMGUI_SRCS})

target_include_directories(${PROJECT_NAME}
PUBLIC
    src/
    deps/
    deps/imgui/
    deps/imgui/backends/
    deps/glad/include
)

target_link_libraries(${PROJECT_NAME}
    glfw
    OpenGL::GL
)