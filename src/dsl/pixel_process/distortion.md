# Distortion Simulation
MINERVAS system supports distortion simulation.

Following function has the parameter for distortion.
<!-- ``` -->
* get_rgb(distort=0, noise=0)
* gen_normal(distort=0, noise=0)
* gen_instance(normal_threshold=230, distort=0, noise=0)
* gen_semantic(normal_threshold=230, distort=0, noise=0)
* gen_depth(distort=0, noise=0)
* gen_albedo(distort=0, noise=0)
<!-- ``` -->

<!-- Notes: -->
<!-- flag is a integer flag. -->
Parameter `distort` is an integer flag:
* 0: No distortion
* 1: Add distortion
### Example
Add distortion when rendering photo-realistic image.
```python
class AddDistortionDsl(PixelProcessor):
    def process(self, **kwargs):
        gen_rgb(distort=1, noise=0)
```
