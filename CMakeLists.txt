cmake_minimum_required(VERSION 3.7)

project(App)
include(CheckCCompilerFlag)

set(CMAKE_REQUIRED_LINK_OPTIONS "-arch;x86_64")
check_c_compiler_flag("-arch x86_64" x86_64Supported)
message("x86_64Supported=${x86_64Supported}")

set(CMAKE_REQUIRED_LINK_OPTIONS "-arch;arm64")
check_c_compiler_flag("-arch arm64" arm64Supported)
message("arm64Supported=${arm64Supported}")

set(SDL2_INCLUDE_DIRS /opt/homebrew/include/SDL2)
set(SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)

add_subdirectory(src)

find_package(SDL2 REQUIRED COMPONENTS SDL2)

set(APP_SRC ${SOURCE_DIR}/main.cpp)

add_executable(App ${APP_SRC} ${SOURCE_DIR}/Application.cpp)

target_link_libraries(App PRIVATE SDL2::SDL2)