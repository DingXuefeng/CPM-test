cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

# create project
project(CPM-test)

# add dependencies
include(cmake/CPM.cmake)
CPMAddPackage(
        NAME googletest
        GITHUB_REPOSITORY google/googletest
        GIT_TAG release-1.8.1
        VERSION 1.8.1
        OPTIONS
        "INSTALL_GTEST OFF"
        "gtest_force_shared_crt ON"
        "BUILD_GMOCK OFF"
)

enable_testing()
include(GoogleTest) # necessary for gtest_discover_tests, not needed for target_link_libraries
add_executable(myTest tests.cc)
target_link_libraries(myTest PRIVATE gtest gtest_main)
gtest_discover_tests(myTest )