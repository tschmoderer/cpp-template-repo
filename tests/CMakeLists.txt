add_executable(test_foo_1 test_foo_1.cpp)
target_link_libraries(test_foo_1 LINK_PUBLIC foo)
add_test(test_1 test_foo_1)

if (NOT TARGET memcheck)
add_custom_target(memcheck
    COMMAND ${CMAKE_CTEST_COMMAND} 
        --force-new-ctest-process --test-action memcheck
    COMMAND cat "${CMAKE_BINARY_DIR}/Testing/Temporary/MemoryChecker.*.log"
    WORKING_DIRECTORY "${CMAKE_BINARY_DIR}")
endif()
