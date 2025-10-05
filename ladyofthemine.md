---
layout: default
title: Martin Nyman
---

<link rel="stylesheet" href="/assets/css/custom.css">

# Lady of the Mine 

<iframe width="560" height="315" src="https://www.youtube.com/embed/73YuYuVfbac?si=DSVQUG7Dir8qkI36" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Lady of the Mine is a exploration game heavily inspired by the survival horror game Amnesia. The player is stuck in a cave-in and need to escape by navigating through maze like tunnels while also staying in the light. If the player runs out of sanity they will become mad and forever be lost in the mine. The Lady of the Mine gives players useful hints on how to navigate the treacherous tunnels and possibly escape with their life intact.
For this project we work with our own Game Engine called Arinn Engine. My responsibilities include photogrammetry, vfx, tools and shaders. The work on this project is still ongoing and a gameplay trailer is expected to be launched here soon.

# Photogrammetry

I chose to do a bread scan for this project, i really like how much detail and variation this type of object has in its shape and texture. The photos where taken on a turntable at 3 different angles and lengths for a total of 54 pictures for the top part and about 20 pictures for the bottom part. for the lighting we used a simple 3 point light setup. Although the scan ended up pretty good i wish i had taken more photos for a more pain free experience, unfortunately there was some issues with time constraints & lack of memory in the SD card.

Once i had the photos for the bread i filtered and added the images to lightroom to tweak the raw images, especially shadows and exposure needed a tweak here.
Next, the images where processed where i generated masks for the object and then proceeded with the mesh generation in Substance 3D Sampler. I tried using reality capture but unfortunatley had trouble matching the images there, more images would probably have helped in this case, especially since the bread was quite hard to set matching control points for with it's highly varyiable texture.

When the mesh and textures was done i put the bottom and top part together, an issue with the bottom scan was the lack of images for the scan so i had to get creative here. I managed to merge the 2 parts together in Houdini and bake them to one mesh. The issue was now that their textures where not matching too well in terms of color and normal strength with some artifacts.
I took the baked version into Substance painter and cleaned up the artifacts using the stamp tool, brushwork and some overlay colors.

# VFX

In the project i also created some VFX with Embergen to make flipbooks, which was probably the easiest way to implement VFX in our quite limited game engine. I also made some simple default particles such as embers & rain.

# Tool

In this project the programmers changed how the level loading is done and how we handle rotations, since our levels are loaded from JSON files with a certain format we now had to convert the old levels to a brand new format.
To avoid loss of our previous levels i created a tool that reads the old JSON and converts it to the new format.

# Shader

I created a depth shader that fades with a stack of different noise texture, it also fades out with a gradient based on the Y position in the UV map. The shader was created using Emil Lehtola's custom made HLSL node graph tool.
It was quite challenging working with a node tool that has less features then what i am used to working with (Unity/Unreal). This forced me to think more about how the underlying logic works for each node. I also had to be quite creative to recreate missing functions, however, I was actually quite surprised with what you can create even with just the basic nodes. 
With that said it was very fun to work with this tool and see how our collaboration with feedback and development could improve the tool further.