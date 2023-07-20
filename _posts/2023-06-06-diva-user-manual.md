---
title : DIVA User Manual
date : 2023-07-12 17:00:00 +0800
tags: [user_manual]
---

    
<!-- <div align="justify"> -->

<img align="left" src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/20ade68e-e562-471e-98d1-02e43c343741" width="200px"/>

 **DIVA** (Data Integration and Visualisation in Augmented and virtual environments) software is a user-friendly platform that generates volumetric reconstructions from raw 3D microscopy image stacks and enables efficient visualization and quantification in VR without pre-treatment. 

 LIEN GITHUB ?? 
 
## **Installation and Requirements**
---

DIVA is designed to run on the Windows 10 operating system with at least OpenCL 2.0. We recommend using DIVA with an Intel i5 processor equivalent or better, at least 4GB RAM of memory, 300 MB of storage and a NVIDIA GeForce 900 Series or better Graphical Processing Unit (GPU). DIVA can be used with and witout VR headset and is compatible with HTC Vive, HTC Vive Pro, Oculus Rift, Oculus Rift S, Oculus Quest (with Link Cable) and Windows Mixed Reality headsets. You can find DIVA user manual and all the information about the legacy software [here](https://diva.pasteur.fr/). 

1. For each type of VR headsets you have to download the corresponding installation software (such as [ViveSetup](https://www.vive.com/fr/setup/pc-vr/) or [Oculus](https://www.oculus.com/setup/?locale=fr_FR)).
2. Install [SteamVR](https://www.steamvr.com/fr/) required to use VR functions.
3. Install DIVA : load the [*diva_TOCOMPLETE* folder](/diva_voxel_learning) and execute DIVA by double-clicking on the provided *diva.exe* file. DIVA will take a moment to load as it allocates memory (roughly 20–30 seconds).
  
> Launch SteamVR before DIVA software if you want to use VR environment
  {: .prompt-warning }


 
## **Import your image**

### Data requirements
---
The DIVA software can be used with Digital Imaging and COmmunications in Medicine (DICOM) or Tagged Image File Format (TIFF) image files in 8 or 16-bits. Multichannel files organized using the ImageJ/Fiji convention are supported.
> We recommend limiting the size of loaded files to less than 1 GB. Larger files may be scaled or cropped via [ImageJ/Fiji](https://imagej.net/software/fiji/downloads) for example. 
{: .prompt-warning }

> To improve DIVA performances, use images that are located on your disk.
{: .prompt-tip }

### Tips for data transformations
 ---
TODO IN DETAILS

 1) Open the DICOM image via *Plugins/bio-Fromats/Bio-Formats* Importer with options :
    - View stack with : Hyperstack
    - Group files with similar names : ON
    - Open all series : ON
    - All other options are OFF
2) Improve visualization with *Image/Adjust/Brightness* => Click on **Auto**
3) Make sure that the format is 8 or 16bit, if not change it in *Image/Type/* 
4) Save as TIFF format : *File/Save As/Tiff*

### Importation in DIVA
---
Importation can then be done in DIVA using the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/79998e80-0de4-406b-a847-421edb5d87c6" width="20px"/> button with the *TIFF* option (in the top-left corner) which opens a file browser or by drag-and-dropping your TIFF file direclty. 
 
<img align="left" src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/2273efab-4c21-45d3-83d0-8b48bcae848b" width="80px"/> 

> If you see this type of behavior after loading your image in DIVA, press R in your keyboard to reload the image and correct the rendering artefact.
{: .prompt-warning }
  
##  **Improve visualization**
---

Voxel color and opacity can be modified in real-time through a user-friendly transfer function interface located in the **Volume** panel under <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/e6a82720-edf6-4d24-92c0-ab4f316a3d67" width="20px"/> or <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/7f009be9-ad73-43ab-a945-38f1379b8659" width="20px"/> icon. 
 
 <!-- <img align="left" src="/materials/article_gif/VideoS2_DIVA_tagging_lung_image01_TF.gif" width="480" height="270"/> -->
 
As shown on the video above with a CT-scan of lung tumor, this interface is composed of the image histogram in gray, one white curve for the opacity and one color bar. Each of them are defined with control points which can be adjusted by dragging with the left mouse button (more details on the [DIVA user manual](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf)). The basic principle of the transfer function is that each pixel of the histogram under the curve will be displayed with the corresponding color in the color bar, and each pixel above the curve will be disabled in the 3D and VR view. 
 
For multichannel files, each channel possesses its own transfer function which can be activated by left clicking on the corresponding channel icon in the **Volume** panel. 

> We recommend you to customize this transfer function to highlight your object of interest and save it as .json file using the **Save** button in order to be able to re-open if necessary.
{: .prompt-tip }
  
 
## **Navigate in Virtual Reality**
--- 
Switching to and from the VR mode is performed by clicking on <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/28a179d0-e410-4a72-b7a5-6b0a33f0fd6a" width="20px"/> in the top-left corner and will automatically launch SteamVR to activate the plugged VR headset. 
> This button will not respond if SteamVR is not installed.  
{: .prompt-danger }

<!-- <img align="left" src="/materials/article_gif/VideoS2_DIVA_tagging_lung_image01_TAGS.gif" width="480" height="270"/>  -->

In the VR environment, you can iteract with the volume with the VR controller, see details [here](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf). For the tagging step you have to first activate the **Clipper Tool** to cut in real-time in the volume and then use the **Tagger tool**. Tagging is done with the controller by clicking on the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px"/> button and choosing the tag's color (cyan for positive tags and magenta for negative tags). All the tags can be saved as .json file (in order to be re-opened later in DIVA) by clicking on **VR Annotations** in the top-right corner, then on the icon <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/220632b6-990c-41e8-9046-52642ebac901" width="20px"/> and on the **Export** button.
   
 
   
  
# Example
You will find in [here](/materials/data_examples/) different applications of **Voxel Learning** on CT scans, MRI and microscopy images. Raw data in TIFF format is available with an adapted transfer function to ensure correct visualization, as well as an expert segmentation of the tumor. Tagging file in the format JSON can be loaded to see which tags were used to train the different models. We propose in the folder all the different learners available (for more details see the [folder_structure file](/folder_structure.md)).
 
 <!-- </div> -->
