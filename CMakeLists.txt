cmake_minimum_required(VERSION 3.8)
project(cmake-circleci)

set(CMAKE_CXX_STANDARD 14)

set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")

include(cmake/DownloadProject.cmake)

download_project(
    PROJ   googletest
    GIT_REPOSITORY      git@github.com:google/googletest.git
    GIT_TAG             master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
)

add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})

set(SOURCE_FILES main.cpp)

add_executable(cmake-circleci ${SOURCE_FILES})

target_link_libraries(cmake-circleci gtest gtest_main)
