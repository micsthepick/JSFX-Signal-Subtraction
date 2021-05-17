# JSFFTDenoise

A Jesusonic FX based FFT denoiser
can denoise one signal from another, utilizing the FFT to remove all traces of the original signal,
sometimes including encoder artifacts.

## Loading the effect:

### Reaper
Reaper supports JSFX natively, just copy vocalrediso.jsfx to `%AppData%\REAPER\Effects` (In a subfolder if preferred)

### VST compatible DAW (Instructions for windows)
JSFX can usually be run in a vst through [ReaPlugs by Cocos](https://www.reaper.fm/reaplugs/).  
Download and install ReaPlugs, and pay attention to where it installs.  
If you have Reaper installed, ReaPlugs should detect that `%AppData%\REAPER` exists and use that to load JSFX from %AppData%\REAPER\Effects instead of the local copy.
Otherwise, ReaPlugs will load effects from `...\ReaPlugs\JS` at the install location  
(My install is located at `C:\Program Files\VSTPlugins\ReaPlugs\JS`). If you want override the location to store JSFX, you should include a file called reajs.ini in the install folder for ReaPlugs, with the following contents:

    [ReaJS]
    rootpath=\path\to\custom\folder\JS

where \path\to\custom\folder\JS is the path to the JS folder that contains the ColorThemes, Data, Effects and presets folders that you would like ReaJs to use. (For example I run Equalizer APO and when reaper is installed, the audio service tries to load plugins from %AppData%\REAPER\Effects but is denied because of permissions)


## Using the effect
There are two different effects (so far) in this repo, "L-R subtract fft.jsfx" and "L-R subtract fft denoise.jsfx".
The denoise version is based on @Nbickford's REAPERDenoiser, and is very robust to encoding errors and the like,
and is more likely to work in the general case, where as the regular version is based on my own JSVocalRediso,
and will likely sound better when the noise channel you want to get rid of is just about exact in volume and phase througout the entire section where you want to apply the effect, and if this is the case,
you may consider using "both" as the option, otherwise, if the signal to subtract is on the R channel, choose L-R, otherwise R-L.
Adjust noise scale, or strength to control how strongly the signal is subtracted, while keeping the denoising artifacts low.
The resulting two channels will both contain the subtracted signal.
dry-wet mix will let you control how much of the signal is subtracted, so after setting the strength, you can fade between no subtraction and fully subtracted if you like.
Low Cut and High Cut allow you to control what frequency range is outputted in the final result, usually you should leave these to the extremes.
for "L-R subtract fft.jsfx", there are a couple extra sliders. "Attenuate if different volume" probably should be left away from zero, but it can be interesting to fiddle with that slider to get a better subtraction. Phase width controls how out of phase the signal is before it gets attenuated, so for more clean signals, you might get away with smaller values, and you can control how this is distributed along the frequency axis by setting each endpoint, and it will interpolate between those two values.