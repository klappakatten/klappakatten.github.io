---
layout: default
title: Martin Nyman
---

<link rel="stylesheet" href="/assets/css/custom.css">

# Level  Generator

<iframe width="560" height="315" src="https://www.youtube.com/embed/uTRFTNt6nAU?si=5plU20Lz-LNgwfaD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

In this project, I developed a tool that generates corridors and rooms based on text input from the user.
The goal was to reduce development time for level designers by minimizing the need for manual asset placement.
The tool can be used to generate complete levels, corridors, or to create quick but not dirty prototypes.
I used PySide2 to build the custom UI as a shelf tool in Houdini but i plan to implement this fully as a custom node in the future.
The tool was developed over the course of 4 weeks. Feel free to check out the code section of the project at GitHub

# The code

The process begins by receiving input from the user through a standard text area. This input is then converted into a two-dimensional list of characters.
Next, the list is looped through to create a node for each character, assigning it a coordinate (x, y). A character check is performed to determine the type of input, which is later used to decide which modules to place.
After all nodes are created, the list is looped through again to identify connected nodes by examining the adjacent positions: above, below, left, and right of each node. If any neighbouring nodes are found, they are added to the current node neighbour list.
With all connection data available, a depth-first recursive search is performed to explore every possible path. This is used to apply logic such as setting the height of nodes following a stair module or assigning normal directions to ensure proper orientation of doors and stairs.
Finally, points are created in Houdini, each containing relevant attributes such as position, type, wall direction, and point normal direction.

# The nodes

The first step here is to take the generated points and create new points for the walls. Since the wall direction is already known, it's easy to determine placement and assign the correct normal direction to each wall. Additional points are also created for the roof, which are simply offset duplicates of the floor modules. In hindsight, this logic should probably have been handled in the coding section to keep all point-related operations centralized, making future adjustments simpler and more organized.
By using bounding boxes for the modular meshes, placement and scaling can be accurately controlled to ensure proper integration within the level. A manual scaling option with position offset controls will likely be added in the future, as non-standard shapes may introduce potential issues.

Another feature intended for this tool was the ability to place objects along the wall. This was relatively straightforward to implement, as the wall positions were already available. Objects could simply be placed at those positions with a new Y-offset as the starting point. Groups were then created for each type of point, which served as the basis for copying the appropriate modules to their corresponding locations.

Since I wanted the user to be able to add a variety of mesh types for each category, I added some Python code to load multiple meshes from the UI and assigned an item type variable to each one using a for loop. I could then import the relevant points, assign them a random module type attribute based on the total number of available types, and copy the modules with a randomized attribute value to the corresponding point.
I applied this method to each type of module, as their placement varies depending on their relation to the bounding box. Otherwise, I would have used a more generalized approach to avoid repeating code and nodes. That said, this is something I’d like to refactor into its own subnetwork with user-configurable placement options in the future.

Finally, there were many small issues that had to be addressed. Unfortunately, I won’t be able to go into detail within this limited format, but some of the issues that needed fixing included:
Exception handling for adding additional floors with modules such as doors and stairs. For example, there must always be a wall above every door, rather than another door.
If the height of a stair module did not match the full height of a standard module, it had to be offset to align properly with neighbouring modules. This was resolved by checking for uneven height values and shifting the stairs by the missing amount.
Walls had to be placed to fill any gaps that could occur when there was an uneven height level.

# Reflection

Going into this project, I felt quite confident and had a clear idea of how the project and code would be structured. This was mainly because I had done similar work before involving multi-directional graphs and recursive searching, particularly in the context of studying computer science at Stockholm University. However, it turned out that the complexity increased significantly as more variables were introduced such as module directions, height, module dimensions, module variety, levels, and so on.
I managed to solve many of these issues, but the challenges became especially apparent when addressing them using Houdini nodes. These problems ideally should have been handled in the code itself, as the logic is now split between the nodes and the code, which can lead to inconsistency and confusion.
I’m looking forward to revisiting the project in the future to refactor and expand on the functions. One feature I am particularly excited to add is a bias attribute for asset placement, I think it could be a really cool addition.
If you have any questions about the project or suggestions on how I can improve it further, feel free to reach out.