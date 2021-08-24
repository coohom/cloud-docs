# Semantic Segmentation

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
from ksecs.ECS.processors.pixel_processor import PixelProcessor
from ksecs.ECS.processors.entity_processor import EntityProcessor
```

For the semantic segmentation task, we set the type of camera to panorama in the Entity Process Stage, and output the semantic label image in the Pixel Process Stage.
We also map our semantic label to the NYUv2 40 label set using our DSL.

```python
class CameraSetting(EntityProcessor):
    def process(self):
        for camera in self.shader.world.cameras:
            camera.set_attr("imageWidth", 1024)
            camera.set_attr("imageHeight", 512)
            camera.set_attr("cameraType", "PANORAMA")
```

```python
class LabelMapping(PixelProcessor):
    def process(self, **kwargs):
        self.gen_semantic(label_arch=NYU40_Mapping)
```


## MINERVAS output sample

## Experimental Setup

In this experiment, we use 2D-3D-S [[1]](#1) as the real data. We split the images into 955 for
training, 84 for validation, and 373 for testing. Then, we
synthesize 12k panoramic images using our system. Each
panorama image corresponds to one room in scenes.
We use an SGD optimizer with an initial learning rate of
2 × 10−2 with a polynomial decay policy, momentum 0.9,
and weight decay of 10−4. We set the mini-batch size to
8. In “s + r”, each batch contains 4 images from the real
dataset and 4 from the synthetic dataset. For each strategy,
we train the whole network for 10k iterations.

## Results

We show more qualitative results of semantic segmentation in Figure 5. As can be seen, training
on the synthetic and real dataset achieves the best result.
The boundary is more clear in semantic segmentation. It
demonstrates that our synthetic data could be used to im-
prove the performance of network.

![fig_segmentation](./../examples_figs/fig_semantic.png)
<!-- ![table_layout](./../examples_figs/table_layout.png) -->

## References
<a id="1">[1]</a> 
Iro Armeni, Sasha Sax, Amir R Zamir, and Silvio Savarese. Joint 2d-3d-semantic data for indoor scene understanding. arXiv preprint arXiv:1702.01105, 2017.