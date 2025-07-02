# Changing fonts

If you want to personalize the GUI of your audio plugin, you should change the font to another one than the default one. Maybe you got that one font that you really want to use. In this guide there is a tutorial on how to do that.

Generally there are two ways of changing the font:

1. Use a system font, that is installed on your OS. This however has a huge flaw. Somebody else might not have this font installed and your plugin might not work correctly for them.

2. Embed the font you want to use into the plugin. This will work regardless if the user has this font installed or not.

In this tutorial we're going to take a look at the second option.

## Changing the font with Projucer


## Changing the font with CMake
First of all, we will use the nerdfont [*3270 Nerd Font*](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/3270.zip) for this project but you can use whatever `.ttf`-file that you want.

We will put the font into a new folder; The `Assets`-folder. If you want to use more fonts, you might just drop them into here. The project structure should now look like this:

```
|assets
  |-3270NerdFont.ttf
|-PluginEditor.h
|-PluginProcessor.cpp
|-PluginProcessor.h
|-PluginProcessor.cpp
```

Next we need to tell *cmake* that we want to actually use this font in our project and that it should add it into the binary file. This is done by telling `juce_add_binary_data` that it should include our font:

```CMakeLists
juce_add_binary_data(BinaryData 
  SOURCES
    assets/_3270NerdFont.ttf)
```

Now we should be able to use the font in our project. Lets try to visualize it by changing the font of a label. First we actually need a label defined in the `PluginEditor.h` and also make it visible in the `PluginEditor.cpp`, however I assume, that you already know how to do that.

Next we simply need to create a [Typeface](https://docs.juce.com/master/classTypeface.html) and set it as our font. Here we also apply a custom height for the font. Since you should do the initialisation of the GUI components in the constructor, we will do just that. First we create a type of `juce::Typeface::Ptr` and tell it, that it should point to our font (3270 Nerd Font in this example). Next, we set the font and apply a custom height. This is done by the `label.setFont();` stuff. The last two lines `addAndMakeVisible(label)` and `setSize(600,400)` you should already know of and these just make the label visible and set the window size.

```c++
AudioProcessorEditor::AudioProcessorEditor (AudioProcessor& p)
    : AudioProcessorEditor (&p), audioProcessor (p)
{
    static juce::Typeface::Ptr customTypeface = juce::Typeface::createSystemTypefaceFor(
        BinaryData::_3270NerdFont_ttf,
        BinaryData::_3270NerdFont_ttfSize
    );
    label.setFont(juce::FontOptions(customTypeface).withHeight(40));
    label.setText("custom font label", juce::NotificationType::dontSendNotification);

    addAndMakeVisible(label);

    setSize (600, 400);
}
```
