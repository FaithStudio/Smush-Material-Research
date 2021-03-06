# Stage Lighting Material Parameter Descriptions
The stage light nuanmb files use the same material parameter names as model materials. The parameters are not the same, however.

## Float Vector 4
| Name | Description |
| --- | --- |
| CustomVector0 | RGB color multiplier for lights. Multiplied by CustomFloat0. |
| CustomVector1 | Distance fog color. Used with CustomVector13. RGB = color, A = *unused* |
| CustomVector2 | RGB? Affects the color of the sun on zelda_tower. RGB values can be negative. |
| CustomVector3 | XYZW? Values are usually 0 to 1. Values can be negative. |
| CustomVector4 | Mixes the final color with the blend color. RGB = blend color, A = blend factor. |
| CustomVector5 | Specular cube map color multiplier (Texture7). |
| CustomVector6 | RGB = shadow color, A = ??? |
| CustomVector7 | RGB? RGB values are 0 to 6. |
| CustomVector8 | Rim lighting color. RGB = color, A = blend amount |
| CustomVector9 | RGB? |
| CustomVector10 | XYZW? Related to fog. X is very small. YZ appear to be angle values. W is always 1. |
| CustomVector11 | XYZW? Related to fog. Z is very large. |
| CustomVector12 | XYZW? XY are very large. ZW are small. XY can be negative. |
| CustomVector13 | Controls distance fog blending along with CustomVector1. XYW appear are distance values. X = ???, Y = ???, Z = intensity, W = ??? |
| CustomVector14 | XYZW? Always set to (1, 1, 0, 0). |
| CustomVector15 | Similar to CustomVector5. RGB = specular cube map color multiplier, A = ??? |
| CustomVector16 | XYZW? Similar values to CustomVector18. |
| CustomVector17 | XYZW? XYZ are 0 to 1. W is always 0. |
| CustomVector18 | XYZW? XY can be negative. Z is always 0. |
| CustomVector27 | ??? Always set to (1, 0, 0, 0). |

# Float
| Name | Description |
| --- | --- |
| CustomFloat0 | Direct lighting strength. Multiplied by CustomVector0. |
| CustomFloat1 | Affects the intensity of the sun on zelda_tower. Values are 0 to 1. |
| CustomFloat2 | ??? Values are always 0. |
| CustomFloat3 | ??? Values are always 2. |
| CustomFloat4 | ??? Values are always 8. |
| CustomFloat5 | ??? Values are always 0.2. |
| CustomFloat6 | ??? Values are always 50000. |
| CustomFloat7 | ??? Values are always 0. |
| CustomFloat8 | ??? Values are always 1000. |
| CustomFloat9 | ??? Values are always 1. |
| CustomFloat10 | ??? Values are always 0.2. |
| CustomFloat11 | ??? Values are always 1. |
| CustomFloat12 | ??? Values are always 0.  |
| CustomFloat13 | ??? Values are always 0. |
| CustomFloat14 | ??? Values are always 1. |
| CustomFloat15 | ??? Values are always 1. |
| CustomFloat16 | ??? Values are always 1. |
| CustomFloat17 | ??? Values are always 0. |
| CustomFloat18 | ??? Values are always 100000. |
| CustomFloat19 | ??? Values are always 1. |

# Boolean Flags
| Name | Description |
| --- | --- |
| CustomBoolean0 | Affects sunshaft points. |
| CustomBoolean1 | Affects lights. |
