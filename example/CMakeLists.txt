cmake_minimum_required(VERSION 3.15)
project(example C)

find_package(TIFF REQUIRED)

add_executable(${PROJECT_NAME} src/main.c)
target_link_libraries(${PROJECT_NAME} PRIVATE TIFF::TIFF)
