# FlatColorCellShader

A minimal cell shader for textureless flat colors.

![](https://github.com/ZhengYiHu/FlatColorCellShader/blob/main/Media/CellShadeDemo.png)
## Usage
Simply download `FlatColor.shadergraph` and `ShadeColor.shadersubgraph` and create a material for `FlatColor` to apply to the objects.
>Note that the shaders are made with `Shader Graph` so the package needs to be installed and `URP` be the rendering pipeline.

## Implementation
1. Compare the normal angle with the Light source's angle from `_WorldSpaceLightPos0` to determine how much light the surface is receiving using Dot Product. 
![](https://github.com/ZhengYiHu/FlatColorCellShader/blob/main/Media/DotProduct.png)
And Remap the values from [-1 , 1] to [0, 1].

2.  Use a step function to separate the two sides based on a threshold and render the lit part with the Main Color and the shadow part with the Shade Color 
![](https://github.com/ZhengYiHu/FlatColorCellShader/blob/main/Media/CellShading.png)

3. Add the results together and multiply the main light's color in the final render's color output.
Main light can be obtained with the variable `_LightColor0`
![](https://github.com/ZhengYiHu/FlatColorCellShader/blob/main/Media/LightColor.png)

Note: `_WorldSpaceLightPos0` and `_LightColor0` are Unity [Built-In Shader variables](https://docs.unity3d.com/Manual/SL-UnityShaderVariables.html)


## Shadow Color

In order to generate automatically a Shade color from the main color, I added a small way to tweak the HSV values to get one procedurally.

![](https://github.com/ZhengYiHu/FlatColorCellShader/blob/main/Media/ShadowColor.png)
Since shade colors usually work better with some Hue shift and Saturation/Value change instead of just reducing the brightness of the Main Color, or having to pick a Shade color manually for each newly created material.

![](https://github.com/ZhengYiHu/FlatColorCellShader/blob/main/Media/ShadowColorDemo.gif)
