# Pixel Processor

## Description

The pixel process stage modifies image output pixel-wisely and generates the final dataset.
Users can implement a `PixelProcessor` to control the pixel process stage.
Users could get:
1. rgb
2. depth
3. normal
4. instance
5. semantic

Each image is an instance of `class RenderResult`.
Based on these, users could modify image outputs.

More description about [RenderResult](./image.md)
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
