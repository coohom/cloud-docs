# Depth Estimation

## Introduction
Depth estimiation is an essential task in indoor scene understanding. We show the performance gain by generating dataset using our system.

Here we show the DSL for generating depth images which helps boosting the current depth estimation task.
More details can be found in the [paper](https://arxiv.org/pdf/2107.06149.pdf) and [supplementary document](https://drive.google.com/file/d/1avGTr44sGrWx_jWiNYEIrp3R7jbNPOgj/view).
## DSL code
<!-- For room layout estimation task, we create a
filter rule using DSL in the Scene Process Stage, and setting
the type of camera as “panorama”. We also use the sampler
of the transform component to randomly move cameras, and
use the output component to write out corner positions and
camera parameters. -->

TBD.

```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
from shapely.ops import nearest_points
from shapely.geometry import Point
import numpy as np
import math
 
class CameraSetter(EntityProcessor):
    # Set a camera in the room by a heuristic rule
    def set_camera(self, room):
        width = 640
        height = 480
        # look from right corner of the room
        camera_height = min(2000, self.shader.world.levels[0].height)
        right_corner = np.max(room.boundary, axis=0)
        room_polygon = room.gen_polygon()
        border, point = nearest_points(room_polygon, Point(right_corner))
        pos = [border.x - 200, border.y - 200, camera_height - 200]
        # look at room center
        look_at = room.position + [camera_height / 2]
            
        hfov = 57
        tan = (math.tan(math.radians(hfov / 2))) / (width / height)
        vfov = math.degrees(math.atan(tan)) * 2
            
        self.shader.world.add_camera(
            id=f"view_{room.roomId}",
            cameraType="PERSPECTIVE",
            hfov=hfov,
            vfov=vfov,
            imageWidth=width,
            imageHeight=height,
            position=pos,
            lookAt=look_at,
            up=[0, 0, 1]
        )
    
    def is_valid_room(self, room, num_furniture=3):
        # Check if the number of furniture in the room is above threshold.
        polygon = room.gen_polygon()
        count = 0
        for ins in self.shader.world.instances:
            if not ins.type == 'ASSET':
                continue
            if polygon.contains(Point([ins.transform[i] for i in [3, 7, 11]])):
                count += 1
        return count > num_furniture

    def process(self):
        # Delete all existing cameras
        for camera in self.shader.world.cameras:
            self.shader.world.delete_entity(camera)
 
        # Set new camera for valid room
        for room in self.shader.world.rooms:
            if self.is_valid_room(room):
                self.set_camera(room)

from ksecs.ECS.processors.render_processor import RenderProcessor
class Render(RenderProcessor):
    def process(self, *args, **kwargs):
        self.gen_rgb(distort=0, noise=0)

from ksecs.ECS.processors.pixel_processor import PixelProcessor
class DepthOutput(PixelProcessor):
    def process(self, **kwargs):
        self.gen_depth(distort=0, noise=0)
```

<!-- 
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
``` -->

## MINERVAS output sample
TBD.

<!-- ## Experimental Setup

In this experiment, we use NYUv2 as 
the real data. We split the images into 795 for training and
654 for testing. Then, we synthesize 14k images using our
system.
We use an SGD optimizer with an initial learning rate
1 × 10−4 with polynomial decay policy, momentum 0.9,
and weight decay 5 × 10−4. We set the mini-batch size to 8. In “s + r”, each batch contains 4 images from the real
dataset and 4 from the synthetic dataset. For each strategy,
we train the whole network for 15k iterations. -->

<!-- ## Results. 
We show more qualitative results in
Figure 7. As one can see, training on the synthetic and real
dataset, the network generates more accurate estimations
than that only using real images for training. The noise has
been significantly reduced in the depth estimation.

![fig_layout](./../examples_figs/fig_depth.png) -->