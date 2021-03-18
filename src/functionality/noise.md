# Noise simulation
Currently, it supports to simulate four common image noises and add them to the depth map output, namely:
1. Gaussian noise
2. Poisson noise
3. Salt and pepper noise
4. kinect noise

## Instructions for use

### Example

```python
class KwsPixelDsl(PixelProcessor):
     def process(self, **kwargs):
         for cid, img in self.shader.image_handler.load_images("camera_depth.png", mode="pillow"):
             img_after_noise = self.shader.image_handler.add_depth_noise(img, 3)
             self.shader.image_handler.save_files(
                 cid, content=img_after_noise, suffix="png", name='depth'
             )
```
### Description
`add_depth_noise(img, noise_type)` can be called according to the above use cases
among them

1. `noise_type` is an integer flag, and the corresponding relationship with the noise model is:

```bash
0: GaussianNoiseModel
1: PoissonNoiseModel
2: SaltAndPepperNoiseModel
3: KinectNoiseModel
```
2. The data type of `img` is `numpy.ndarray` with `dtype=uint16`