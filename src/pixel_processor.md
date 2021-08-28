# Pixel Processor

<!-- ## Description -->

In the pixel process stage, the system modifies imagery output pixel-wisely and generates the final dataset.
Users can implement a `PixelProcessor` to control the pixel process stage.

Specifically, users can 
1. select the output information with interest. (e.g., normal map, semantic map)
2. generate randomized image noise.
3. add distortion to rendered image.
4. visualize strucutre of room.

<!-- ## Attributes
|Attributes |Type | Description    |
|---    |---    |--- |
| -|-|- | -->
## Function
|Function|Description|
|---|---|
|gen_normal(distort=0)|Generate normal map. (distort: `int`)|
|gen_instance(distort=0)|Generate intance map. (distort: `int`) |
|gen_semantic(distort=0)| Generate semantic map. (distort: `int`)|
|gen_depth(distort=0, noise=0)|Generate depth map. (distort: `int`, noise: `int`)|
|gen_traj(**params)|Generate trajectory visualization (top-down view). (params: `dict`: parameter list from each type of [Trajectory](dsl/../../trajectory.md))|
|gen_albedo(distort=0)|Generate albedo map. (distort: `int`)|
<!-- Each image is an instance of `class RenderResult`. -->
<!-- Based on these, users could modify image outputs. -->

<!-- More description about [RenderResult](./image.md) -->
<!-- 
## Example

```python
class PixelExample(PixelProcessor):
    def process(self, **kwargs):
        images = kwargs.get("images")
        albedo = images.get('rgb')
        depth = images.get('depth')
        normal = images.get('normal')
        ...
``` -->
