cmake_minimum_required(VERSION 3.2)
project(fs-events_tests)

enable_testing()

add_subdirectory(lib/googletest)

include_directories(${FSEVENTS_HEADERS_DIR})
include_directories(lib/googletest/googletest/include)

set(SOURCE_FILES main.cpp src/fs-events_tests.cpp)

add_executable(fs-events_tests ${SOURCE_FILES})
if (MSVC)
    target_compile_options(fs-events_tests PRIVATE "/MTd")
endif()

target_link_libraries(fs-events_tests gtest)
install(TARGETS fs-events_tests DESTINATION bin)