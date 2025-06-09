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

First create a new directory in a location of your choosing and name it `hello-world-cmake`. In there you need to create a file called `CMakeLists.txt`. Please be aware of the case of the letters. Write the following text into the file:

```
cmake_minimum_required(VERSION 4.0 FATAL_ERROR)
project(hello-world-cmake)
add_executable(hello-world-cmake src/main.cpp)
```

This will tell CMake, that a minimum version of 4.0 is required and else it throws a fatal error. Next it tells cmake, that we're creating a project called *hello-world-cmake* and lastly that we want to generate an executable from the file *src/main.cpp*.

This file doesn't exist yet so lets create it. First you need to create a new folder called `src` and in there create a new file called `main.cpp`. In there we will write a simple hello world text:

```c++
#include <iostream>
int main(){
  std::cout << "Hello World" << std::endl;
}
```

After that, we should be able to run `cmake -B build .` to generate the build files and store them in the *build* directory. Finally run `cmake --build build` to build the application.

This will generate a new executable inside the `build` folder called `hello-world-cmake`. If you want to test it, go inside the build folder and run it with `./hello-world-cmake` this should now output the string *Hello World*.

Another useful information: You can generate different forms of the build using the `--config` flag. Here you can choose `Debug` or `Release`. Debug will create a build without compiler optimisations, set debug flags and assertions asserted. Release will create a build with compiler optimisations on, without debug flags and the assertions are not asserted. An example is `cmake --build build --config Release`

If you want to, you now also can create a packageroject for your IDE based on your CMakeLists.txt. You list all available projects using `cmake -G`. To select one you need to run something like that:
```c++
cmake -G "Visual Studio 17 2022" -B build .
```

This should create a folder called `build` and in there should be your IDE project.

## CMake JUCE Project
### Setup the Project
Now you should have installed CMake and can use it to build C++ projects. Also you should be able to use it to create project files for your desired IDE, if wanted. However you don't know yet how to use CMake to build a JUCE project.

The first step is to setup a simple JUCE project and then create the `CMakeLists.txt`. Thankfully JUCE provides some CMake examples which can be found inside the `JUCE/examples/CMake` folder. You also can find them [on github](https://github.com/juce-framework/JUCE/tree/master/examples/CMake). In here you can find examples for various projects. Copy the folder for the application, that you want to create. In my case this is the `AudioPlugin` folder.

**Copy this folder** into a directory of your choice (probably your repositories folder). When you now try to build the application using CMake, it wont work just yet, because CMake doesn't know where JUCE is located. We can fix that by **copying our JUCE folder into the project**. In this case, we also have all the files, that are used to create the application in one directory and it will always work, even when JUCE removes some functions.

Your project should now look like this:

```
AudioPlugin
|-JUCE/
|-CMakeLists.txt 
|-PluginEditor.cpp
|-PluginEditor.h
|-PluginProcessor.cpp
|-PluginProcessor.h
```

Next, we need to adjust the `CMakeLists.txt` to tell CMake where JUCE is located in the project. This can be done by **uncommenting a line inside of the example CMakeLists.txt**: `# add_subdirectory(JUCE)` to `add_subdirectory(JUCE)`.


Lastly we can rename the variables to our likings. For example we can change the project name, plugin name, plugin manufacturer code and the formats that our plugin will be exported to. In this tutorial, we wont do any of that because we don't really need to.

### Build the project
We now can build our project using the CMake cli:

Generate build files
```bash
cmake -B build .
```

Build the application
```bash
cmake --build build
```

The compiled application should now be located in `build/<ProjectName>_artefacts`.

### Add new files to the project
You often have multiple files outside of the default ones and trying to build them with the default CMakeLists.txt wont work. However they can be added pretty easily and you just need to add a few lines to the `CMakeLIsts.txt`:

```CMakeLists
target_sources(AudioPluginExample
    PRIVATE
        PluginEditor.cpp
        PluginProcessor.cpp
        <YourFileName>.cpp
      )
```

### Add JUCE modules to the project
If you want to add a new JUCE module, like for example the DSP module, you need to add those to the project like this:

```CMakeLists
target_link_libraries(AudioPluginExample
    PRIVATE
        juce::juce_audio_utils
        juce::juce_dsp
    PUBLIC
        juce::juce_recommended_config_flags
          juce::juce_recommended_lto_flags
          juce::juce_recommended_warning_flags)
```
