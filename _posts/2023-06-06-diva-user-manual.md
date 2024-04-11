---
title : DIVA User Manual
date : 2023-07-12 17:00:00 +0800
tags: [user_manual]
---
    
<div align="justify">

![diva logo black](https://github.com/DecBayComp/VoxelLearning/assets/49953723/20ade68e-e562-471e-98d1-02e43c343741){: width="200px" height="200px" .left .light}
![diva logo white](https://github.com/DecBayComp/VoxelLearning/assets/49953723/e07d2b6e-38af-4a74-b50f-83d58e80bb08){: width="200px" height="200px" .left .dark}
**DIVA**, standing for Data Integration and Visualisation in Augmented and virtual environments, is a user-friendly platform that generates volumetric reconstructions from raw 3D microscopy image stacks, enabling users to efficiently visualise and quantify data in virtual reality (VR) without any pre-treatment. 

DIVA features a dual interface: a desktop mode ideal for displaying data on a standard 2D screen and a VR mode crafted for an immersive visualisation in an artificial environment. The desktop mode focuses on adjusting visualisation settings and providing a preliminary view of the data, whereas the VR mode intensifies focus on data visualisation, user interaction, exploration and analysis.
 
## **INSTALLATION AND REQUIREMENTS**
<hr class="title_style">

DIVA is designed to run on the Windows 10/11 operating system with at least OpenCL 2.0. We recommend using DIVA with the following minimum requirement: 
- Intel i5 processor equivalent or better
- 4GB RAM of memory
- 300 MB of storage
- NVIDIA GeForce 900 Series or better Graphical Processing Unit (GPU). 

DIVA can be used with and/or witout a VR headset and is compatible with HTC Vive, HTC Vive Pro, Oculus Rift, Oculus Rift S, Oculus Quest (with Link Cable) and Windows Mixed Reality headsets. You can find the first version of DIVA, user manual and all the information about the legacy software [here](https://diva.pasteur.fr/). For the updated version of DIVA working with Hesperos go to the corresponding Github repository : [diva-hesperos](https://github.com/DecBayComp/diva-hesperos).

1. For each type of VR headsets you have to download the corresponding installation software (such as [ViveSetup](https://www.vive.com/fr/setup/pc-vr/) or [Oculus](https://www.oculus.com/setup/?locale=fr_FR)).
2. Install [SteamVR](https://www.steamvr.com/fr/), required to use VR functionnalities.
3. Install DIVA : load the [*diva-2.9.13-hesperos* folder from the corresponding Github repository](https://github.com/DecBayComp/diva-hesperos/tree/main/diva-2.9.13-hesperos) and execute DIVA by double-clicking on the provided *diva.exe* file. DIVA will take a moment to load as it allocates memory (roughly 20–30 seconds).
  
> Launch SteamVR (and Oculus app) before the DIVA software if you want to use the VR environment.
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

1. Open images by dragging and dropping or via the *File/Open* option
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
- *`quality`*: quality of the rendered volume.
- *`bricks`*: numbers of volume elements displayed simultaneously.

### 2D tools
<hr class="subtitle_style">
In the **View** panel, users can enable/disable a **Desktop Clipper** tool by right clicking on <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/609c54f0-dcf8-43a5-9bf7-089579e0661c" width="20px" height="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/2e130457-0cb0-4add-b481-d5d6aca4b59d" width="20px" height="20px" class="dark"/>. The tool is visually symbolised by three spherical markers positioned in the two corners of the volume. Shifting one of these markers along any of the three fundamental axes of a cube disables the corresponding section, enhancing the visibility of internal details. 


### The transfer function (TF) interface
<hr class="subtitle_style">

Voxel colour and opacity can be modified in real-time through a user-friendly transfer function (TF) interface located in the **Volume** panel under ![channel1](https://github.com/DecBayComp/VoxelLearning/assets/49953723/e6a82720-edf6-4d24-92c0-ab4f316a3d67){:.inline-image width="20px" height="20px" .light} ![channel1](https://github.com/DecBayComp/VoxelLearning/assets/49953723/fdb49542-fb08-431d-885f-a029bf62ebac){:.inline-image width="20px" height="20px" .dark} or ![chanel2](https://github.com/DecBayComp/VoxelLearning/assets/49953723/7f009be9-ad73-43ab-a945-38f1379b8659){:.inline-image width="20px" height="20px" .light} ![chanel2](https://github.com/DecBayComp/VoxelLearning/assets/49953723/c1661a1f-241e-491f-a0e7-9f5de16814ab){:.inline-image width="20px" height="20px" .dark} icon. For multichannel files, each channel possesses its own transfer function. 

<!-- <img align="center" src="https://github.com/DecBayComp/VoxelLearning/blob/main/materials/article_gif/VideoS2_DIVA_tagging_lung_image01_TF.gif?raw=true"/> -->
<img align="center" src="/assets/videos/DIVA_interface_TF1D_b.gif"/>

As shown on the video above with a CT-scan of lung tumor from [the Medical Segmentation Decathlon challenge’s public dataset](https://www.nature.com/articles/s41467-022-30695-9), the interface comprises :

- an <ins>image histogram</ins> plotted in grey, that illustrates the distribution of pixel intensities across the image, stretching on a log scale from 0(representing black pixels) to 255 (indicating white pixels) on the horizontal axis. The vertical axis quantifies the occurrences of each intensity value.

- a white <ins>absorption curve</ins> on the histogram indicates opacity, revealing pixels below the curve and disabling those above it by setting their absorption to zero. In DIVA, this curve can be formed from spline segments, symmetric Gaussian mixture models (GMM), asymmetric GMM, or a blend of these.
    > The lock option for the absorption curve can help to explore your data by fixing three colour points to one curve points.
    {: .prompt-tip }

- an <ins>emission curve</ins> represented with a horizontal colour bar, , facilitating the colour-coding of specific pixel intensity ranges.

- a <ins>global opacity</ins> index represented with a vertical blue slider, uniformly affecting the opacity of all voxels.

The configuration of absorption and emission curves relies on control points that users can manage by right-clicking to add or delete and left-clicking to drag to a new position (more details on the [DIVA user manual](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf)). For Gaussian curves, the slope at each control point can be fine-tuned by placing the mouse over the point and using the scroll wheel to decrease (scrolling down) or increase (scrolling up) the slope.

Adjusting the transfer function settings enhances the visualisation of certain structures of interest. As illustrated in the video, applying a GMM-based curve makes it easier to isolate structures distinguished by unique pixel intensities. This becomes clear as the curve is shifted from left to right, initially showcasing the lungs and subsequently revealing bones at its rightmost adjustment.
> We recommend you to customise this transfer function to highlight your object of interest and save it as .json file using the **Save** button in order to be able to re-open if necessary.
{: .prompt-tip}


##  **NAVIGATE IN VIRTUAL REALITY**
<hr class="title_style">

Switching to and from the VR mode is performed by clicking on <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/28a179d0-e410-4a72-b7a5-6b0a33f0fd6a" width="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/39e3d2e8-b415-43a4-a3c6-ff459e6af1bf" width="20px" class="dark"/> in the top-left corner and will automatically launch SteamVR to activate the plugged VR headset. 
> This button will not respond if SteamVR is not installed.  
{: .prompt-danger }


Interaction with the volume in the VR environment is facilitated by the VR controller, see details on controller buttons [here](https://diva.pasteur.fr/wp-content/uploads/2019/09/diva-viewer-manual.pdf). To access the **VR Menu**, simply direct the laser pointer from the VR controller towards the volume and click the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/73cf82c3-ad95-45c9-a566-d89d64b6d5eb" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/8eddc41d-4932-442f-bbf1-1402289157a3" width="20px" class="dark"/> button. 
> Note that depending on the VR headset being used, the position of this button will differ.
{: .prompt-warning }

The **VR Menu** offers access to a selection of tools, each symbolised by a unique icon. Selecting a tool involves pointing the laser pointer at its icon and pressing the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/73cf82c3-ad95-45c9-a566-d89d64b6d5eb" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/8eddc41d-4932-442f-bbf1-1402289157a3" width="20px" class="dark"/> button, which will turn the tool icon blue to denote its selection. Closing the **VR Menu** requires pointing the laser into empty space (away from the menu and the volume) and pressing the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/73cf82c3-ad95-45c9-a566-d89d64b6d5eb" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/8eddc41d-4932-442f-bbf1-1402289157a3" width="20px" class="dark"/> button once more.
> If the volume is not visible, a guide arrow points towards the volume. At any moment, the volume will reappear in front of the user by pressing on the spacebar of the keyboard.
{: .prompt-tip}


### Physical manipulation
<hr class="subtitle_style">

The VR controller enables physical interaction within the virtual environment through motion tracking capabilities, supporting movements such as grasping (activated by the trigger button) and rotating in any chosen direction. 

To navigate complex and dense images more easily, users can employ the **VR Clipper** tool by clicking its designated icon <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/a9be1963-7084-4a21-9638-91ad2ec7df88" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/1ed2ba88-e665-4b91-8f80-512df3455896" width="20px" class="dark"/> in the **VR Menu**. Represented by a square attached to the controller, it actively removes a planar fragment from the volume, aligned with the square, exposing deeper image structures. 

The **VR Flashlight** tool, activated via the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/53e8c011-a522-4f28-9d29-8dbb29a26aab" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/b455ddf3-d71d-4006-9a11-6b8ed968d99d" width="20px" class="dark"/> icon in the **VR Menu**, illuminates a chosen spherical section, leaving the rest of the image in shadow, thereby drawing focus to the selected area.


### Quantitative analysis tools
<hr class="subtitle_style">

Basic quantitative analysis is facilitated with counting and distance measurement tools. To access these tools, users click on a submenu located under the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/ae56543e-bcfe-4cad-a588-926f21134f74" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/69b0f7f2-ffbd-41d3-bd25-87b10e075cac" width="20px" class="dark"/> icon within the **VR Menu**.

<img align="center" src="/assets/videos/DIVA_VR_tools.gif"/>

From the **VR Annotations** panel (in the Desktop mode), measurement data, including x, y, z coordinates, pixel-based distances, and additional details, can be exported into a .csv file by using the **Export** button. Via the **Save** button, these results can be saved as .json file in order to be re-opened later in DIVA.
> Additionally, screen and movie capture exports are also available.
{: .prompt-tip}

The **VR Landmark** tool, accessible through the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/c24d6f64-93f1-4c1a-9d2b-22f1cbef950b" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/e5f5a95a-159b-43ea-8418-984f28a04bc5" width="20px" class="dark"/> icon in the **VR Menu**, enables counting by allowing users to add elements with a click on the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/1d8f5852-b73f-434d-b7d7-cd10dc924cb7" width="15px" class="dark"/> button found on the VR controller. This action generates a sphere that may appear in cyan, magenta, yellow, or gray, depending on the colour chosen with the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/9308206e-00b2-4a49-847b-6d99ba6e345d" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/e5a68fc4-ef2f-48e1-bed7-e85a74711760" width="20px" class="dark"/> button on the controller. To delete a counting sphere, position the controller so the sphere turns green, indicating it can be removed by pressing the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/4928762e-5515-42c9-bd9b-d5410ffc1c39" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/4928762e-5515-42c9-bd9b-d5410ffc1c39" width="20px" class="dark"/> button.

Measuring physical distances is facilitated by the **VR Ruler** tool, accessible from the **VR Menu** with the the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/402c08a6-cdb1-4180-a901-c024f8669778" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/0c8e028a-05bc-44da-8369-872e57da04d9" width="20px" class="dark"/> icon. Users begin a measurement by pressing the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/1d8f5852-b73f-434d-b7d7-cd10dc924cb7" width="15px" class="dark"/> button, creating a sphere linked by a white line to where the controller is located. Adding additional segments to the measurement is as simple as pressing the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/1d8f5852-b73f-434d-b7d7-cd10dc924cb7" width="15px" class="dark"/> button again, and this can be done multiple times to create a series of connected segments. If a mistake is made, pressing the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/ac6d908d-0eb6-4367-94d9-4165712f81d9" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/901ca3a7-5544-492f-b644-ce04a57b88d3" width="20px" class="dark"/> button will undo the last segment. Completing the measurement process requires pressing the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/73cfd126-de3e-45df-9567-c21909151697" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/73cfd126-de3e-45df-9567-c21909151697" width="20px" class="dark"/> button, and measurements can be entirely removed by using the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/4928762e-5515-42c9-bd9b-d5410ffc1c39" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/4928762e-5515-42c9-bd9b-d5410ffc1c39" width="20px" class="dark"/> button found on the controller's widget.


### Other tools
<hr class="subtitle_style">

Additional VR functionalities can be accessed through a submenu found beneath the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/93ba7823-3f89-4422-bd8d-a87675d07f13" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/67630e01-801b-4895-8968-aa77f7a242b1" width="20px" class="dark"/> icon in the **VR Menu**. For tagging purposes, the **VR Tagging tool** can be activated by selecting the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/220632b6-990c-41e8-9046-52642ebac901" width="20px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/2160bf27-b50e-49c3-9d95-065c67cd0315" width="20px" class="dark"/> icon. Users can create tags by pressing the <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/35c93203-6e80-4a4e-849f-370bf26ba56d" width="15px" class="light"/> <img src="https://github.com/DecBayComp/VoxelLearning/assets/49953723/1d8f5852-b73f-434d-b7d7-cd10dc924cb7" width="15px" class="dark"/> button on the controller and then choosing between four colours with the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/9308206e-00b2-4a49-847b-6d99ba6e345d" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/e5a68fc4-ef2f-48e1-bed7-e85a74711760" width="20px" class="dark"/> button. Each tag can be deleted by using the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/4928762e-5515-42c9-bd9b-d5410ffc1c39" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/4928762e-5515-42c9-bd9b-d5410ffc1c39" width="20px" class="dark"/> button. Furthermore, the size of the virtual brush used for tagging can be adjusted by clicking on the <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/cd33bf56-dd25-4298-a347-e4cb8c605e38" width="20px" class="light"/> <img src="https://github.com/DecBayComp/diva-hesperos/assets/49953723/a7988b1e-b540-43f2-83b4-c3fb02d48857" width="20px" class="dark"/> button. There are four sizes available, organised in ascending order, and each click on the button cycles through these sizes sequentially.

<img align="center" src="/assets/videos/DIVA_tagging.gif"/>


##  **DIVA AND LEARNING**
<hr class="title_style">

We have developed a new variant of DIVA, aiming to enhance voxel learning by combining virtual reality with an easy annotation system, straightforward classifier learning, and robust cloud-based computation. For further details, please visit our [GitHub repository VoxelLearning](https://github.com/DecBayComp/VoxelLearning) to access a dedicated user manual.

<img align="center" src="/assets/videos/DIVA_Cloud_VoxelLearning_pipeline.gif"/>


##  **DIVA AND POINT CLOUD**
<hr class="title_style">

Localising molecules in large images can generate a huge amounts of data to process. Analysing these point clouds and trajectories to detect localisation errors can therefore be very time consuming. This is what motivated the combination of two platforms: DIVA and [Genuage](https://www.nature.com/articles/s41592-020-0946-1), in order to visualise raw image in virtual reality, overlayed with the trajectory data, thus allowing users to explore and check the validity of multidimensional point cloud data. For more information, our [GitHub repository diva-genuage](https://github.com/DecBayComp/diva-genuage) contains a specific user manual.


<img align="center" src="/assets/videos/DIVA_Genuage_VR_interface.gif"/>


## **LICENSE**
<hr class="title_style">

**DIVA** is a free but not open source software.