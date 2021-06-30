# Depth Estimation
## Introduction
Depth estimiation is an essential task in indoor scene understanding. We show the performance gain by generating dataset using our system.

## DSL code
<!-- For room layout estimation task, we create a
filter rule using DSL in the Scene Process Stage, and setting
the type of camera as “panorama”. We also use the sampler
of the transform component to randomly move cameras, and
use the output component to write out corner positions and
camera parameters. -->


First, we import some necessary packages.
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
```

We filter scenes that contain rooms for manhattan layout estimation in the Scene Process Stage.

For the depth estimation task, we set the resolution of the image to 640x480 and horizontal field-of-view (FoV) to 53 degree in the Entity Process Stage, which is the same as those in Microsoft Kinect used in the NYUv2 dataset.

```python
class CameraSetting(EntityProcessor):
    def process(self):
        for camera in self.shader.world.cameras:
            camera.set_attr("imageWidth", 640)
            camera.set_attr("imageHeight", 480)
            camera.set_attr("cameraType", "PERSPECTIVE")
            camera.set_attr("hfov", 53)
```

## Minervas output sample

## Experimental Setup
In this experiment, we use NYUv2 as
the real data. We split the images into 795 for training and
654 for testing. Then, we synthesize 14k images using our
system.
We use an SGD optimizer with an initial learning rate
1 × 10−4 with polynomial decay policy, momentum 0.9,
and weight decay 5 × 10−4. We set the mini-batch size to 8. In “s + r”, each batch contains 4 images from the real
dataset and 4 from the synthetic dataset. For each strategy,
we train the whole network for 15k iterations.

## Results. 
We show more qualitative results in
Figure 7. As one can see, training on the synthetic and real
dataset, the network generates more accurate estimations
than that only using real images for training. The noise has
been significantly reduced in the depth estimation.

![fig_layout](./../examples_figs/fig_depth.png)