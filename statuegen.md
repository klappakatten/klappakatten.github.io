---
layout: default
title: Martin Nyman
---

<link rel="stylesheet" href="/assets/css/custom.css">

# Statue Generator

<img src="/assets/images/statuetool.png" class="btn-icon">

In this project, I developed a tool over the course of three weeks (part-time) that allows users to first input their own rigged characters and then generate statue-like outputs with predefined poses and materials. 
The tool enables users to easily add surface detail and introduce visual variation to the model. 
Additionally, users have the option to generate procedural platforms to accompany their statues, offering further customization and creative control.

### 1. Input custom character

The user can input any rigged character, and it will work out of the box as long as the correct naming conventions are followed.​​​​​​​

### 2. Choose pose
The user can easily retarget their rigged character to one of the preset poses by selecting from the available options in the pose list.​​​​​​​

### 3. Choose material
The user can choose from a list of preset materials.​​​​​​​

### 4. Add edge highlights
The user can add a highlight to the edges based on the model's curvature to make the edges more defined.

### 5. Add surface noise
Noise can be added to create a more defined shape that better fits the desired statue style.​​​​​​​
# How it works

First, the rigged model and materials are automatically added to the UI using Python code. When additional materials and pose options are added to the system, they will appear in their corresponding lists for the user.
Next, when the user inputs their rigged model into the system, Python code automatically scans the entire rig and attempts to match its bones to the internal rig. This is done by setting values on the Houdini Map Points node based on commonly used bone names such as "head," "spine," "hand," and so on. While this automated matching works well in most cases, inconsistencies in naming may lead to occasional mismatches. If that happens, the user can manually adjust the bone mappings to correct any issues.

Then, the rig is retargeted using basic nodes within Houdini. This process works well even with models of varying scale and proportions, thanks to the Compute Offset options.
Since the rig doesn't need to be animated, there's no need to focus on tasks like smoothing out animations or preventing jitter, as would typically be required for animated characters.

Next, we handle exceptions for meshes that consist of many separate pieces or lack sufficient thickness. In the following step, when converting the model to a VDB, we aim for a fully closed surface. We may also choose to smooth out areas of the mesh with low curvature to avoid overly sharp lines that can occur when the geometry is sparse.​​​​​​​

Next, the model is converted to a VDB. This step fuses intersecting parts of the mesh, resulting in a unified and visually interesting look for the statue. The idea behind this is inspired by how real-life statues are often carved from a single block of stone or cast as one piece of metal, making it difficult to include intricate, non-intersecting parts. For example, a statue holding a sword would typically be sculpted as a single, continuous piece rather than as separate components.
The user also has the option to add a custom shape that subtracts part of the mesh using a VDB Combine node. This allows for creative variation in the overall silhouette of the model.
After that, noise is added. Here, the user can choose the type of noise and how strongly it should affect the shape of the mesh. This effect is achieved by applying 3D turbulent noise to subtract density from the VDB, giving the surface a more organic and stylized appearance.

The next step is to apply materials along with some color variation driven by curvature and ambient occlusion.
Finally, we generate a low-poly version using the QuadRemesher, unwrap the UVs, and bake the details from the high-poly model generated from the VDB process.
With that, the mesh is complete!

Lastly, I added options for generating a procedural platform. Nothing too complex, just some basic shapes copied in an array, combined using VDB operations, with texture options like curvature and ambient occlusion.
I also included a caching option to ensure this part of the tool doesn’t slow down the main workflow.

# Reflection

This tool sounded a lot more promising in concept than it turned out to be in practice. In hindsight, its use case feels quite limited. That said, it was still a valuable learning experience, and I believe it has potential, especially if it is reworked or taken in a new direction. For instance, the retargeting part of the code could be highly useful for a range of future applications.
Also while I did not spend much time on the procedural platform feature, it probably should have been scrapped altogether. It would have been more worthwhile to focus on refining the retargeting system and improving the overall look and feel of the statue itself.

## Materials & Poses

The poses displayed in this project come from mixamo.com. The material options are made by Quixel Megascans at Fab with some default houdini ones sprinkled in there aswell.