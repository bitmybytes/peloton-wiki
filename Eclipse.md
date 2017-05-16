## Setup

We use `Eclipse CDT` for development. In particular, we recommend using `eclipse-4.4` (Eclipse Luna). Here's a [blog post](http://difusal.blogspot.com/2014/07/how-to-install-eclipse-luna-44-on-ubuntu.html) on installing it on Ubuntu.

First, install the [EGit plug-in](https://www.eclipse.org/egit/?gclid) that enables Eclipse to work with Git repositories.

## Setup Peloton

1.  Create a new workspace for Eclipse (if necessary).
2.  Select `File -> Import -> Git -> Projects` from Git.
3.  When the next panel comes up, click the `Clone` button. In the next window, enter the path to the Github repository into the URI field at Location: `git@github.com:cmu-db/peloton.git`. Then, click `Next`.
4.  In the next panel you can select which branches you wish to clone from the remote repository. You most likely only need to clone the `master` branch. Then, click `Next`.
5.  Select the location on your local machine where you wish to store your cloned repository. You can leave the other defaults. Then, click `Finish`.    
6.  It will now begin to pull down the repository. Once it’s finished, select `peloton`. Then, click `Next`.
7.  In the next panel, select the `Import Existing Projects` option at the top. Then, click `Next`.
8.  In the next page, select the `peloton` checkbox. Click `Finish`. 

## CDT does not recognize C++11 features

GCC needs the compiler option "-std=c++0x" or "-std=gnu++0x" depending on your needs. (please note: check the GCC manual also, because different GCC version may support different switches. For example GCC `4.7` accepts -std=c++11 also.)

Open `Project Properties`->`C/C++ Build`->`Settings`->`Tool Settings`->`GCC C++ Compiler`->`Miscellaneous`->`Other Flags`. Put "-std=c++0x" at the end.

Since CDT 8.3 there is a new "Dialect" option in the compiler option settings, see: https://wiki.eclipse.org/CDT/User/NewIn83#Toolchains

### To make the code completion and code analysis work:

You should add the option -std=c++0x to the scanner discovery in `Project Properties`->`C/C++ Build` ->`discovery Options` in the field "compiler invocation arguments" (note the warning at the bottom of the page).

### You then need to make the indexer update:

Open `Project Properties`->`C/C++ General`->`Index`->`Index source and header files opened in the editor`.  If you are not using project specific settings you need to follow the link to "Configure workspace settings".  This needs to be checked.  Give it a minute to reindex.

Since Eclipse Juno a new Scanner Discovery is integrated in CDT version 8.1. This new scanner has a "hidden" option to set the C++11 feature, see this message: http://www.eclipse.org/forums/index.php/mv/msg/373462/909018/#msg_909018

## Setup GDB in Eclipse
0. Ensure that you have run `../configure` with `-g` and `-ggdb` flags.
1. Select `Project -> Properties -> Run/Debug Settings`
2. Click `New` to add a configuration
3. Click on `Main` tab, enter the project name `Peloton`, and type in the path to executable file `peloton` into `C/C++ Application`. 
4. Click on `Arguments` tab, enter the program arguments: `-D $PATH_TO_DATA_DIRECTORY`. Replace `$PATH_TO_DATA_DIRECTORY` with the absolute path to the directory when you run `initdb` in previous steps.
5. Then you can set breakpoints and debug with it.


## Setup Formatter in Eclipse
1. Install `clang-format` and `cpplint.py` according to the [Requirement](https://github.com/wangzw/CppStyle#requirement)
2. To configure CppStyle globally, go to `Preferences -> C/C++ -> CppStyle` dialog
3. Fill in the path for `Clang-format` and `Cpplint`, and tick `Enable cpplint` and `Run clang-format on file save`.

Have fun hacking !
