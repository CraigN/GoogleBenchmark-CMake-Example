# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.11)

project ("Benchmarks")

# Include sub-projects.
add_subdirectory ("StringBenchmarks")
