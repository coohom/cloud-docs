# Output selection
There are servel renderer output we support: RGB renderings, instance map, depth map, normal map. Image based operation like noise, distortion, structure visualization are also supported.

What is the default output if PixelProcessor is not specified? 

<span style="color:blue">*Comments:* Argument list and description of each funtion should be added.</span>


<span style="color:blue">*Comments:* Differences between `RenderProcessor` and `PixelProcessor`.</span>
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
2. Each pixel value represent a instance_id.
    * The mapping of pixel value and instance id can be found in `instance_map.json`.

Usage:
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class InstanceDsl(PixelProcessor):
    def process(self, **kwargs):
        self.gen_instance(normal_threshold=230, merge_bias=30, distort=0, noise=0)
```

Notes:
<span style="color:blue">*Comments:* TODO.</span>
1. normal_threshold:
2. merge_bias


## Semantic map

Output format:
1. 1 channel * 16 bit
2. Each pixel value represents a label_id

Usage:
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class SemanticDsl(PixelProcessor):
    def process(self, **kwargs):
        self.gen_semantic(normal_threshold=230, distort=0, noise=0)
```

Notes:
<span style="color:blue">*Comments:* TODO.</span>
1. normal_threshold:

## Depth map

Output format:
1. 1 channel * 16 bit

Usage:
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class DepthDsl(PixelProcessor):
    def process(self, **kwargs):
        self.gen_depth(distort=0, noise=0)
```

## Trajectory map
Visualize trajectory in the top-down view rendering result. Customized trajectory and bow-shape trajectory are currently supported.

Usage:
```python
from ksecs.ECS.processors.render_processor import RenderProcessor
class TrajDSL(RenderProcessor):
    def process(self, *args, **kwargs):
        self.gen_traj(**params)
```

Notes:
**params can be:
1. type: int. Select trajectory type.
    * 0: Customized trajectory
    * 1: Bow-shape trajectory
    * 2: Random trajectory

<span style="color:blue">*Comments:* More parameters?.</span>

## Albedo map

Ouput format:
4 channel * 8 bits

```python
from ksecs.ECS.processors.render_processor import RenderProcessor
class Render(RenderProcessor):
    def process(self, *args, **kwargs):
        self.gen_rgb(distort=0, noise=0)
```