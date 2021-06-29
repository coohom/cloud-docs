# Output selection
There are servel renderer output we support: RGB renderings, instance map, depth map, normal map. Image based operation like noise, distortion, structure visualization are also supported.

What is the default output if PixelProcessor is not specified? 

<span style="color:blue">*Comments:* Argument list and description of each funtion should be added.</span>

## RGB rendering

Output format:
3 channel * 8 bit

Usage:

```python
from ksecs.ECS.processors.render_processor import RenderProcessor
class Render(RenderProcessor):
    def process(self, *args, **kwargs):
        self.gen_rgb(distort=0, noise=0)
```

## Normal map

Output format:
1. 3 channel * 8 bit
2. Suppose r, g, b represent three color channels
   * [-1, 1] range of normal direction value are mapped to [0, 255]


Usage:

```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class NormalDsl(PixelProcessor):
    def process(self, **kwargs):
        self.gen_normal(distort=1, noise=2)
```


## Instance map

Output format:
1. 1 channel * 16 bit
2. Each pixel value represent the instance id.
    * The mapping of pixel value and instance id can be found in `instance_map.json`.

Usage:
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class InstanceDsl(PixelProcessor):
    def process(self, **kwargs):
        self.gen_instance(normal_threshold=230, merge_bias=30, distort=0, noise=0)
```

Notes:
1. 