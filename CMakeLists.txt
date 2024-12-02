if (NOT WIN32)
    return()
endif()

cmake_minimum_required(VERSION 2.8.11)

project (dlfcn-win32 C)

list(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake/modules")
include(Macros)

option(BUILD_SHARED_LIBS "shared/static libs" ON) 
option(BUILD_TESTS "tests?" OFF)

add_subdirectory(src)
if (BUILD_TESTS)
    if (CMAKE_CROSSCOMPILING AND NOT DEFINED CMAKE_CROSSCOMPILING_EMULATOR)
        message(WARNING "You might want to set CMAKE_CROSSCOMPILING_EMULATOR to wine path in order to run tests")
    endif ()
    enable_testing()
    add_subdirectory(tests)
endif()
