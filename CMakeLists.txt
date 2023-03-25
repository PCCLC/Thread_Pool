cmake_minimum_required(VERSION 3.0)

project(ThreadPool)

add_compile_options(-std=c++17)

include_directories(${PROJECT_SOURCE_DIR}/include)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(LIBRARY_OUTPUT_DPATH ${PROJECT_SOURCE_DIR}/lib)

add_subdirectory(src)