# Setup CMake with JUCE

If you are already creating JUCE plugins for a while or you maybe want to be more flexible while using JUCE, you may came across [CMake](https://cmake.org/). You can imagine it like being a better Projucer, but also a bit more complicated. So if you are a beginner, you might want to learn Projucer before learning CMake.

Another advantage of CMake is that you can integrate third party libraries very easy like the machine learning library [libtorch](https://docs.pytorch.org/docs/main/cpp_index.html) which is needed for most ai-plugins.

## Installing CMake
### Windows
To install CMake on Windows, go to the [homepage of CMake](https://cmake.org/) and follow the instructions. After that you should be able to open Powershell and type `cmake`. There should be an output of how to use CMake.

### MacOS
On MacOS, CMake is very easy to install using the package manager [Homebrew](https://brew.sh/). Follow the instructions on the website to install Homebrew. After you installed homebrew, you can just run the following command in the Terminal app to install CMake:
`brew install cmake`

### Linux
If you are on linux, you should already be familiar with the concepts of package managers and there is probably a package for CMake. If not, you should be able to download a compiled version on the [website of CMake](https://cmake.org/). However in the following list there are the commands for various distributions:

- Debian/Ubuntu: `sudo apt install cmake`
- Arch: `pacman -Syu cmake`

## Using CMake

### Test application
If everything done correctly, you now should have CMake and an IDE installed. If you are new to CMake it's good if you learn the basics. Lets create a simple test application for this.

First create a new directory in a location of your choosing and name it *hello-world-cmake*. In there you need to create a file called *CMakeLists.txt*. Please be aware of the case of the letters. Write the following text into the file:

```
cmake_minimum_required(VERSION 4.0 FATAL_ERROR)
project(hello-world-cmake)
add_executable(hello-world-cmake src/main.cpp)
```

This will tell CMake, that a minimum version of 4.0 is required and else it throws a fatal error. Next it tells cmake, that we're creating a project called *hello-world-cmake* and lastly that we want to generate an executable from the file *src/main.cpp*.

This file doesn't exist yet so lets create it. First you need to create a new folder called *src* and in there create a new file called *main.cpp*. In there we will write a simple hello world text:

```c++
#include <iostream>
int main(){
  std::cout << "Hello World" << std::endl;
}
```

After that, we should be able to run `cmake -B build .` to generate the build files and store them in the *build* directory. Finally run `cmake --build build` to build the application.

This will generate a new executable inside the *build* folder called *hello-world-cmake*. If you want to test it, go inside the build folder and run it with `./hello-world-cmake` this should now output the string *Hello World*.

Another useful information: You can generate different forms of the build using the `--config` flag. Here you can choose `Debug` or `Release`. Debug will create a build without compiler optimisations, set debug flags and assertions asserted. Release will create a build with compiler optimisations on, without debug flags and the assertions are not asserted. An example is `cmake --build build --config Release`

If you want to, you now also can create a packageroject for your IDE based on your CMakeLists.txt. You list all available projects using `cmake -G`. To select one you need to run something like that:
```c++
cmake -G "Visual Studio 17 2022" -B build .
```

This should create a folder called *build* and in there should be your IDE project.
