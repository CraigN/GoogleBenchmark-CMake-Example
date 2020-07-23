# GoogleBenchmark-CMake-Example

A working example of how to integrate the Google `benchmark` library with 
`CMake` and `Visual Studio`.

## Background

Being familiar with C# benchmarking packages like 
[BenchmarkDotNet](https://github.com/dotnet/BenchmarkDotNet), I was looking for
a similar solution for C++ projects. I stumbled upon 
[benchmark](https://github.com/google/benchmark) but couldn't find a decent 
example on how to get it working quickly with Visual Studio 2019. Ideally I'd 
like to be able to produce benchmark data under Windows and Linux.

## Requirements

The following minimum versions are required to run this example:

* CMake 3.11
* Visual Studio 2019 with the C++ workload 
    OR
  Visual Studio 2019 Build Tools

## Example

This example is based on a slightly modified version of the example used on the
`benchmark` documentation:

```c++
#include <benchmark/benchmark.h>

static void BM_StringCreation(benchmark::State& state) {
  for (auto _ : state)
    std::string empty_string;
}
// Register the function as a benchmark
BENCHMARK(BM_StringCreation);

// Define another benchmark
static void BM_StringCopy(benchmark::State& state) {
  std::string x = "hello";
  for (auto _ : state)
    std::string copy(x);
}
BENCHMARK(BM_StringCopy);

BENCHMARK_MAIN();
```

## Building

The benchmark application needs to be linked against the `benchmark` library to
run. The build is configured to download the latest `benchmark` library using 
`Git` and compile it as a dependency. The following steps should build the 
example using an out-of-source build folder:

```
mkdir build && cd build
cmake ../src
msbuild Benchmarks.sln -p:Configuration=Release
```

## Usage

To run the benchmark execute the following from the `build` folder:

```
StringBenchmarks\Release\StringBenchmarks.exe
```

For additional examples of arguments that can be passed to the test executables
please refer to the `benchmark` documentation
[Running Benchmarks](https://github.com/google/benchmark#running-benchmarks).

## How it Works

The key to getting this to work is by making use of the `CMake` 
[FetchContent](https://cliutils.gitlab.io/modern-cmake/chapters/projects/fetch.html)
module. This will download the `origin/master` from the `benchmark` repository
on Github and build it as a dependency. To reduce the build complexity the flag
`BENCHMARK_ENABLE_TESTING` is set to `NO` to prevent and extra build dependency
against the Google Test library.

## Resources

* Google Benchmark https://github.com/google/benchmark
