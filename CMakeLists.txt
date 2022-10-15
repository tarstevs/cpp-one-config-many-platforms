cmake_minimum_required(VERSION 3.21)
project (sections-of-cpp CXX)

include(CTest)

# GoogleTest setting relevant for Windows
# See https://github.com/google/googletest/blob/main/googletest/README.md
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# The following is what would appear here if the library "range-v3" were added to vcpkg.json (this is just an example
# for the next library that needs to be added to the project):
#find_package(range-v3 REQUIRED)
find_package(GTest REQUIRED) # linking to the gtest library happens in the CMakeLists.txt file found in the tests directory

add_executable(main src/main.cpp)
target_compile_features(main PUBLIC cxx_std_20)


# The following is what would appear here if the library "range-v3" were added to vcpkg.json (this is just an example
# for the next library that needs to be added to the project):
#target_link_libraries(main
#       PRIVATE
#      range-v3::range-v3
#     )

# eigen3 is a header only library, so we only need to include the path to the Eigen
# directory so that calls like `#include <Eigen/Dense>` will work within our project.
# (Note: We are still using vcpkg to download the eigen headers into this repository
# using vcpkg.json)
find_path(EIGEN_INCLUDE_DIR Eigen)
include_directories(${EIGEN_INCLUDE_DIR})

# for unit tests with GoogleTest
add_subdirectory(tests)