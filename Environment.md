## Prologue 

This page contains information that is intended to help start hacking on Peloton. It covers a wide set of topics related to software development, like development environment, debugging, version control etc. We are only attempting to provide biased suggestions that we think are invaluable for low-level software development. Feel free to deviate from them in case you are comfortable with other tools that solve similar problems.

## Operating System

We prefer the `Linux` OS for development and testing. You can use any other OS for development as long as your modified source code can be built and run on Linux. 

In case you are a `Mac OS` or `Windows` user, we encourage you to consider using `Virtual Box` and `Vagrant`. `Virtual Box` is a hypervisor for x86 computers, and `Vagrant` is a tool for sharing easy to configure virtual development environments. More information is available [here](https://github.com/cmu-db/peloton/wiki/Installation). 

## Language

We are developing Peloton in `C++`. In particular, we are following the `C++11` standard. C++ provides a lot of leeway in DBMS development compared to other high-level languages. For instance, it supports both manual and automated memory management, varied styles of programming, stronger type checking, different kinds of polymorphism etc. 

Here's a list of useful references : 

* [CPP Reference](http://en.cppreference.com/w/cpp) is an online reference of the powerful `Standard Template Library` (STL).
* [C++ FAQ](https://isocpp.org/faq) covers a lots of topics.

Here's a list of C++11 features that you might want to make use of:

* `auto` type inference
* Range-based `for` loops
* Smart pointers, in particular `unique_ptr`.
* STL data structures, such as `unordered_set`, `unordered_map`, etc.
* Threads, deleted member functions, lambdas, etc.

## Comments, Formatting, and Libraries

Please **comment** your code. Comment all the class definitions, non-trivial member functions and variables, and all the steps in your algorithms. [Here's](https://github.com/cmu-db/peloton/blob/master/src/backend/storage/tile.h) an example.  

We follow the [Google C++ style guide](https://google.github.io/styleguide/cppguide.html). As they mention in that guide, these rules exist to keep the code base manageable while still allowing coders to use C++ language features productively.
Make sure that you follow the [naming rules](https://google.github.io/styleguide/cppguide.html#General_Naming_Rules). For instance, use `class UpperCaseCamelCase` for type names, `int lower_case_with_underscores` for variable/method/function names.

Please refrain from using any libraries other than the `STL` (and `googletest` for unit testing) without contacting us.
 
## Directory Structure

Organize source code files into relevant folders based on their functionality. Separate binary files from source files, and production code from testing code. 

In general, the `src` directory contains all the production code, the `test` directory contains all the testing code, and the `build` directory contains all the built binary files. Within the `src` directory, `src/storage` contains files related to our storage engine, while `src/index` contains files related to the indexes, etc..

## Source Code Management

We exclusively use `git` for source code management, and `github` for collaboration. Here's a simple [guide](https://rogerdudler.github.io/git-guide/) for using it. If you have never used a tool like git, I am sure that you will soon wonder how you managed to live without it. In case you want to learn more, here's a free [book](http://git-scm.com/book).

Please update or add a `.gitignore` file to exclude unwanted files (e.g. the build directory with binary files, backup/temporary files of your editor/IDE, large files containing test data, etc.) from the repository.

## Build System

We use `cmake` for building Peloton. In particular, we use `cmake` for automatically generating `Makefile` files. You will probably _not_ need to add file names to existing cmake files (with extension `CMakeLists.txt`) since the cmake script automatically collects all files with `cpp` extension.

In case you are curious about `cmake`, here's a short [introduction](http://derekmolloy.ie/hello-world-introductions-to-cmake/).

## Compiler

We use the `g++` compiler, which is part of the GNU compiler collection. [Here's](https://gcc.gnu.org/projects/cxx0x.html) more information on the status of C++11 support in GCC. In particular, we suggest g++ compilers with version higher than [4.7](https://gcc.gnu.org/gcc-4.7/cxx0x_status.html). Here's a list of useful compiler flags:

* `-std=c++11`: Enables C++11 support
* `-g`: Produces debugging information in the OS's native format.
* `-ggdb`: Produces debugging information specifically intended for gdb.
* `-O0`: Optimize option that reduces compilation time and makes debugging more reliable.
* `-O3`: Increases both the compilation time and the performance of the generated code. Use this when running benchmarks.
* `-Wall`: Generate helpful warnings. Do not ignore them! In fact, force yourself to deal with warnings by handling them as errors with the `-Werror` compiler flag.

## Debugging Tools

We encourage you to use a debugger to find bugs, rather than relying on `printf` statements. Specifically, we recommend `gdb`, the GNU debugger. Most development platforms have a graphical `gdb` front-end, but the command line can already be very helpful for debugging program crashes. You can consider using the curses-based interface for gdb, called `cgdb`.

[Here's](https://github.com/cmu-db/peloton/wiki/GDB) some information on debugging Peloton using gdb.

If your program behaves in "mysterious" (a.k.a. "non-deterministic" ways), `valgrind` is your friend. It can automatically detect many memory management and threading bugs. In particular, its `memcheck` tool is useful for finding illegal accesses to memory, uninitialized reads and much more. Check out this [blog post](http://billiob.net/blog//20140330_vgdb.html) on the interaction between GDB and Valgrind.

[Here's](https://github.com/cmu-db/peloton/wiki/Valgrind) some information on debugging Peloton using valgrind.

It is a good habit to make sure that Peloton passes all the memchecked unit tests every time you commit a set of changes with `git`.

## Development Environment

`Eclipse` is an awesome IDE that provides a nice project workspace, and has an extensible plug-in system for customizing the environment. It is really hard to match the capabilities of Eclipse, in particular its refactoring features, with editors like `emacs` or `vim` and a command line. 

[Here's](https://github.com/cmu-db/peloton/wiki/Eclipse) some information on setting up Eclipse to develop Peloton.

## Unit Testing

Unit tests are critical for ensuring the correct functionality of your modules and reduce time spent on debugging. It can help prevent regressions. We use `googletest`, a nice unit-testing framework for C++ projects. 

We encourage you to write unit test cases for each class/algorithm that you have added or modified. For instance, look at this [test suite](https://github.com/cmu-db/peloton/blob/master/tests/storage/tuple_test.cpp) for testing the functionality of tuples. Try to come up with test cases that make sure that the module exhibits the desired behavior. Some developers even suggest writing the unit tests before implementing the code. Make sure that you include corner cases, and try to find off-by-one errors.

`gcov` is a code coverage analysis tool that tells us how much of the code base is covered by the unit tests. We have already integrated it in our build system.

## Profilers

Profilers help better understand the performance of Peloton and the environment in which it is running. We suggest `perf` and `strace` tools for profiling. [Here's](https://github.com/cmu-db/peloton/wiki/Perf) some information on profiling Peloton using perf.
 
## Terminal Multiplexer

A terminal multiplexer lets you switch easily between several programs in one terminal. This is particularly useful if you are benchmarking or developing on a remote server. We recommend the `tmux` tool. [Here's](http://lukaszwrobel.pl/blog/tmux-tutorial-split-terminal-windows-easily) a short tutorial, and [here's](http://www.dayid.org/comp/tm.html) a nice cheat sheet.

## Shell

We suggest the `zsh` shell for development. In particular, along with [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh), it provides an amazing command line experience with its autocomplete features. [Here's](http://mikebuss.com/2014/02/02/a-beautiful-productive-terminal-experience/) more information on improving the terminal experience.

## Epilogue

If you are already comfortable with most of these tools (and maybe even more), and want to hack on Peloton -- then that's awesome ! Drop me a line at <mailto:jarulraj@cs.cmu.edu>.

