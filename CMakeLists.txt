cmake_minimum_required(VERSION 3.10)

# string(REGEX REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
# if (MSVC)
#     set(CMAKE_C_FLAGS_INIT "")
#     set(CMAKE_CXX_FLAGS_INIT "")
#     set(CMAKE_C_FLAGS_DEBUG_INIT "")
#     set(CMAKE_CXX_FLAGS_DEBUG_INIT "")
#     set(CMAKE_C_FLAGS_RELEASE_INIT "")
#     set(CMAKE_CXX_FLAGS_RELEASE_INIT "")
#     set(CMAKE_C_FLAGS "")
#     set(CMAKE_CXX_FLAGS "")
#     set(CMAKE_C_FLAGS_DEBUG "")
#     set(CMAKE_CXX_FLAGS_DEBUG "")
#     set(CMAKE_C_FLAGS_RELEASE "")
#     set(CMAKE_CXX_FLAGS_RELEASE "")

#     set(CMAKE_C_STANDARD_LIBRARIES_INIT "")
#     set(CMAKE_CXX_STANDARD_LIBRARIES_INIT "")
#     set(CMAKE_C_STANDARD_LIBRARIES "")
#     set(CMAKE_CXX_STANDARD_LIBRARIES "")
# endif()

set (CMAKE_USER_MAKE_RULES_OVERRIDE "${CMAKE_CURRENT_LIST_DIR}/CompilerOptions.cmake")
project(fs-actions)

option(PEDANTIC "Build with high compiler warning level" ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR})

set(FSEVENTS_INSTALL_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)
set(FSEVENTS_INSTALL_BIN_DIR ${PROJECT_SOURCE_DIR}/bin)
set(FSEVENTS_INSTALL_LIB_DIR ${PROJECT_SOURCE_DIR}/lib)

set(FSEVENTS_HEADERS_DIR ${PROJECT_SOURCE_DIR}/include)

include_directories(${FSEVENTS_INSTALL_INCLUDE_DIR})
include_directories(${FSEVENTS_HEADERS_DIR})

if (PEDANTIC)
    if(MSVC)
        string(REGEX REPLACE "/W[0-4]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
    else()
        add_definitions(-Wall -Wextra -pedantic -Werror)
    endif()
endif()

add_subdirectory(src)
add_subdirectory(test)