# What is JUCE?
JUCE is an open-source cross-platform C++ application framework, used for the development of desktop and mobile applications. JUCE is used in particular for its GUI and plug-ins libraries. It is dual licensed under the GPLv3 and a commercial license.

The aim of JUCE is to allow software to be written such that the same source code will compile and run identically on Windows, macOS and Linux platforms. It supports various development environments and compilers.


## Features
JUCE provides a range of functions, covering user-interface elements, graphics, audio, XML and JSON parsing, networking, cryptography, multi-threading, an integrated interpreter that mimics ECMAScript's syntax and various other commonly used features.

A notable feature of JUCE when compared to other similar frameworks, like Qt or GTK, is its large set of audio functionality; this is because JUCE was originally developed as a framework for Tracktion, an audio sequencer, before being split off into a standalone product.

JUCE comes with wrapper classes for building audio and browser plugins. When building an audio plugin, multiple plugin formats can be selected for build targets. Those include VST & VST3, RTAS, AAX and Audio Units.

## Tools

### Projucer
The "Projucer" is an IDE tool for creating and managing JUCE projects. When the files and settings for a JUCE project have been specified, the Projucer automatically generates a collection of 3rd-party project files to allow the project to be compiled natively on each target platform. It can currently generate Xcode projects, Visual Studio Projects, Linux Makefiles, Android Ant builds and CodeBlocks projects.

### AudioPluginHost
The "AudioPluginHost" is a standalone application included with JUCE that allows users to load, test, and route audio plugins in a flexible environment. Designed primarly for plugin development and testing, it supports both VST and AU plugin formats and provides a real-time visual interface for managing plugin chains. With its built-in graph editor, users can freely connect audio and MIDI paths between loaded plugins, making it an essential tool for quickly verifying plugin behaviour outside of a DAW.