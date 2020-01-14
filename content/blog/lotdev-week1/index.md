+++
title = "Landscape of Thorns Devblog: Week 1"
date = 2020-01-12

[taxonomies]
blog-tags = ["desert of thorns", "game development", "unity", "graphics programming"]
+++

# Landscape of Thorns Devblog: Week 1

It occured to me that now that I'm developing a game for real, I should start blogging my weekly progress. I'm calling this project Desert of Thorns for the moment, though the name is likely temporary. The short version is that it's a mix of walking simulator, survival game, horror game, and art game inspired by [this 1993 report](https://prod-ng.sandia.gov/techlib-noauth/access-control.cgi/1992/921382.pdf) on how to deter human entry to the [Waste Isolation Pilot Plant](https://www.wipp.energy.gov/), a nuclear waste storage facility in the New Mexico desert, for the next 10,000 years. A more detailed writeup on the design is forthcoming.<!-- more -->

## First stab at the game's aesthetic

Aesthetics are important, so my first step was to cook up a simple dithering post-processing shader in Unity and a simple scene to test it on. The shader just compares each screen pixel's luminance to the coressponding pixel of a tileable noise texture, turning pixels darker than the noise black, and brighter white. I experimented with a few different noise textures, including perlin noise, blue noise, blurred blue noise, and solid gray.

I quickly discarded the perlin noise, since it wasn't well suited to producing shades or sharp areas of dark and light. The unblurred blue noise preserved shades well, but was rather destructive to textures, while the blurred noise and gray had the opposite problem, preserving textures but reducing shades to (near-)pure black or white. This was a problem: near the player, textures are essential for making the world visually interesting, while in the distance mipmapping takes over and shade becomes much more important. Here's a comparison of the two kinds of dithering, to illustrate.  

{{captioned_image(image="unblurred_noise_example.png", caption="Unblurred noise")}}

{{captioned_image(image="blurred_noise_example.png", caption="Blurred noise")}}

## Implementing depth-sensitive dithering

My first attempt at a solution was to do some sort of dynamic blurring based on the depth buffer. But, computing a gaussian blur at every pixel is expensive, especially when the blur radius and kernel size can vary. I tried to be clever and use trilinear interpolation with [Kaiser-sampled](https://en.wikipedia.org/wiki/Kaiser_window) mipmaps of the dither texture to mimic the dynamic blur, but after spending a while making this work, the result was unacceptably ugly. The power-of-two scaling was apparent in how the pattern changed with depth, and the lower-resolution mips were completely unsuitable for dithering due to their low frequency. 

I declared that attempt a failure, and moved on to a new, markedly simpler solution. Linearly interpolate between unblurred and blurred noise based on the depth buffer. This was simple to implement and easy to tweak the parameters for. I think the results look pretty good, though there's certainly still room for improvement.

{{captioned_image(image="interpolated_noise_example.png", caption="Interpolated noise")}}

The texture of the ground is still apparent, but the sky isn't a harsh (not to mention visually confusing) black and white. I may tweak the interpolation curve in the future, but I think this basic technique is the best solution.

## Trying to stabilize the dither
After that I thought about trying to stabilize the dither, which as a screen-space effect is not pinned to the scene's geometry. In order to do so, I turned to [this excellent post on the topic](https://forums.tigsource.com/index.php?topic=40832.msg1363742#msg1363742) written by [Lucas Pope](https://dukope.com/), which documents a number of techniques for dither stabilization. Judging that what he calls "Screen-mapping with Offset" would fit my intended artstyle best, I set about implementing it.

Due to my relative inexperience with Unity and its... sparse documentation, it took about six hours of work to figure out the necessary incantations, but in the end I was able to get the effect working. Uuuunfortunately, it was extremely disorienting. I suspect this was because of the higher resolution of my scene, as well as its much greater range of depth than Lucas'. The latter factor is particularly bad for this effect, since the fact that the dither texture moves by the same amount at each pixel, regardless of distance, makes it *more* obvious that the effect is in screen-space, not less. So, in the end I stuck with the existing dithering algorithm.

The stabilization attempt wasn't a total loss though, since I figured out how to peform some tricky shader calculations in Unity, the code for which I will reproduce here. Be warned that I am using the new [High-Definition Render Pipeline](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@4.6/manual/index.html), so I cannot guarantee these samples will work correctly in any other pipeline configuration.

```hlsl
// Returns a unit vector representing the world-space facing direction of the camera.
// HDRP uses camera-relative rendering, so it is not necessary to subtract the camera's position.
// If using another rendering pipeline, subtract _WorldSpaceCameraPos.
float3 GetCameraViewDirection() {
	return normalize(mul(UNITY_MATRIX_I_V, float4(0.0, 0.0, 1.0, 1.0)).xyz);
}

/// Returns the rotation of the camera in the xz (yaw), yz (pitch), and xy (roll) planes in radians.
float3 GetCameraRotation() {
	float3 viewDir = GetCameraViewDirection();
	return atan2(-viewDir.zzx, -viewDir.xyy) + PI.xxx;
}

/// Returns the horizontal and vertical FOV of the camera in radians.
float2 GetCameraFOV() {
	return atan2(-_ScreenSize.xy, -UNITY_MATRIX_P._m11.xx) + PI.xx;
}
```

## End of Week 1

With a good-enough aesthetic, I'm now shifting my focus to the game's terrain generation, and starting by researching the terrain and ecology of the real world areas the setting is based on (chiefly the Chihuahuan Desert in New Mexico). If I do return to the dither, it will likely be to add some kind of selective local contrast (sharpening) effect, to further show the texture of materials. Until next time!
