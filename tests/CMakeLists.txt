project(alglib-cpp-cmake-tests)
cmake_minimum_required(VERSION 2.22)

set(TESTS test_c.cpp
          test_i.cpp
          test_x.cpp
          test_xpart0.cpp)


if (${ALGLIB_NO_EXCEPTIONS})
set(TESTS test_xne.cpp
          test_c.cpp)
endif()


foreach(TEST_FILE ${TESTS})
    get_filename_component(TEST_NAME ${TEST_FILE} NAME_WLE)
    
    add_executable(${TEST_NAME} ${TEST_FILE})
    target_link_libraries(${TEST_NAME} PUBLIC alglib-cpp)
    
    add_test(NAME ${TEST_NAME} COMMAND $<TARGET_FILE:${TEST_NAME}>)

endforeach()