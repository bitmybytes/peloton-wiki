### Build and Run ALL Unit Test Cases

By default, all the test cases are first built and then run under [Valgrind](https://github.com/cmu-db/peloton/wiki/Valgrind). To build and run all the unit test cases :

```Shell
make check
```

**PARALLEL MAKE** 

If your machine has more than `8 GB` DRAM and `4 physical cores`, you can increase the [concurrency settings](https://www.gnu.org/software/make/manual/html_node/Parallel.html) of make.

```Shell
make check -j4
```

### Build and Run INDIVIDUAL Unit Test Case

Here's the command to build an individual test:

```Shell
make $TEST_NAME
```

`EXAMPLE:`
```Shell
make sample_test
```
To run an [individual test](https://cmake.org/Wiki/CMake/Testing_With_CTest#Running_Individual_Tests) using `ctest`, list the test cases:

```Shell
ctest -N
```

Then run it thus:

```Shell
ctest -I 26,26 -V
```
### Valgrind Command

***ADVANCED:*** Here's the `valgrind` command to run an individual test (once it has already been built) :

```Shell
valgrind "--trace-children=yes" "--leak-check=full" "--track-origins=yes" "--soname-synonyms=somalloc=*jemalloc*" "--error-exitcode=1" "--suppressions=/$LOCATION_OF_PELOTON_SOURCE_DIR/third_party/valgrind/valgrind.supp /$LOCATION_OF_PELOTON_BUILD_DIR/test/$TEST_NAME
```

`EXAMPLE:`
```Shell
valgrind "--trace-children=yes" "--leak-check=full" "--track-origins=yes" "--soname-synonyms=somalloc=*jemalloc*" "--error-exitcode=1" "--suppressions=/home/parallels/git/peloton/third_party/valgrind/valgrind.supp" ./test/sample_test
```