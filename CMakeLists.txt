cmake_minimum_required(VERSION 3.15)

project(vs_mkr_test1)

set(CMAKE_CXX_STANDARD 14)

include(FetchContent)

FetchContent_Declare(
        googletest
        URL https://github.com/google/googletest/archive/release-1.12.1.zip
)

FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(vs_mkr_test1
        pch.cpp
        test.cpp
)

target_link_libraries(vs_mkr_test1
        gtest
        gtest_main
)

add_test(NAME vs_mkr_test1 COMMAND vs_mkr_test1)
