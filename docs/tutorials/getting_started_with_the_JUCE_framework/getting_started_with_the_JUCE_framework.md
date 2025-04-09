# Getting started with the JUCE framework
To start as a beginner, I clearly suggest you to use *Projucer*. This is a application, provided by JUCE, to simplify the configuration and setup for your project. Here you will learn, how to install and use it with [Xcode](https://developer.apple.com/xcode/) (macOS) or [Visual Studio](https://visualstudio.microsoft.com/) (Windows).

## Prerequisites
- Completed [Whats JUCE and how to use it](/tutorials/whats_juce_and_how_to_use_it/whats_juce_and_how_to_use_it)

## Download JUCE
First, you need to download JUCE. You can download juce [here](https://juce.com/download/). Scroll a bit down and under *Download from this website*, choose your operating system.

## Install JUCE
JUCE should now be downloading as a `.zip`-file. Extract this. You now should have a `JUCE`-folder. I recommend you to change the location of this folder. This folder contains every file from the JUCE framework and will need those. I suggest you to put the files into your applications folder:

- Windows: `C:\Program Files`
- Mac: `/Applications`

## create start menu entry for projucer
If you are on Windows, I suggest you to create a start menu entry. This can be done by going to this path: `C:\Users\YOURUSERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs`.

>You have tho change `YOURUSERNAME` to your actual username.

Create a link to `C:\Program Files\JUCE\Projucer.exe`.

Now if you search for *Projucer* in the windows search, it should now show an application.

## Set global paths
Since you could have *Projucer* in any file location, we need to set the path for the JUCE modules. Those are the tools, JUCE provides you. *Projucer* is manages those modules and sets them as a dependency for your project. Because of this, *Projucer* needs to know, where those modules are and you need to set this up.

First you need to open *Projucer*. On the top left click on `File>Global Paths...`. You need to set those paths:

- Path to JUCE: `C:\Program Files\JUCE`
- JUCE Modules: `C:\Program Files\JUCE\modules`

and then close this window.


Now you should be all setup to [create a JUCE project](/tutorials/create_a_juce_project/create_a_juce_project).