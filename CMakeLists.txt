cmake_minimum_required(VERSION 3.28)
project(ImGui CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(ImGui STATIC
        imconfig.h
        imgui.h
        imgui.cpp
        imgui_draw.cpp
        imgui_tables.cpp
        imgui_internal.h
        imgui_widgets.cpp
        imstb_rectpack.h
        imstb_textedit.h
        imstb_truetype.h
        imgui_demo.cpp
        backends/imgui_impl_glfw.h
        backends/imgui_impl_glfw.cpp
        backends/imgui_impl_opengl3.h
        backends/imgui_impl_opengl3.cpp
)

target_include_directories(ImGui PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/backends
)
target_link_libraries(ImGui PUBLIC glfw)

if(UNIX)
    set_target_properties(ImGui PROPERTIES POSITION_INDEPENDENT_CODE ON)
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/$<CONFIG>/ImGui")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/$<CONFIG>/ImGui")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/$<CONFIG>/ImGui")

if(MSVC)
    set_property(TARGET ImGui PROPERTY
            MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"
    )
endif()