cmake_minimum_required(VERSION 3.10.2)

project(imgui)

file(GLOB imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

if(WIN32)
    list(APPEND imgui_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_win32.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_dx9.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_dx10.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_dx11.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_dx12.cpp
    )
elseif(APPLE)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_metal.mm)
    if (CMAKE_SYSTEM_NAME STREQUAL "Darwin")
        list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_osx.mm)
    endif()
elseif(ANDROID)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_android.cpp)
elseif(EMSCRIPTEN)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_wgpu.cpp)
endif()

if(IMGUI_IMPL_OPENGL)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp)
endif()
if(IMGUI_IMPL_VULKAN)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_vulkan.cpp)
endif()
if(IMGUI_IMPL_GLUT)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glut.cpp)
endif()
if(IMGUI_IMPL_GLFW)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_glfw.cpp)
endif()
if(IMGUI_IMPL_SDL2)
    list(APPEND imgui_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdl2.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdlrenderer2.cpp
    )
endif()
if(IMGUI_IMPL_SDL3)
    list(APPEND imgui_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdl3.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdlrenderer3.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_sdlgpu3.cpp
    )
endif()
if(IMGUI_IMPL_ALLEGRO5)
    list(APPEND imgui_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/backends/imgui_impl_allegro5.cpp)
endif()

add_library(imgui STATIC ${imgui_SOURCES})

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

if(IMGUI_IMPL_GLUT)
    target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../glut/include)
endif()
if(IMGUI_IMPL_GLFW)
    target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../glfw/include)
endif()
if(IMGUI_IMPL_SDL2)
    target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../SDL2/include)
endif()
if(IMGUI_IMPL_SDL3)
    target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../SDL3/include)
endif()
if(IMGUI_IMPL_ALLEGRO5)
    target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../allegro5/include)
endif()

set_target_properties(PlasmaLib PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
    LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
    ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
)
