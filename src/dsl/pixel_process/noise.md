# Noise simulation

MINERVAS system supports to simulate four common image noises:

1. Gaussian Noise
2. Poisson Noise
3. Salt and Pepper Noise
4. Kinect Noise

<!-- ## Instructions for use -->

<!-- ### Description -->
## Function

|Function |Description|
|---|---|
|add_depth_noise(img, noise_type) | img (`numpy.ndarray` with `dtype=uint16`) is the image to be processed. `noise_type` is an integer flag for noise type. See following list.|

<!-- Relationship of noise type flag with noise model: -->
```
0: GaussianNoiseModel
1: PoissonNoiseModel
2: SaltAndPepperNoiseModel
3: KinectNoiseModel
```
<!-- `add_depth_noise(img, noise_type)` can be called according to the above use cases -->
<!-- among them -->

<!-- ### Example
Following DSL shows the procedure of adding the noise to an exising image.
```python
class TestPixelDsl(PixelProcessor):
     def process(self, **kwargs):
         for cid, img in self.shader.image_handler.load_images("camera_depth.png", mode="pillow"):
             img_after_noise = self.shader.image_handler.add_depth_noise(img, 3)
             self.shader.image_handler.save_files(
                 cid, content=img_after_noise, suffix="png", name='depth'
             )
``` -->