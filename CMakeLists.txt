project(alglib-cpp-cmake)
cmake_minimum_required(VERSION 2.22)

include(cmake/sources.cmake)

option(ALGLIB_NO_EXCEPTIONS OFF)
option(ALGLIB_BUILD_TESTS OFF)

add_library(alglib-cpp ${ALGLIB_SOURCES})
target_include_directories(alglib-cpp PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

if (${ALGLIB_NO_EXCEPTIONS})
    target_compile_definitions(alglib-cpp PUBLIC AE_NO_EXCEPTIONS AE_THREADING=AE_SERIAL_UNSAFE)
endif()

if (${ALGLIB_BUILD_TESTS})
    enable_testing()
    add_subdirectory(tests)
endif()

