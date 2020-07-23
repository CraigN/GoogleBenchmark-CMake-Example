# CMakeList.txt : CMake project for StringBenchmarks, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.11)

# Include Google Benchmark
include(../cmake/GoogleBenchmark.cmake)

# Add source to this project's executable.
add_executable (StringBenchmarks "StringBenchmarks.cpp" "StringBenchmarks.h")

# Link Google Benchmark to the project
target_link_libraries(StringBenchmarks benchmark::benchmark)

# Link Shlwapi to the project
if ("${CMAKE_SYSTEM_NAME}" MATCHES "Windows")
    target_link_libraries(StringBenchmarks Shlwapi)
endif()

# TODO: Add tests and install targets if needed.
