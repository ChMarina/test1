cmake_minimum_required (VERSION 2.8)

# disable in-source build
set(CMAKE_DISABLE_SOURCE_CHANGES ON)
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)

# set name of project
project (TEST)

# set name of binary file
set(BIN test)

#add_subdirectory(src)


# list files for compiling
file(GLOB_RECURSE PROJECT_SOURCES src/*.cpp)
file(GLOB_RECURSE PROJECT_HEADERS src/*.h)

# Collecting all headers directories
set (PROJECT_INCLUDE_DIRS "")
foreach (_headerFile ${PROJECT_HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND PROJECT_INCLUDE_DIRS ${_dir})
endforeach()
list(REMOVE_DUPLICATES PROJECT_INCLUDE_DIRS)

# Include all headers directories
include_directories(${PROJECT_INCLUDE_DIRS})

# set name of binary file
add_executable(${BIN} ${PROJECT_SOURCES})


# linking with library
target_link_libraries(${BIN} fcgi)
target_link_libraries(${BIN} config++)
