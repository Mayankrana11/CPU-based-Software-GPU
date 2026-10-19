
cmake_minimum_required(VERSION 3.20)

project(SoftwareGPU LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_path(SDL2_INCLUDE_DIR
    NAMES SDL.h
    PATHS "C:/msys64/ucrt64/include/SDL2"
    REQUIRED
)

find_library(SDL2_LIBRARY
    NAMES SDL2
    PATHS "C:/msys64/ucrt64/lib"
    REQUIRED
)

add_executable(SoftwareGPU
    src/main.cpp
)

target_include_directories(SoftwareGPU PRIVATE
    "${SDL2_INCLUDE_DIR}"
)

target_compile_definitions(SoftwareGPU PRIVATE
    SDL_MAIN_HANDLED
)

target_link_libraries(SoftwareGPU PRIVATE
    "${SDL2_LIBRARY}"
)

if(MSVC)
    target_compile_options(SoftwareGPU PRIVATE /W4)
else()
    target_compile_options(SoftwareGPU PRIVATE -Wall -Wextra -Wpedantic)
endif()
