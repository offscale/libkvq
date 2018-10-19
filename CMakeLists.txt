cmake_minimum_required(VERSION 3.0)
project(libkvq)

set(CMAKE_CXX_STANDARD 11)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(KEEP_RPATHS)

configure_file(lib/version.h.in version.h @ONLY)

include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_library(libkvq library.cpp library.h)

if (NOT "$ENV{TEST_ENABLED}" STREQUAL "")
    set(TEST_ENABLED "$ENV{TEST_ENABLED}" CACHE INTERNAL "Copied from environment variable")
else ()
    set(TEST_ENABLED 1)
endif ()

if (TEST_ENABLED)
    enable_testing()
    include(CTest)

    find_package(CMOCKA REQUIRED)
    if (CMOCKA_FOUND)
        include_directories("${CONAN_INCLUDE_DIRS_CMOCKA}/include")

        file(GLOB files "test/test_*.c")
        foreach (file ${files})
            get_filename_component(file_without_ext ${file} NAME_WE CACHE INTERNAL)
            add_executable(${file_without_ext} ${file})
            add_test(${file_without_ext} ${file_without_ext})
            target_link_libraries(${file_without_ext} cmocka)
        endforeach ()
    else ()
        message(could not find CMocka, did you run `conan install`?)
    endif ()
endif ()
