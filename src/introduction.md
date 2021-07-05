## Introduction to Minervas

Minervas is a scene cognitive training dataset solution for the interior scene agent industry. Users can use Minervas to generate large-scale low-cost scene recognition data sets based on Coohom's massive scene sets.

The core workflow of Minervas includes the following parts:

* `Scene Processor`: In this stage, user can filter and re-arrange the layout of 3D scene
* `Entity Processor`: User can modify scene content such as Light, Mesh, Material, as well as the camera. We also support to export the customized scene related structure information as JSON output
<!-- * `Render Processor`: Based on the processed 3D scene, use render engine to generate RGB and auxiliary channel images such as Depth, Normal, Semantic etc -->
* `Pixel Processor`: In this stage, user can add image processing algorithm to the previous stage output

Currently, we have deployed Minervas as an online system for public usage. Please check the [User Manual](./user_manual.md) for details.