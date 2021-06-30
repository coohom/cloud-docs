# Distortion Simulation

Usage:
```python
class AddDistortionDsl(PixelProcessor):
    def process(self, **kwargs):
        gen_rgb(distort=flag, noise=0)
```

Notes:
flag is a integer flag.
* 0: No distortion
* 1: Add distortion