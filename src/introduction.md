# Introduction

## Introduction to EUS
EUS (Environment Understanding Solution) is a scene cognitive training data set solution for the indoor agent industry.
Users use EUS to generate large-scale low-cost scene recognition data sets based on KJL's massive scene sets.

The core workflow of EUS includes the following parts:
* Scene modification: users modify scene content (furniture, lighting, etc.), modify camera information (including ordinary camera and track camera)
* Rasterize data generation: based on the scene and camera, use the FF engine to generate instance, normal, and depth maps
* Render data generation: based on the scene and camera, use the Vray engine to generate rgb images
* Information extraction (Structure): extract scene or camera information to an output json file

## Introduction to KsSDK

