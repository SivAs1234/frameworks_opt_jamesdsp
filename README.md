# JamesDSPManager (Audio Effect Digital Signal Proccessing library for Android)
GUI is based on Omnirom DSP Manager and able to run in all recent Android rom include Samsung, AOSP, Cyanogenmod. 
This app in order to improve your music experience especially you want realistic bass and more natural clarity.
We don't work too much around with modifying Android framework.

##### Basic:

1. Compression
2. Bass Boost

   --> 4 order IIR and 1023/4095 order FIR linear phase low pass bass boost
3. Reverberation

   --> GVerb and Progenitor 2
4. 10 Band Hybrid Equalizer (1 low shelf, 8 bands shelves, 1 high shelves)(Different bands designed with different filter order)
5. Stereo Widen
6. Convolver

   --> Only support stereo
   
   --> Samples per channels should less than 500000

## Important
### FAQ
#### 1. Computation datatype?

A: Float32

#### 2. What is Clip control?

A: When effect strength going extreme, value will go beyond -1.0 / +1.0 range, this will cause clipping.

   Effect provide you more option, that is Hyperbolic tangent function/tanh() that will clip the value more natural.
   
   But using tanh() will change the waveform even signal is haven't clip.

#### 3. Bass boost filter type?

A: Effect have 3 algorithms to boost low frequency, the first one is the traditional one from previous release, based on IIR Filter.

   Linear phase filter type is work on convolution basis. When user change the bass boost parameter, driver will compute new low pass filter impulse response.
   
   4095 order FIR filter should work on all frequency listed on options, 1023 order should work well above 80Hz.

#### 4. What is the Misc folder

File reverbHeap is modified Progenitor 2 reverb, memory allocation is using heap not stack, it will be useful when you play around with Visual Studio, because VS have 1Mb stack allocation limit...

#### 5. Why you change the Effect structure?

A: This is the only way to full control all DSP effects...

#### 6. Why libjamesdsp.so so big?

A: Because of fftw3 library linked.

#### 7. Why open source? Any license?

A: Audio effects actually is not hard to implement, I'm don't think close source is a good idea. Many audio effects is exist in the form of libraries, or even in thesis, everyone can implement it...
   This is published under GPLv2.

#### 8. Why no effect after installed?

A: Check step in release build ReadMe.txt.
   audio_effects.conf is file for system to load effect using known UUID, you can just add
   ```
  jdsp {
    path /system/lib/soundfx/libjamesdsp.so
  }
   ```
   ### under
   ```
   bundle {
    path /system/lib/soundfx/libbundlewrapper.so
  }
   ```
   ### AND
   ```
   jamesdsp {
    library jdsp
    uuid f27317f4-c984-4de6-9a90-545759495bf2
  }
   ```
   ### under
   ```
   effects {
   ```

##### On development:
1. Parameterized Room Convolution

	-->May be I will implement this in my other repository: [Complete C implementation of Room Impulse Response Generator]
	(https://github.com/james34602/RIR-Generator)

##### TODO:
1. More optimization on all component (JAVA, Native)

Now work on AOSP, Cyanogenmod, Samsung on Android 5.0, 6.0 and 7.0/7.1(TESTED)

## Download Link
1. See my project release page

We won't modify SELinux, let your device become more safe.
Also, it is good for you to customize your own rom or even port rom.

## How to install?
See readme in download link.

# Contact
Better contact me by email. Send to james34602@gmail.com

# Terms and Conditions / License
The engine frame is based on Antti S. Lankila's DSPManager

All compatibility supporting by James Fung

Android framework components by Google

Advanced IIR filters library by Vinnie Falco, modify by Bernd Porr

Source code is provided under the [GPL V2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)

### More Credit
DSPFilter.xlsx is a tool for you to desgin IIR Biquad Filter, it is a component from miniDSP.

RBJ_Eq.xls is a RBJ Biquad Equalizer designer. Not very useful and I will not implement it, but could be a reference to designing equalizer.

# Structure map generated by Understand (Hosted on rawgit)
<a><img src="https://rawgit.com/james34602/JamesDSPManager/master/libjamesdsp_StructureMap.svg"/></a>
