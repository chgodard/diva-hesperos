---
title : DIVA User Manual
date : 2023-07-12 17:00:00 +0800
tags: [user_manual]
---

    
<div align="justify">

![diva logo black](https://github.com/DecBayComp/VoxelLearning/assets/49953723/20ade68e-e562-471e-98d1-02e43c343741){: width="200px" height="200px" .left .light}
![diva logo white](https://github.com/DecBayComp/VoxelLearning/assets/49953723/e07d2b6e-38af-4a74-b50f-83d58e80bb08){: width="200px" height="200px" .left .dark}
**DIVA** (Data Integration and Visualisation in Augmented and virtual environments) software is a user-friendly platform that generates volumetric reconstructions from raw 3D microscopy image stacks and enables efficient visualization and quantification in VR without pre-treatment. 
 
## **INSTALLATION AND REQUIREMENTS**
---

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
---

### Data requirements
---
The DIVA software can be used with Digital Imaging and COmmunications in Medicine (DICOM) or Tagged Image File Format (TIFF) image files in 8 or 16-bits. Multi-channel files organized using the ImageJ/Fiji convention are supported.
> We recommend limiting the size of loaded files to less than 1 GB. Larger files may be scaled or cropped via [ImageJ/Fiji](https://imagej.net/software/fiji/downloads). 
{: .prompt-warning }

> To improve DIVA performances, use images that are located on your disk.
{: .prompt-tip }

### Data transformation
 ---
As DIVA software supports multi-channel files, overlay different image types can enhance visualization. For example, in a segmentation task, overlaying the raw image (as a gray image) in the first channel and the segmentation in the second channel can facilitate the segmentation evaluation. 

This is the step you can realized in [ImageJ/Fiji](https://imagej.net/software/fiji/downloads):

1. Open the different images by dragging and dropping or with *File/Open*
2. Improve visualisation : go in *Image/Adjust/Brightness* and click on *Auto*.
    > Sometimes you can see a black image for the segmented image, this doesn't mean the image is empty: it's a visualisation issue. Be sure to have selected the segmented image (by clinking on it) otherwise it will apply this effect on the other image image.
    {: .prompt-warning }
3. If the segmented image is not a binary image (i.e. with several labels) and if the labels are incremented by 1 (for example as 0-1-2-3) you have to stretch the histogram of the segmented image between 0 and 255 to facilitate the use of the TF interface in DIVA (the exemple before can became 0-85-170-255). Go in *Process/Enhance Contrast* with the options: 
    - Saturated pixels : 0.00%
    - Normalize : True
    - Equalize histogram : False
    - Process all 256 slices : True
    - Use stack histogram : True
4. Make sure that all images have the same format in 8 or 16bit, if not change it in *Image/Type/*.
    > We recommend to use 8 bits to increase performance.
    {: .prompt-warning }
5. Fuse channels in *Image/Color/Merge Channels...* with the options: 
    - C1(red) : the raw image
    - C2(green) : the segmented image
    - C3(blue) : 
    - C4 (gray) :
    - Create composite : True
        > DIVA only supports 4 channels.
        {: .prompt-warning }
6. Save as TIFF format : *File/Save As/Tiff*


### Importation in DIVA
---
DIVA automatically transform a stack of images as a 3D volume. Importation can then be done in DIVA using the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/79998e80-0de4-406b-a847-421edb5d87c6" width="20px" height="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/8aa81fdd-8fc0-4ff3-b487-e189406842c9" width="20px" height="20px" class="dark"/> button with the *TIFF* or *DICOM* option (in the top-left corner) which opens a file browser or by drag-and-dropping your file direclty. 


![Desktop View](https://github.com/DecBayComp/VoxelLearning/assets/49953723/2273efab-4c21-45d3-83d0-8b48bcae848b){: width="80px" height="80px" .right}
> If you see this type of behavior after loading your image in DIVA, press R in your keyboard to reload the image and correct the rendering artefact. 
{: .prompt-tip }

You can enable or disable each channel independently by right- or left-clicking on the corresponding circle in the top right corner of the interface : <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/5b63bd50-24bb-4719-86da-39771e7d21e2" width="60px" height="60px"/>. You can also use keyboard shortcuts : 1 (to enable/disable channel 1), 2 (to enable/disable channel 2), 3 and 4.


> If the image is loaded with strange scale (possible artifact if there is no information about image size in the metadata), go in the Information panel and finetune the scale for each axis.
{: .prompt-tip }

##  **IMPROVE VISUALIZATION**
---
Voxel color and opacity can be modified in real-time through a user-friendly transfer function interface located in the **Volume** panel under ![channel1](https://github.com/DecBayComp/VoxelLearning/assets/49953723/e6a82720-edf6-4d24-92c0-ab4f316a3d67){:.inline-image width="20px" height="20px" .light} ![channel1](https://github.com/DecBayComp/VoxelLearning/assets/49953723/fdb49542-fb08-431d-885f-a029bf62ebac){:.inline-image width="20px" height="20px" .dark} or ![chanel2](https://github.com/DecBayComp/VoxelLearning/assets/49953723/7f009be9-ad73-43ab-a945-38f1379b8659){:.inline-image width="20px" height="20px" .light} ![chanel2](https://github.com/DecBayComp/VoxelLearning/assets/49953723/c1661a1f-241e-491f-a0e7-9f5de16814ab){:.inline-image width="20px" height="20px" .dark} icon. 
 
<img align="center" src="https://github.com/DecBayComp/VoxelLearning/blob/main/materials/article_gif/VideoS2_DIVA_tagging_lung_image01_TF.gif?raw=true"/>

<!-- <img align="center" src="/assets/video/demo_TF1D.mp4"/> -->

As shown on the video above with a CT-scan of lung tumor, this interface is composed of the image histogram in gray, one white curve for the opacity and one color bar. Each of them are defined with control points which can be adjusted by dragging with the left mouse button (more details on the [DIVA user manual](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf)). The basic principle of the transfer function is that each pixel of the histogram under the curve will be displayed with the corresponding color in the color bar, and each pixel above the curve will be disabled in the 3D and VR view. 
 
For multichannel files, each channel possesses its own transfer function. 

> We recommend you to customize this transfer function to highlight your object of interest and save it as .json file using the **Save** button in order to be able to re-open if necessary.
{: .prompt-tip }


TODO explain les points, how to add point, chage TF type, ...

- dekstop clipper
- TF : 
    - add/remove point click droit
    - change TF type
    - move point : click gauche 
    - lock option for TF
    - same for color
    - opacity 
- act
## **NAVIGATE IN VIRTUAL REALITY**
--- 
Switching to and from the VR mode is performed by clicking on <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/28a179d0-e410-4a72-b7a5-6b0a33f0fd6a" width="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/39e3d2e8-b415-43a4-a3c6-ff459e6af1bf" width="20px" class="dark"/> in the top-left corner and will automatically launch SteamVR to activate the plugged VR headset. 
> This button will not respond if SteamVR is not installed.  
{: .prompt-danger }

<!-- <img align="left" src="/materials/article_gif/VideoS2_DIVA_tagging_lung_image01_TAGS.gif" width="480" height="270"/>  -->

In the VR environment, you can iteract with the volume with the VR controller, see details [here](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf). For the tagging step you have to first activate the **Clipper Tool** to cut in real-time in the volume and then use the **Tagger tool**. Tagging is done with the controller by clicking on the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/1d8f5852-b73f-434d-b7d7-cd10dc924cb7" width="15px" class="dark"/> button and choosing the tag's color (cyan for positive tags and magenta for negative tags). All the tags can be saved as .json file (in order to be re-opened later in DIVA) by clicking on **VR Annotations** in the top-right corner, then on the icon <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/220632b6-990c-41e8-9046-52642ebac901" width="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/2160bf27-b50e-49c3-9d95-065c67cd0315" width="20px" class="dark"/> and on the **Export** button.
   
 
TODOCOMPLETE