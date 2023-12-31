# DuckStation Android Post-Processing Shaders Guide

![My Image](example.jpg)
> Example of Final Fantasy IX with crt-lottes shader

> [!IMPORTANT]
> **WITH THE RELEASE OF BETA V0.1-6039, STENZEK ADDED OFFICIAL SUPPORT FOR POSTPROCESSING SHADERS.**
>
> **THERE'S NO NEED OF THIS GUIDE ANYMORE.**
>
> **THANK YOU STENZEK!**

This is a guide to get post-processing shaders working on the Android version of DuckStation. 

Stenzek ported this feature on the Android version, but didn't implemented it (yet) in the settings GUI for some reason. 

You can still enable them by adding some lines of text in per-game settings .ini files. 

# What you need?

1. Latest beta version (v0.1-5997 as of writing) from the [official website](https://www.duckstation.org/android/).

2. A file manager with text editor that can access Android/data folder (e.g. [X-plore](https://play.google.com/store/apps/details?id=com.lonelycatgames.Xplore&hl=it&gl=US))

# Guide

1. Open DuckStation, long tap a game and select **Game Properties**, take note of the **Serial** in **Summary** tab.
   
2. Change any settings and go back to save (Doing this will create the game .ini file).
   
3. Open your file manager and navigate to: **Android/data/com.github.stenzek.duckstation/files/gamesettings** (Here you will find your per-game settings files).
   
4. Identify your game using the **Serial** number in Step 1, open and edit the **.ini** file with text editor and paste these lines:

> [PostProcessing] <br>StageCount = 1 <br>Enabled = true
>
>[PostProcessing/Stage1]

5. Select the desired shader in the following list and paste it under **[PostProcessing/Stage1]**, save and close.

> [!NOTE]
> **Some shaders only work with Vulkan renderer!**
>
> **Others, like crt-lottes, are CPU intensive, so you'll need a good device!**

# Shaders List

ShaderName = Cccalibrator

ShaderName = crt-lottes

ShaderName = dolphinfx/bloom

ShaderName = dolphinfx/celshading

ShaderName = dolphinfx/scanlines

ShaderName = simple-brightness

ShaderName = simple-flip

ShaderName = simple-gamma

ShaderName = simple-sharpen

ShaderName = Daltonize

ShaderName = Deband

ShaderName = LUT

# Chain Multiple Shaders

To chain multiple shaders increase **StageCount** number and create additional **[PostProcessing/Stage#]** lines with relative increasing number. Paste a different shader under each **[PostProcessing/Stage#]**.

Example:

> [PostProcessing] <br>StageCount = 3 <br>Enabled = true
> 
> [PostProcessing/Stage1] <br>ShaderName = dolphinfx/scanlines
> 
>[PostProcessing/Stage2] <br>ShaderName = simple-brightness
>
> [PostProcessing/Stage3] <br>ShaderName = simple-flip

# Shaders Advanced Configuration

Use this shader list instead if you want to customize them. Each shader has it's own editable parameters, there's a comment under each setting with relative minimum/maximum range. (You'll also find the list in [this](shaders_list_advanced.txt) text file for easiest copy/paste)

Example of celshading shader with thicker edges:

> [PostProcessing] <br>StageCount = 1 <br>Enabled = true
>
>[PostProcessing/Stage1] <br>ShaderName = dolphinfx/celshading <br>A_EDGE_STRENGTH=1 <br>B_EDGE_FILTER=0.6 <br>C_EDGE_THICKNESS=1.75 <br>D_PALETTE_TYPE=1 <br>E_YUV_LUMA=0 <br>G_COLOR_ROUNDING=1

### CCCalibrator
   
ShaderName = Cccalibrator

LUMINANCE = 1.2
> #Luminance(Y) Range: 0.0 to 3

ORANGECYAN = 1.2
> #Orange-Cyan(I) Range: 0.0 to 3

MAGENTAGREEN = 1.2
> #Magenta-Green(Q) Range: 0.0 to 3

BLACK = 10
> #Black Range: 0 to 255

WHITE = 240
> #White Range: o to 255

NOISE = 10
> #Noise Range: 0 to 50

SATURATION = 50
> #Saturation Range: 0 to 100

### CRT-Lottes

ShaderName = crt-lottes

hardScan = -8
> #Scanline Weight Range: -20 to 0

hardPix = -3
> #Scanline Scale Range: -20 to 0

warpX = 0.031
> #Screen Warp X Range: 0.000 to 0.125

warpY = 0.041
> #Screen Warp Y Range: 0.000 to 0.125

maskDark = 0.5
> #Mask Dark Range: 0.0 to 2

maskLight = 1.5
> #Mask Light Range: 0.0 to 2

shadowMask = 3
> #Shadow Mask Type Range: 0 to 4

brightBoost = 1
> #Brightness Boost Range: 0.0 to 2

hardBloomPix = -1.5
> #Bloom Soft X Range: -2.0 to -0.5

hardBloomScan = -2
> #Bloom Soft Y Range: -4.0 to -1

bloomAmount = 0.15
> #Bloom Amount Range: 0.0 to 1

shape = 2
> #Filter Kernel Shape Range: 1.0 to 10

scaleInLinearGamma = true
> #Scale in Linear Gamma Range: true or false

### Bloom

ShaderName = dolphinfx/bloom

A_BLOOM_TYPE = 0
> #Bloom Type Range: 0 to 5

B_BLOOM_STRENGTH = 0.22
> #Bloom Strength Range: 0.000 to 1

C_BLEND_STRENGTH = 1
> #Blend Strength Range: 0.00 to 1.2

D_B_DEFOCUS = 2
> #Bloom Defocus Range: 1.0 to 4

D_BLOOM_WIDTH = 3.2
> #Bloom Width Range: 1.0 to 8

E_BLOOM_REDS = 0.02
> #Bloom Reds Range: 0.000 to 0.5

F_BLOOM_GREENS = 0.01
> #Bloom Greens Range: 0.000 to 0.5

G_BLOOM_BLUES = 0.01
> #Bloom Blues Range: 0.000 to 0.5

### Cel Shading

ShaderName = dolphinfx/celshading

A_EDGE_STRENGTH = 1.1
> #Edge Strength Range: 0.00 to 4

B_EDGE_FILTER = 0.6
> #Edge Filter Range: 0.25 to 1

C_EDGE_THICKNESS = 1
> #Edge Thickness Range: 0.25 to 2

D_PALETTE_TYPE = 1
> #Palette Type Range: 0 to 2

E_YUV_LUMA = 0
> #Use Yuv Luma Range: 0 or 1

G_COLOR_ROUNDING = 1
> #Colour Rounding Range: 0 or 1

### Scanlines

ShaderName = dolphinfx/scanlines

A_SCANLINE_TYPE = 0
> #Scanline Type Range: 0 to 2

B_SCANLINE_INTENSITY = 0.18
> #Scanline Intensity Range: 0.15 to 0.3

B_SCANLINE_THICKNESS = 0.5
> #Scanline Thickness Range: 0.2 to 0.8

B_SCANLINE_BRIGHTNESS = 1.1
> #Scanline Brightness Range: 0.50 to 2

B_SCANLINE_SPACING = 0.25
> #Scanline Spacing Range: 0.1 to 0.99

### Simple Brightness

ShaderName = simple-brightness

BRIGHTNESS_SCALE = 1
> #Brightnss Scale Range: 0.1 to 5

### Simple Flip

ShaderName = simple-flip

G_FLIP_HORZ = 1
> #Flip Horizontally Range: 0 or 1

G_FLIP_VERT = 0
> #Flip Vertically Range: 0 or 1

### Simple Gamma

ShaderName = simple-gamma

GAMMA_IN = 2.2
> #Gamma In Range: 0.1 to 10

GAMMA_OUT = 2.2
> #Gamma Out Range: 0.1 to 10

### ReShade Deband

ShaderName = Deband

enable_weber = true
> #Weber Ratio Range: true or false

enable_sdeviation = true
> #Standard Deviation Range: true or false

enable_depthbuffer = false
> #Depth Detection Range: true or false

t1 = 0.007
> #Standrd Deviation Threshold Range:

t2 = 0.04
> #Weber Ratio Threshold Range: 0.000 to 0.5

banding_depth = 1
> #Banding Depth Range: 0.00 to 2

range = 24
> #Radius Range: 0.000 to 1

iterations = 1
> #Iterations Range: 1 to 4

### ReShade LUT

ShaderName = LUT

fLUT_AmountChroma = 1
> #LUT Chroma Amount Range: 0.00 to 1

fLUT_AmountLuma = 1
> #LUT Lum Amount Range: 0.00 to 1

# Special Thanks 
Stenzek and every DuckStation contributors
