---
title : DIVA User Manual
date : 2023-07-12 17:00:00 +0800
tags: [user_manual]
---

    
<div align="justify">

![diva logo black](https://github.com/DecBayComp/VoxelLearning/assets/49953723/20ade68e-e562-471e-98d1-02e43c343741){: width="200px" height="200px" .left .light}
![diva logo white](https://github.com/DecBayComp/VoxelLearning/assets/49953723/e07d2b6e-38af-4a74-b50f-83d58e80bb08){: width="200px" height="200px" .left .dark}
**DIVA** (Data Integration and Visualisation in Augmented and virtual environments) software is a user-friendly platform that generates volumetric reconstructions from raw 3D microscopy image stacks and enables efficient visualisation and quantification in VR without pre-treatment. 

DIVA is composed of a dual interface, featuring a desktop mode suitable for visualising data on a conventional 2D computer screen and a VR mode designed for immersive visualisation in an artificial environment. The desktop mode is designed for setting optimal visualisation parameters and initial visual of the data, while the VR mode is dedicated to data visualisation, interaction, navigation and analysis.
 
## **INSTALLATION AND REQUIREMENTS**
<hr class="title_style">

DIVA is designed to run on the Windows 10/11 operating system with at least OpenCL 2.0. We recommend using DIVA with the following minimum requirement: 
- Intel i5 processor equivalent or better
- 4GB RAM of memory
- 300 MB of storage
- NVIDIA GeForce 900 Series or better Graphical Processing Unit (GPU). 

DIVA can be used with and/or witout a VR headset and is compatible with HTC Vive, HTC Vive Pro, Oculus Rift, Oculus Rift S, Oculus Quest (with Link Cable) and Windows Mixed Reality headsets. You can find the first version of DIVA, user manual and all the information about the legacy software [here](https://diva.pasteur.fr/). For the updated version of DIVA go to the corresponding Github repository : [diva-hesperos](https://github.com/DecBayComp/diva-hesperos).

1. For each type of VR headsets you have to download the corresponding installation software (such as [ViveSetup](https://www.vive.com/fr/setup/pc-vr/) or [Oculus](https://www.oculus.com/setup/?locale=fr_FR)).
2. Install [SteamVR](https://www.steamvr.com/fr/), required to use VR functionnalities.
3. Install DIVA : load the [*diva-2.9.13-hesperos* folder from the corresponding Github repository](https://github.com/DecBayComp/diva-hesperos/tree/main/diva-2.9.13-hesperos) and execute DIVA by double-clicking on the provided *diva.exe* file. DIVA will take a moment to load as it allocates memory (roughly 20–30 seconds).
  
> Launch SteamVR before the DIVA software if you want to use the VR environment.
  {: .prompt-warning }


## **IMPORT YOUR IMAGE**
<hr class="title_style">

### Data requirements
<hr class="subtitle_style">
The DIVA software can be used with Digital Imaging and COmmunications in Medicine (DICOM) or Tagged Image File Format (TIFF) image files in 8 or 16-bits. Multi-channel files organised using the ImageJ/Fiji convention are supported.
> We recommend limiting the size of loaded files to less than 1 GB. Larger files may be scaled or cropped via [ImageJ/Fiji](https://imagej.net/software/fiji/downloads). 
{: .prompt-warning }

> To improve DIVA performances, use images that are located on your disk.
{: .prompt-tip }

### Data transformation
<hr class="subtitle_style">

As DIVA software supports multi-channel files, overlay different image types can enhance visualisation. For example, in a segmentation task, overlaying the raw image (as a grey image) in the first channel and the segmentation in the second channel can facilitate the segmentation evaluation. 

This is the step you can realised in [ImageJ/Fiji](https://imagej.net/software/fiji/downloads):

1. Open the different images by dragging and dropping or with *File/Open*
2. Improve visualisation : go in *Image/Adjust/Brightness* and click on *Auto*.
    > Sometimes you can see a black image for the segmented image, this doesn't mean the image is empty: it's a visualisation issue. Be sure to have selected the segmented image (by clicking on it) otherwise it will apply this effect on the other image.
    {: .prompt-warning }
3. If the segmented image is not a binary image (i.e. with several labels) and if the labels are incremented by 1 (for example as 0-1-2-3) you have to stretch the histogram of the segmented image between 0 and 255 to facilitate the use of the TF interface in DIVA (the exemple before can became 0-85-170-255). Go in *Process/Enhance Contrast* with the options: 
    - Saturated pixels : 0.00%
    - Normalise : True
    - Equalise histogram : False
    - Process all 256 slices : True
    - Use stack histogram : True
4. Make sure that all images have the same format in 8 or 16bit, if not change it in *Image/Type/*.
    > We recommend to use 8 bits to increase performance.
    {: .prompt-warning }
5. Fuse channels in *Image/Color/Merge Channels...* with the options: 
    - C1(red) : the raw image
    - C2(green) : the segmented image
    - C3(blue) : 
    - C4 (grey) :
    - Create composite : True
        > DIVA only supports 4 channels.
        {: .prompt-warning }
6. Save as TIFF format : *File/Save As/Tiff*


### Importation in DIVA
<hr class="subtitle_style">
Once a stack of 2D images is loaded, DIVA generates a 3D reconstruction using the volume ray-casting technique. Importation can be done using the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/79998e80-0de4-406b-a847-421edb5d87c6" width="20px" height="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/8aa81fdd-8fc0-4ff3-b487-e189406842c9" width="20px" height="20px" class="dark"/> button with the *TIFF* or *DICOM* option (in the top-left corner) which opens a file browser or by drag-and-dropping your file direclty. 


![Desktop View](https://github.com/DecBayComp/VoxelLearning/assets/49953723/2273efab-4c21-45d3-83d0-8b48bcae848b){: width="80px" height="80px" .right}
> If you see this type of behavior after loading your image in DIVA, press R in your keyboard to reload the image and correct the rendering artefact. 
{: .prompt-tip }

You can enable or disable each channel independently by right- or left-clicking on the corresponding circle in the top right corner of the interface : <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/5b63bd50-24bb-4719-86da-39771e7d21e2" width="60px" height="60px"/>. You can also use keyboard shortcuts : 1 (to enable/disable channel 1), 2 (to enable/disable channel 2), 3 and 4.


> If the image is loaded with strange scale (possible artefact if there is no information about image size in the metadata), go in the Information panel and finetune the scale for each axis.
{: .prompt-tip }

##  **IMPROVE VISUALISATION**
<hr class="title_style">

Upon loading, a menu in blue appears in the top right corner and is attached to the loaded volume, with volume information accesible in the  **Information** panel under the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/df440c3e-aeb4-44bd-88d3-fee0aa6e0174" width="20px" height="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/7c966a23-9074-4785-ad53-4f7729cb5ea2" width="20px" height="20px" class="dark"/> button.

### Basic visualisation settings
<hr class="subtitle_style">
In the **Information** panel, parameters interface can be access via the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/023cc05e-1cbb-40ec-8bfd-f63d12bab7f6" width="20px" height="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/c21ad1f1-5ec1-4d07-bc1e-c11f92da0dae" width="20px" height="20px" class="dark"/> button. It includes basic visualisation settings such as:
- *`x`*, *`y`*, *`z`*: voxel unit size in each dimension.
- *`scale`*: global isotropic scaling of the volume.
- *`brightness`*: ambient lighting coefficient which is an offset globally applied to all pixel intensity values.
- *`diffuse`*: diffuse lighting coefficient, taking into account directional light to create shading effects from top to bottom in DIVA.
- *`quality`*: TODO.
- *`bricks`*: TODO.

### 2D tools
<hr class="subtitle_style">
In the **View** panel, users can enable/disable a **Desktop Clipper** tool by right clicking on <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/609c54f0-dcf8-43a5-9bf7-089579e0661c" width="20px" height="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/2e130457-0cb0-4add-b481-d5d6aca4b59d" width="20px" height="20px" class="dark"/>. The tool is visually symbolised by three spherical markers positioned in the two corners of the volume. Shifting one of these markers along any of the three fundamental axes of a cube disables the corresponding section, enhancing the visibility of internal details. 


### The transfer function interface
<hr class="subtitle_style">

Voxel colour and opacity can be modified in real-time through a user-friendly transfer function (TF) interface located in the **Volume** panel under ![channel1](https://github.com/DecBayComp/VoxelLearning/assets/49953723/e6a82720-edf6-4d24-92c0-ab4f316a3d67){:.inline-image width="20px" height="20px" .light} ![channel1](https://github.com/DecBayComp/VoxelLearning/assets/49953723/fdb49542-fb08-431d-885f-a029bf62ebac){:.inline-image width="20px" height="20px" .dark} or ![chanel2](https://github.com/DecBayComp/VoxelLearning/assets/49953723/7f009be9-ad73-43ab-a945-38f1379b8659){:.inline-image width="20px" height="20px" .light} ![chanel2](https://github.com/DecBayComp/VoxelLearning/assets/49953723/c1661a1f-241e-491f-a0e7-9f5de16814ab){:.inline-image width="20px" height="20px" .dark} icon. For multichannel files, each channel possesses its own transfer function. 

<!-- <img align="center" src="https://github.com/DecBayComp/VoxelLearning/blob/main/materials/article_gif/VideoS2_DIVA_tagging_lung_image01_TF.gif?raw=true"/> -->
<!-- <img align="center" src="/assets/video/demo_TF1D.mp4"/> -->
<img align="center" src="/assets/videos/DIVA_interface_TF1D.gif"/>

As shown on the video above with a CT-scan of lung tumor from [the Medical Segmentation Decathlon challenge’s public dataset](https://www.nature.com/articles/s41467-022-30695-9), the interface comprises :

- an <ins>image histogram</ins> plotted in grey. The image histogram represents the pixel intensity distribution of the image, always
log-scaled and normalised from 0 to 255 (from left to right in the horizontal axis), where 0 corresponds to the dark pixel and 255 to the white pixel. The vertical axis corresponds to the number of occurrences of each pixel intensity.

- an <ins>absorption curve</ins> plotted in white on the histogram. The absorption curve defines the opacity. Each pixel under the absorption curve is displayed, while each pixel above the absorption curve is disabled (i.e. with an absorption value of zero). DIVA allows the curve to be constituted of spline segments or a combination of symmetric or asymmetric Gaussian mixture models (GMM).
    > The lock option for the absorption curve can help to explore your data by fixing three colour points to one curve points.
    {: .prompt-tip }

- an <ins>emission curve</ins>  represented with a horizontal colour bar. This allows users to apply a specific colour to a specific pixel intensity range.

- a <ins>global opacity</ins>  index represented with a vertical blue slide bar, applied uniformly to all voxels.

Absorption and emission curves are defined with control points which can be created or deleted by right cliking, moved by dragging with the left mouse button (more details on the [DIVA user manual](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf)). For curve as Gaussian the slope of each control point can be independently adjusted by positionning the mouse on the point and scrolling down to decrease and up to increase.

Transfer function setting allow to hightligh structures of interest. As shown in the video, a curve based on GMM simplifies isolating a structure in the image with distinct pixel intensities. as we can see in the video when moving the curve from left to right  with curve at left displaying lung and cruve at right displaying bones.
 
> We recommend you to customise this transfer function to highlight your object of interest and save it as .json file using the **Save** button in order to be able to re-open if necessary.
{: .prompt-tip}


##  **NAVIGATE IN VIRTUAL REALITY**
<hr class="title_style">

Switching to and from the VR mode is performed by clicking on <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/28a179d0-e410-4a72-b7a5-6b0a33f0fd6a" width="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/39e3d2e8-b415-43a4-a3c6-ff459e6af1bf" width="20px" class="dark"/> in the top-left corner and will automatically launch SteamVR to activate the plugged VR headset. 
> This button will not respond if SteamVR is not installed.  
{: .prompt-danger }

In the VR environment, you can interact with the volume with the VR controller, see details [here](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf). The VR menu is accessed by pointing the VR controller at the loaded volume with the laser
pointer and pressing the Menu Button . Note that depending on the VR headset being used, the position of the Menu Button will differ.


HOW TO open menu 




> If the volume is not visible, a guide arrow points towards the volume. At any moment, the volume will reappear in front of the user by pressing on the spacebar of the keyboard.
{: .prompt-tip}


### Physical manipulation
<hr class="subtitle_style">
Physical manipulation is achieved through the VR controller, which relies on motion tracking, including actions such as grasping, by pressing on the trigger button, and turning in any direction and position.

Users can activate the **VR Clipper** tool, by clicking on the ICON button in the VR menu, to ease the navigation in complex and dense images. The tool is symbolised by a square attached to the controller. It operates dynamically by removing a planar portion,corresponding to the square, from the rendered volume, allowing deep structures in the image to be revealed. 

The **VR Flashlight** tool, activated via the ICON button in the VR menu, highlights a user-defined spherical region while dimming the surrounding image.


### Quantitative analysis tools
<hr class="subtitle_style">

Basic quantitative analysis is facilitated with tagging, counting, and distance measurement tools. Each tools posees its own specialised widget displayed on the VR controller.

Counting is done with the **VR Landmark** tool, activated via the ICON button in the VR menu. Adding a element by clicking on the ICON PLUs will create a sphere that can be cyan, magenta, yellow or gray according to the color select by ICON ?. To remove a counter sphere, place the controller in front of the sphere until it changes color to green. At this point, the counter sphere can be deleted by pressing the Delete Button ( icon).

Physical distance measurement is done with the **VR Ruler** tool, activated via the ICON button in the VR Menu. To start a measurement segment, users press the ICON PLUS, creatibg a sphere anb a white line that connect the sphere to the controller porsition. To connect a segment, simply press the Connect Button again. Multiple segments can be connected in this way. To undo a previously made segment, press the Undo Button ( icon). A measurement is finished by pressing the Finish Button ( icon). Measurement segments can additionally be entirely deleted by pressing the Cancel Button (
icon) that appears on the controller widget, shown below.

Tagging is done with the controller by clicking on the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/1d8f5852-b73f-434d-b7d7-cd10dc924cb7" width="15px" class="dark"/> button and choosing the tag's colour (cyan for positive tags and magenta for negative tags).
 
 
 
Each measurement result can be exported to a .csv file in the **VR Annotations** panel with the **Export** button, including data such as x, y, z coordinates, distances in pixels, and additional details. Via the **Save** button, these results can be saved as .json file in order to be re-opened later in DIVA.

 
 
 icon <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/220632b6-990c-41e8-9046-52642ebac901" width="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/2160bf27-b50e-49c3-9d95-065c67cd0315" width="20px" class="dark"/> 


Additionally, screen and movie capture exports are also available.