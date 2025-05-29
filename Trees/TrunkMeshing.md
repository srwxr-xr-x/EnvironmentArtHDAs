# Trunk Mesher
![](https://raw.githubusercontent.com/srwxr-xr-x/EnvironmentArtHDAs/refs/heads/main/Trees/Trees.png)
## Introduction
### Mission
- Realistic Root and Trunk meshing, according to simple rules derived in the node. 
- Easy to manipulate to give varieties of results quickly. *Control is key*
- *Ease of Use!* Users should be able to get a variety of results quickly and easily.

### Overview
This HDA is a easy to use skeleton or L-System meshing algorithm to create realistic trunk's and roots to trees. Best paired with a tool like [Natsura](https://natsura.com/) to create the beginning skeleton to mesh, which is what was used to create the base skeletons for the example imagery here.
This node has quite a few main steps that are taken "under the hood";

First, a simple `width` attribute is created if it does not exist. This is simply a normalized attribute for each branch root to tip, typically starting small and ending smaller.
This `width` is used as the baseline for detangling the branches if they overlap, `width` typically needs to be set manually by the user based on use case. with [Natsura](https://natsura.com), you are given a width attribute that you control with its base meshing, but with L-Systems and skeletons that will default to base logic, which can and will change from each usecase, remap it to find the best settings!

After detangling, the algorithm adds noise to a resampled skeleton and lerps it back into the original mesh. Continues to find a new normalized distance from root to tip for each branch, tetrahedrizes and runs multiple `Find Shortest Path` and resamples without upsampling to get normalized distance, and adds these veiny "Find Shortest Path" results to the base mesh.

Finally, a low and high frequency noise is lerp'd to the final mesh and polyreduced by 66%. These give the best control in my experience.
The result is a quite realistic wood trunk texture that can vary greatly based on the inputs and skeleton. This can then be run through a `Mask by AO` and `Mask by Feature` node to extract details for texturing!

## *Configuration*
As of now, there are two sections to the HDA; Splitting between main trunk controls, and the noise controls for each step.

The first, *Trunk Controls*, controls the base trunk thickness and result. 
"*Final Polyreduce Percentage*" controls the Polyreduce "keep" percent, this means a value of 33 will reduce the mesh to 33% of its original polygon count.
"*Trunk Vein Root Bias*" is possibly one of the most important controls, this parameter tweaks the amount of veins that will appear on the surface of the trunk, essentially higher values == more points for `Find Shortest Path` to run on. This is a very artistic control based on tree species
"*Visualization Mode*" is a drop down menu to change the output to a specific stage of algorithm. This helps visualize the thickness, noise, and skeleton.
Now comes the 3 sections within the *Trunk Controls*. The first of which is the *Detangle Controls*. Rather than explain every single control here, and in each other section, I will just reference the Houdini Manual, since these are just mapped straight from them.
"*Detangle Controls*" maps the [Detangle](https://www.sidefx.com/docs/houdini/nodes/sop/detangle.html) node, with "Thickness Bias" being a weight of the `width` attribute which is used to detangle. Higher thickness bias equals a higher impact on detangling.
"*Trunk Thickness Controls*" maps the [Attribute Remap](https://www.sidefx.com/docs/houdini/nodes/sop/attribremap.html) that is used to remap the normalized distance from each root to tip into a usable thickness value. Maximum and Minimum root thickness are the root thickness at the beginning of the root and tip of the root, with the ramp controlling that falloff.
"*Vein Thickness Controls*" does the same thing but for each individual vein, post-"Find Shortest Path". 

In the other tab, *Noise Controls*, controls are solely focused on adding mountain noise and fractal noise to hide smoothing.
"*Skeleton Noise*" contains another Lerp min/max value, and its curve. The noise for this is very simple, and typically does not need to be modified other than these controls. If the user must modify it, it is contained within the "NoiseTree" `Attribute Noise` node.
"*Base Trunk Noise*" contains parameters mapped from the base trunk `Attribute Noise` node. These are just post-processing steps to add noise before converting and combining the veins with the main mesh.
"*Final Noise*" controls final low and high frequency post-processing noise, this is just for artistic controls.

