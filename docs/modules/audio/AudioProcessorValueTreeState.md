# AudioProcessorValueTreeState

## Description
This class helps to store [AudioProcessor](...)'s entire state. This class is very useful to store [Parameter](...)'s inside and handle the save and load function. 

## Features
You too can create [SliderAttachment](...)'s and [ButtonAttachment](...)'s. With those *Attachments*, you don't need to read and write every change of the slider/button. You just need to tell the Attachment, what slider to attach to.

## Implementation
This is a in depth implementation of an APVTS. Here we first define a helper function (`createParameterLayout()`) and then the apvts. 

File: `PluginProcessor.h`
```cpp
public:
    // define the function to create the parameters
    juce::AudioProcessorValueTreeState::ParameterLayout createParameterLayout();
    
    // define the apvts
    juce::AudioProcessorValueTreeState apvts{ *this, nullptr, "Parameters", createParameterLayout() };
```


Next we implement the helper function:

Since we need to return a [*ParameterLayout*](...), we initialize one at the start of the function[1]. After that, we create a [*AudioParameterFloat*](...) called `Gain`. The gain-Parameter can have values from `1.f`-`12.f` and has a step size of `0.000001f`. The skew-factor of `1.f`. The default value of the parameter is `1.f`[2]. Also, we create a [*AudioProcessorParameterGroup*](...) and we call this `misc_parameters`. We too add the parameter `gain` to the `misc_parameters` [3]. The `misc_parameters` need to be added to the `layout` and this we do next[4]. And lastly, we return the `layout`[5].

File: `PluginProcessor.cpp`
```cpp
juce::AudioProcessorValueTreeState::ParameterLayout 
ExoDistAudioProcessor::createParameterLayout()
{
    juce::AudioProcessorValueTreeState::ParameterLayout layout; // [1]
    
    auto gain = std::make_unique<juce::AudioParameterFloat>
    (
        juce::ParameterID { "Gain", 1 }, 
        "Gain", 
        juce::NormalisableRange<float(1.f, 12.0f, 0.000001f, 1.f), 1.0f
    ); // [2]
    
    auto miscParameters = std::make_unique<juce::AudioProcessorParameterGroup>
    (
        "misc_parameters",
        "misc_parameters",
        "|",
        std::move(gain)
    ); // [3]
    
    layout.add
    (
        std::move(miscParameters) // [4]
    );
    
    return layout; // [5]
}
```

You may be asking, why we create a [*AudioProcessorParameterGroup*](...), if we just have one parameter. This we do for the future. You maybe want to have multiple parameters and group them. This is how this can be done. You maybe wanth a parametergroup to hold all the synth parameters, another group to hold the misc parameters and maybe you have some effects inside there too and you want to group those too. This can be done very easily with this setup.