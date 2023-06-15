cmake_minimum_required(VERSION 3.13)

project(
    malloc_count
    DESCRIPTION "Profile memory usage"
    LANGUAGES C
)

list(
    APPEND
    MALLOC_COUNT_C_FLAGS
    "-Wall"
    "-Wextra"
    "-Wpedantic"
    "-W"
    "-Wmissing-prototypes"
    "-Wstrict-prototypes"
    "-Wconversion"
    "-Wshadow"
    "-Wpointer-arith"
    "-Wcast-align"
    "-Wcast-qual"
    "-Wwrite-strings"
    "-Wnested-externs"
    "-fshort-enums"
    "-fno-common"
)
# TODO Remove short-enums and fno-common from that list and look up how to properly add them in CMake

set(CMAKE_INCLUDE_CURRENT_DIR ON)
add_library(malloc_count STATIC)
target_compile_features(malloc_count PRIVATE c_std_99)
set_target_properties(malloc_count PROPERTIES LINKER_LANGUAGE C)
target_compile_options(malloc_count PRIVATE ${MALLOC_COUNT_C_FLAGS})
target_include_directories(malloc_count PUBLIC "${CMAKE_CURRENT_LIST_DIR}")
target_sources(
    malloc_count
    PRIVATE malloc_count.c stack_count.c
    PUBLIC malloc_count.h stack_count.h
)
target_link_libraries(malloc_count kastore m)
