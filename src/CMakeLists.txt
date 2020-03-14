cmake_minimum_required(VERSION 3.2)
project(fs-actions)

# add_subdirectory(division)
set(SOURCE_FILES main.cpp)

add_executable(fs-actions ${SOURCE_FILES})
# target_link_libraries(divider division)
install(TARGETS fs-actions DESTINATION ${DIVISIBLE_INSTALL_BIN_DIR})