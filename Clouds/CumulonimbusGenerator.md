# Cumulonimbus Generator
![](https://raw.githubusercontent.com/srwxr-xr-x/EnvironmentArtHDAs/refs/heads/main/Clouds/Clouds.jpg)
## Introduction
### Mission
- Photorealistic Clouds, mimicking that of real world examples of the specified cloud, in this case, *Cumulonimbus capillatus*. 
- Easy to manipulate to give varieties of results quickly. *Control is key*
- **Simplicity**, users should be able to use this tool without having to read the basics of how it works!

### Overview
This HDA is a simple demonstration that gives powerful results. Utilizing Houdini's built in cloud system, to take 3 components, the base of the Cumulonimbus *(hereafter referred to as CN)*, the mid of the CN Anvil, and the top, anvil like surface. The scientific reasons as to why these are formed, through wind shear and their massive scale is fascinating, but will not be addressed here. 
Splitting a CN cloud into these three components gives us massive levels of control over the end product with quite minimal setup. The first draft published herein is lacking many features *(notably the ability to smooth the underside of the "anvil")*, yet still produces incredibly realistic results.
## *Configuration*
As of now, there are three sections to the HDA; Each one representative of the 3 main segments. By default, all options are set for a simple CN cloud.
The first, *Base Settings*, controls the "*feet*" of the anvil. 
"*Billowy Factor*" is a pseudonym for the Point Separation parameter when creating the cloud shapes. It controls how tightly clumped or loose the initial shape for the base will be. Larger values create a larger, smoother, less chaotic shape, whilst smaller values will create smaller, more chaotic shapes.
"*Scale*" is a control of the *Initial Size* parameter, its the scale of the shape.
"*Base Width"* controls the X width of the spawning area for the cloud, its the X constraint for initial generation size.
Similarly, "*Base Length*" is the same as *Base Width* for the Z direction.

Most settings in the other 2 segments are the same, with some notable differences.
in **Mid Settings**, the *Base Width/Length* parameters are replaced with the *Length* parameter, since the mid segment is vertical, this is just the Z direction length.
in **Top Settings**, the *Top Cutoff* and *Top Wisp Thickness* control 2 things, first; the height to cut off the top of the CN cloud to form the "anvil head" of the cloud, and second; the thickness of the wispy segment that fades the top anvil head at the harsh edges.

These settings *(so far)* will allow you to make an infinite number of CN clouds! Please submit a bug report or pull request if you have additions!
