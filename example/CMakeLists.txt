cmake_minimum_required(VERSION 3.14)

project(dylib_example)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR})

# dylib fetch

include(FetchContent)

FetchContent_Declare(
    dylib
    GIT_REPOSITORY  "https://github.com/martin-olivier/dylib"
    GIT_TAG         "v1.8.3"
)

FetchContent_MakeAvailable(dylib)

# build lib.cpp into a shared library

add_library(dynamic_lib SHARED lib.cpp)
set_target_properties(dynamic_lib PROPERTIES PREFIX "")
target_link_libraries(dynamic_lib PRIVATE dylib)

# build main.cpp into an executable

add_executable(dylib_example main.cpp)
target_link_libraries(dylib_example PRIVATE dylib)
