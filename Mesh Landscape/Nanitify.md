# Nanitify
## Introduction
### Mission
- Split huge objects that would previously run Unreal Engine out of memory whilst importing, or slow it to a halt, into bite sized objects.
- Handle Materials correctly, UV mapping according to its position relative to the center position
- Easily control Unreal mesh building settings from houdini.

### Overview
This HDA is a simple adaptation from the Project Pegasus cliff tiling example. This HDA as of now takes a grid, resizes it to the size of the object, and uses its square's centers to cut an object into many smaller objects and with Houdini Engine, load them one by one.
With Nanite in Unreal Engine 5, we can use incredibly high definition assets, but run into an issue of memory. Unreal Engine's importing uses an exponential amount of memory per the complexity of the object being imported. This asset, with the use of a TOPs network, solves that issue. Development is in progress to increase speed, both on the Houdini side, and the unreal side, but this is a solid solution.
## *Configuration*
As of now, there are three sections to the HDA; Each one representative of the 3 main settings. By default, all options are set as a simple explanation of what they should point to.
Starting off, in the *Grid Settings* tab, you can control the size of the cutting grid, more cells = more import operations, and more objects in the hierarchy, but less memory used per each import, the more is better when loading and importing, but the tradeoff is time, seconds lost when loading the game, and large assets can take lots of unnecessary memory. Currently this is the only option in this tab, but further ideas include expanding into the YZ direction for cutting to handle more complex objects.
In the Debug tab, right now we only have one option, to color the different segments. This just visualizes the different cuts that will be done by showing unique segments that will be cut. Relatively straightforward, this tab will be expanded more in the future as well.
In the Unreal Settings tab, there are 3 different tabs for controlling different aspects of the mesh import routine.
First, in the *Base Settings* tab, you can control the name that will be given to the asset when importing, and in the hierarchy.
The Material Path setting controls a unreal engine path attribute to a material to apply to the object when importing. 
Similarly, the *Level Path* option controls the world hierarchy to load the assets into on import.
The Nanite Settings tab just controls and mirrors some Unreal Engine settings for Building meshes, these can be read about here: [Houdini to Unreal](https://www.sidefx.com/docs/houdini/unreal/attributes.html#houdinitounreal)
Finally, the Mesh Settings tab controls miscellaneous mesh settings, currently just lightmap resolution.
