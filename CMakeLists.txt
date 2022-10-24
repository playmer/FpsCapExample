cmake_minimum_required(VERSION 3.15)

include(FetchContent)
FetchContent_Declare(
    vcpkg
    GIT_REPOSITORY https://github.com/microsoft/vcpkg.git
    GIT_TAG master
)
if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    FetchContent_Populate(vcpkg)
    set(CMAKE_TOOLCHAIN_FILE "${vcpkg_SOURCE_DIR}/scripts/buildsystems/vcpkg.cmake")
endif()

project(fps_cap_example)

add_executable(fps_cap_example main.cpp)

find_package(SDL2 CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
target_link_libraries(fps_cap_example 
PRIVATE 
    SDL2::SDL2 
    SDL2::SDL2main
    imgui::imgui
)

if (${CMAKE_SYSTEM_NAME} STREQUAL Windows)
    target_link_libraries(fps_cap_example PRIVATE Winmm.lib)
endif()
