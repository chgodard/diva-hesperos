---
title : Quantitative Analysis
date : 2024-10-23 17:00:00 +0800
tags: []
---

<div align="justify">

As part of the analyses for this project, we evaluated the progress of one of our models (which will be discussed in a future article) during an iterative process, leveraging Hesperos for interface corrections. Additionally, we internally conducted evaluations to determine the fundamental ability of \Gls{VR}, with DIVA, to rapidly correct segmentation.

## **Evaluation for 2D correction and iterative training**
<hr class="title_style">

Our objective here is to determine how effective our iterative training process is in situations where annotated datasets are absent. To achieve this, we used high-resolution episcopic microscopy images of a 9.5-week mouse embryo, focusing on segmenting the inferior atrio-ventricular canal and left atrium (AVC + LA), the notochord, the outflow tract (OFT), the right ventricle (RV), the left ventricle (LV), and the right atrium (RA).

Initially, experts manually annotate selected slices from 18 different volumes, producing 473 annotated 2D images in Hesperos. These images are used to train a self-supervised leanring (SSL) model with a dataset consisting of 72 large volumes. Following this, a U-Net model is trained using the 473 2D slices. The results presented in the foloowing Figure, including the Dice similarity coefficient (DSC) in a) and the 95th Hausdorff distance (HD) in b) for each label, are illustrated in blue in the following Figure for this first evaluation.
In the iterative steps, the U-Net is applied to every 2D slice within the 18 volumes, after which experts use Hesperos to make corrections, increasing the annotated dataset to 3 844 slices. The performance metrics for this second iteration of the U-Net are displayed in orange in the Figure. The pre-existing segmentation from the U-Net facilitates the overall annotation process.

<img src="https://github.com/user-attachments/assets/562f8b10-de3e-47d6-ac7d-74f17c1ee320" width="1000px"/>

After the second iteration, we see significant improvements in our metrics, confirming the enhanced robustness of our network through iterative training. The DSC score remains low for the notochord, a small and thin label, due to slight misalignment in our segmentation. Although minor in a high-resolution context, this misalignment significantly affects the DSC, which is not ideal for small elements. Thus, we use the 95th percentile Hausdorff distance, better suited for small labels, showing much improved performance in the second iteration.


## **Evaluation of VR correction**
<hr class="title_style">

For a preliminary test, we selected ten volumes from the FeTA 2022 challenge to run with one of our models (2D U-Nets, each trained on a specific axis), which were not used during training. We display the raw and segmented results in DIVA. Corrections are made using the VR Tagging tool in DIVA, focusing on deletion or addition of voxels in three labels—grey matter, white matter, and ventricles—known for their ease of manual correction by non-experts. We display the resulting mean Dice similarity coefficients (DSC) for each label in the following box_plots, with each 2D U-Net model represented on a separate axis.

<img src="https://github.com/user-attachments/assets/a42fd356-aa66-44d9-833f-db0a25d10c44" width="1000px"/>


Although VR may not be optimal for detailed corrections, it has proven to be rapid and effective in correcting segmentations within seconds. This demonstrates VR's capacity to swiftly identify and remove significant outliers, which is essential for the ongoing iterative learning and correction cycle.