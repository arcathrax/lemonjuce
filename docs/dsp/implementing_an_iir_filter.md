# Implementing an IIR Filter

## What's an IIR Filter?
An Infinite Impulse Response (IIR) filter is a type of digital or analog filter used in signal processing to modify signals by selectively attenuating or amplifying certain frequencies. Unlike finite impulse response (FIR) filters, which have a finite duration response to an impulse input, IIR filters theoretically continue their response indefinitely, hence the term "infinite impulse response".

In JUCE it is generally used to create filters of various types, like a high-shelf filter, a low-cut filter and bandpass filter. Designing those filters can be very hard and sometimes even create an unstable output. Thankfully there is a JUCE helper class, that does this part for us.

## Implementation
First off, you need to create the filter and add it to your [ProcessorChain](/dsp/implementing_a_processorchain):

**file:** `PluginProcessor.h`

```c++
using ProcessorChain = juce::dsp::ProcessorChain
<
  juce::dsp::IIR::Filter<float>
>;
```

Don't forget to update your enum, if you're using one.

**file:** `PluginProcessor.h`

```c++
enum
{
  filterIndex
};
```

Next create a function, that reads the parameters and adjusts the filter. This function should be called during the playback, so we can adjust the filters settings in real time. Lets call this function `updateFilter()`. Since we just want to change the settings and don't actually process any audio, we don't need any return type. Also we won't use this function outside of the PluginProcessor-class so we can create it in the private section:

**file:** `PluginProcessor.h`

```c++
private:
  void updateFilter();
```

### Peak Filter

Now lets define the function. We first start of by reading any parameters from our [APVTS](/parameter_handling/implementing_an_apvts) and storing them in a temporary variable, so we can read them better. Please note, that you **need to have parameter's named `Peak Freq`, `Peak Quality` and `Peak Gain`** or else this wont work. Next, we will calculate the coefficients. Thankfully JUCE has a helper class, that can help us out. This is the `juce::dsp::IIR::Coefficients<float>` part. Here we also define, what type of filter we want. Lastly, we will replace the old coefficients with the new ones. Here we assume, that you have a stereo audio plugin with a `leftChain` and a `rightChain`.

**file:** `PluginProcessor.cpp`

```c++
void AudioProcessor::updateFilter()
{
  // storing the parameters
  auto peakFreq = apvts.getRawParameterValue("Peak Freq")->load();
  auto peakQuality = apvts.getRawParameterValue("Peak Quality")->load();
  auto peakGain = apvts.getRawParameterValue("Peak Gain")->load();
  
  // calculating the coefficients
  auto coefficients = juce::dsp::IIR::Coefficients<float>::makePeakFilter(
  peakFreq,
  peakQuality,
  juce::Decibels::decibelsToGain(peakGain)
  );
  
  *leftchain.get<filterIndex>().coefficients = *coefficients;
}
```

## Update the Filter

Now we just need call this function every time, audio is being processed or prepared. This is done in the `prepareToPlay` and in the `processBlock`. We also should update the filters after we loaded the plugin's state.

**file:** `PluginProcessor.cpp`

```c++
void AudioProcessor::prepareToPlay (double sampleRate, int samplesPerBlock)
{
  // existing code
  
  updateFilter();
}
```

```c++
void AudioProcessor::processBlock (juce::AudioBuffer<float>& buffer, juce::MidiBuffer& midiMessages)
{
  // existing code
  
  updateFilter();
}
```

```c++
void SimpleEQAudioProcessor::setStateInformation (const void* data, int sizeInBytes)
{
    auto tree = juce::ValueTree::readFromData(data, sizeInBytes);
    if (tree.isValid())
    {
        apvts.replaceState(tree);
        updateFilters();
    }
}
```

Now your filter should work and usable.
