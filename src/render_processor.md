# Render Processor
In the Render Stage, MINERVAS system uses the generated scenes to generate 2D renderings with the photo-realistic rendering engine.

<!-- ## Attributes
|Attributes |Type | Description    |
|---    |---    |--- |
| -|-|- | -->
## Function
|Function|Description|
|---|---|
|get_rgb(distort=0, noise=0)|Rendering photo-realistic image. distort(int) represent using distortion or not when rendering. See [Distortion Simulation](dsl/pixel_process/distortion.md) for details.  noise (int) represent adding noise or not when rendering. See [Noise Simulation](dsl/pixel_process/noise.md) for details.|

### Example: RGB rendering

Output format:
3 channel * 8 bit

Usage:

```python
from ksecs.ECS.processors.render_processor import RenderProcessor
class Render(RenderProcessor):
    def process(self, *args, **kwargs):
        self.gen_rgb(distort=0, noise=0)
```

