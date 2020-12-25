---
---
# Texture Gamma Correction 
The lighting and shading calculations that determine a model's color are performed on the gpu 
using small programs called shaders. Shaders almost exclusively use floating point values because float values can express values much higher than 1.0 and much lower than 0.0 while still maintaining high precision. 

Storing all of the textures used for the shaders with floating point data would require a massive amount of memory, so the floating point values are often encoded using less precise integer formats. JPEGs and PNGs, for example, typically only use 8 bits per channel instead of the 32 bits required to store a floating point value. The integer values are then converted to floating point for use in the shaders.

After the final post processing step, the linear floating point values from the shaders are converted back to 8 bit per channel RGB values in the SRGB colorspace. The SRGB colorspace defines how RGB values map to the colors displayed on the television or other display device. 

## Gamma Encoding/Decoding
Standard 8 bit per channel textures have channel values in the range 0 to 255 where 0 is black and 255 is white. 
The default behavior for textures is to use linear gamma where each grayscale step has a uniform change in brightness between black and white. An integer value of 128 is twice as bright as an integer value of 64. The image below shows a linear gradient with texture values from 0 to 255.

# TODO: Linear Image (use PNG?)

The 8 bits per channel gives 2^8 = 256 total steps from black to white, but most of the steps are used for brighter tones that 
look very similar to one another. Applying a gamma adjustment of 2.2 in an image editor produces a nicer looking gradient, but there are noticeable banding artifacts in the darker tones. 

# TODO: Naive SRGB Gradient (use PNG?)

Applying the gamma adjustment to an 8 bits per channel image reduces the number of distinct grayscale values. 
A gamma adjustment on an 8 bit per channel image can be performed as follows. 
- Convert the integer value to floating point using `floatValue = integerValue / 255.0`
- apply the gamma adjustment using `gammaAdjusted = floatValue ^ gamma`
- convert the float value back to integer using `output = int(gammaAdjusted * 255.0)`
The final step where the value is converted back to integer introduces banding artifacts due to the limited 8 bit precision. 

# TODO: (graphs of naive gamma "fixing")

A better solution is to use the same 8 bits per channel as before but encode the brightness values more efficiently. 
The SRGB colorspace defines a transfer function that is similar but not identical to the gamma adjustment of 2.2 above. More bits are allocated for darker shades than brighter shades to reduce gradient banding and more closely model our nonlinear perception of brightness. Unlike with linear gamma, a value of 128 in the SRGB colorspace is more than 4x as bright as a value of 64. An 8 bit gradient with values from 0 to 255 in SRGB will appear smooth with uniform changes in brightness between steps when viewed on a properly calibrated display. The image below shows an SRGB gradient with values from 0 to 255.
<img src="{{ "/assets/images/gamma/srgb_ramp.png" | relative_url }}" height="auto" width="auto">

## Texture Formats 
The texture's format tells the game how to interpret the texture's data for use in the shaders. The format should match the type of data stored in the texture and it's intended usage. The process of converting the integer values from integer formats to floating point is called *normalization*. 
See the OpenGL wiki's <a href="https://www.khronos.org/opengl/wiki/Normalized_Integer" target="_blank">normalized integer page</a> for technical details. 

# TODO: data doesn't change when saving as the same compression type with unorm vs srgb

### UNorm (Unsigned Normalized)
# TODO: Graph
Textures with unorm formats are converted to floating point by dividing by the max value. 8 bit values are divided by 255, 16 bit values are divided by 16355, etc. This converts unsigned integer values to floating point values in the range 0.0 to 1.0. 
Textures that don't store color data, such as NOR maps and PRM maps, must be saved as UNorm to render correctly in game.

### SNorm (Signed Normalized)
# TODO: Graph
Textures with SNorm formats are converted to floating point values in the range -1.0 to 1.0. These formats aren't as common as UNorm or SRGB. 

### SRGB
# TODO: Graph
Textures with SRGB formats are assumed to contain data in the SRGB colorspace. The texture values are converted to linear floating point values in the range 0.0 to 1.0 using the SRGB transfer function. The conversion from the SRGB texture values directly to floating point doesn't introduce any of the artifacts caused by applying the adjustment manually in an image editor.  
Textures with color data such as col maps and diffuse maps must be saved as SRGB to render correctly in game. The shader values are assumed to use linear gamma, so the final conversion back to SRGB to display the colors on screen will cause color textures saved without an SRGB format to look washed out.