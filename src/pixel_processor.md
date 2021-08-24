# Pixel Processor

<!-- ## Description -->

In the pixel process stage, the system modifies imagery output pixel-wisely and generates the final dataset.
Users can implement a `PixelProcessor` to control the pixel process stage.

Specifically, users can 
1. select the output information with interest. (e.g., normal map, semantic map)
2. generate randomized image noise.
3. add distortion to rendered image.
4. visualize strucutre of room.

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
