# Introduction

<span style="color:blue">*Comments:* Needs reivision.</span>

## Introduction to Minervas

Minervas is a scene cognitive training dataset solution for the interior scene agent industry. Users can use Minervas to generate large-scale low-cost scene recognition data sets based on Coohom's massive scene sets.

The core workflow of Minervas includes the following parts:
* Scene modification: users modify scene content (furniture, lighting, etc.), modify camera information (including ordinary camera and track camera)
* Rasterize data generation: based on the scene and camera, use the FF engine to generate instance, normal, and depth maps
* Render data generation: based on the scene and camera, use the Vray engine to generate rgb images
* Information extraction (Structure): extract scene or camera information to an output json file


