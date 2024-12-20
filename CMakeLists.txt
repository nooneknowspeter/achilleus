cmake_minimum_required(VERSION 3.22)

project(nooneknows)

# Always use the newest C++ standard on green-field projects if possible.
# Currently, JUCE supports only C++ 20 cross-platform.
set(CMAKE_CXX_STANDARD 20)

# libraries folder assigned to var
set(LIB_DIR ${CMAKE_CURRENT_SOURCE_DIR}/libs)

# downloads cpm
include(cmake/cpm.cmake)

# This commands downloads AND configures JUCE. It sets up some variables, like JUCE_SOURCE_DIR.
CPMAddPackage(
    NAME JUCE
    GIT_TAG 8.0.4
    VERSION 8.0.4
    GITHUB_REPOSITORY juce-framework/JUCE
    SOURCE_DIR ${LIB_DIR}/juce
)

# Adds googletest.
CPMAddPackage(
    NAME GOOGLETEST
    GITHUB_REPOSITORY google/googletest
    GIT_TAG v1.15.2
    VERSION 1.15.2
    SOURCE_DIR ${LIB_DIR}/googletest
    OPTIONS
        "INSTALL_GTEST OFF"
        "gtest_force_shared_crt ON"
)

# This command allows running tests from the "build" folder (the one where CMake generates the project to).
enable_testing()

# Adds all the targets configured in the "plugin" folder.
add_subdirectory(plugin)

# Adds all the targets configured in the "test" folder.
add_subdirectory(test)
