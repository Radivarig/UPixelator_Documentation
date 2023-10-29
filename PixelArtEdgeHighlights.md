# UPixelator - Pixel Art Edge Highlights

Thank you for purchasing Pixel Art Edge Highlights! ❤️  
If you like the asset I would appreciate your review!  

## Contact
If you have any questions or feedback, please contact me at reslav.hollos@gmail.com.  
You can also join the [Discord server](https://discord.gg/uFEDDpS8ad)  

## Quick start
- Drag and drop `Prefabs/PixelArtEdgeHighlights` into scene.  
- Or open the scene under the `Example/Scenes` folder.
- Otherwise go to the [Setup](#setup) section of this readme.  

## Description
Pixel Art Edge Highlights is a post process effect that draws thin edges based on the depth and normal textures screen output.

It is intended to be used with the [Unity Pixelator](https://assetstore.unity.com/packages/slug/243562) asset that pixelates whole 3d scenes in realtime and handles camera movement smoothing and pixel creep reduction.

(You can also use it as a standalone effect to add detail on the edges that would otherwise be indistinguishable like flat colors where normals are equal, see screenshots with the effect off).

## Edge Types
- `Convex Highlights` lightens outward edges
- `Outline Shadow` darkens objects outline
- `Concave Shadow` darkens inward edges

## Supported Pipelines
- Built-in ✓
- URP ✓

## Tested builds
- Unity 2021.3 (Builtin, URP 12): Windows, WebGL  
- Unity 2022.3 (Builtin, URP 14): Windows, WebGL  

## Please note
- This asset automatically sets some camera and render pipeline settings, if you're worried please backup your work.

# Setup
- Scene:
  - Drag the `PixelArtEdgeHighlights` prefab into scene and should immediatelly see the effect
  - Drag the `PixelArtEdgeHighlights - Canvas` prefab into scene to get the runtime UI controls
- Camera:
  - If you're using scene pixelation set `Projection: Orthographic`
  - Have the camera distanced about 10 meters from the target (internal shader values for depth map are adjusted for it)
- Game window
  - Change `Free Aspect` to a fixed resolution eg. `1920x1080`
  - Aspect ratio of width to height should not be close to or over `2:1`
  - Set `Scale: 1` to have pixels render 1 on 1

## Demo scene
- Demo scene is located under the `Example` folder

## Recommended usage
- Lower values from `0.2` to `0.5` are suggested to get nice colored edges just enough to make the highlights differentiate geometry.

## Excluding objects from the effect
The effect is set to execute before transparents, to exclude an object set its render queue to 3000+.
If an opaque material becomes transparent it could mean it is not outputing alpha values correctly.
To change that you can hardcode the alpha value to 1 (eg. `return float4(some_output.rgb, 1);`).

- [Shader Graph] `Advanced Options > Queue Control: UserOverride` then `Render Queue` will appear
- [Builtin: Standard] Set Rendering Mode to `Fade` (otherwise you wont be able to set the queue higher)
- [URP: Lit] `Surface Type: Transparent`
- [Custom] If there isn't a `Render Queue` visible try setting it through inspector Debug (triple dots right of the inspector lock icon)

## In progress/research
- [URP] Exclude cameras with ignore flag from renderer feature effect

## Known Issues
- If the effect is missing after build has finished, please try to enter and exit play mode
- [Unity 2022; URP] There are two obsolete warnings, I will address them when I find replacement code that works
- If you delete the folder, import again and get `Shader not found`, re-enable the `PixelArtEdgeHighlight.cs` script
- [URP] If you get `No Universal Render Pipeline is currently active` please check references under `Project Settings > Quality`
  - This can happen is you deleted some pipeline asset files under the `Settings` folder
