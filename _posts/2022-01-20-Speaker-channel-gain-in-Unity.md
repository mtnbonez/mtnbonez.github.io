---
layout: post
title: "Speaker channel gain in Unity"
date: 2022-01-20 21:07:00 -0800
featured_image: '/images/blog/Speaker-channel-gain-in-Unity/sliders.gif'
categories: unity, audio
exercept: Looking for an easy way to attenuate volume for individual speaker channels? Unity's already built a DSP plugin just for you!
---

Looking for an easy way to attenuate volume for individual speaker channels in Unity? Unity's already built a DSP plugin just for you!

### Background

Working with lower-level audio in Unity, I struggled finding a simple solution for attenuating [low-frequency effects](https://en.wikipedia.org/wiki/Low-frequency_effects) (LFE) channel gain without needing to roll up my sleeves and write a [digital signal processing](https://en.wikipedia.org/wiki/Digital_signal_processing) (DSP) effects plugin. 

Although I highly recommend anyone interested in learning about audio programming to take a swing at writing their own DSP plugins, it's a pretty deep rabbit hole for the uninitiated. Thankfully, Unity already has a solution!

### Attenuating individual speaker channels

Unity provides a staggering 26 DSP plugins in their Native Audio Plugin SDK. However, the [documentation](https://docs.unity3d.com/Manual/AudioMixerNativeAudioPlugin.html) ain't so great - their link to the source currently points to a [BitBucket repo](https://bitbucket.org/Unity-Technologies/nativeaudioplugins) that no longer exists (here's the official [GitHub repo](https://github.com/Unity-Technologies/NativeAudioPlugins)) and they don't go into many details about what the actual plugins do.

Here's a quick way to get individual speaker channel attenuation working in your project:

* Clone the [GitHub repo](https://github.com/Unity-Technologies/NativeAudioPlugins) & navigate to the **`Plugins`** [folder](https://github.com/Unity-Technologies/NativeAudioPlugins/tree/master/Assets/Plugins) on your computer.
* **MacOS**: Locate the entire **AudioPluginDemo.bundle**.
* **Windows**: Navigate to your particular architecture's sub-folder (if you're running Windows 10/11 on modern hardware, you want [x86_64](https://github.com/Unity-Technologies/NativeAudioPlugins/tree/master/Assets/Plugins/x86_64)) and locate the **`AudioPluginDemo.dll`**
* Pull your respective plugin artifact into your Unity project - creating an **`Assets/Plugins`** folder and putting it there is the preferable way. ![](/images/blog/Speaker-channel-gain-in-Unity/macOSPluginBundle.png)
* Add the **`Demo - LevelMixer`** to your target **Mixer**. (Check out Unity's manual on [how Mixers work](https://docs.unity3d.com/Manual/AudioMixer.html)) ![](/images/blog/Speaker-channel-gain-in-Unity/selectPlugin.gif)
* Use the sliders in the plugin to attenuate your desired speaker channel. (In the [zero-based channel index](https://en.wikipedia.org/wiki/Surround_sound#Channel_identification), LFE is channel 3, which corresponds to **Gain4** on this plugin) ![](/images/blog/Speaker-channel-gain-in-Unity/adjustingGain.gif)

### Building the plugins from source

[Othniel Cundangan](https://www.linkedin.com/in/othnielcundangan/) wrote an [excellent article](https://medium.com/@othnielcundangan/how-to-use-unitys-native-audio-plugin-sdk-on-macos-f7e1bdbc8141) around building the plugins from source from a MacOS perspective. If there's any interest on how to build from source for Windows using Visual Studio, I would be glad to do a write up - [let me know](https://github.com/mtnbonez/mtnbonez.github.io/issues/1)!

### Why am I not seeing 8 channels in my Mixer?

Check out your project's Audio settings in **`Edit>Project Settings>Audio`** - change **Default Speaker Mode** to **Surround 7.1** forcibly show all 8 channels in your mixers.

![](/images/blog/Speaker-channel-gain-in-Unity/audioSettings.png)

Take note, your Unity speaker settings will still be downmixed to whatever speaker setup you have registered in your operating system's audio settings.

### Comments, criticism, or ideas for the future?

Head over to this post's [issue page](https://github.com/mtnbonez/mtnbonez.github.io/issues/1) and put your thoughts in there!