# Noise simulation
MINERVAS supports to simulate four common image noises and add them to the depth map output, namely:
1. Gaussian noise
2. Poisson noise
3. Salt and pepper noise
4. kinect noise

<!-- ## Instructions for use -->
### Description
`add_depth_noise(img, noise_type)` can be called according to the above use cases
among them

1. `noise_type` is an integer flag, and the corresponding relationship with the noise model is:

```bash
0: NoNoiseModel
1: GaussianNoiseModel
2: PoissonNoiseModel
3: SaltAndPepperNoiseModel
4: KinectNoiseModel
```
2. The data type of `img` is `numpy.ndarray` with `dtype=uint16`

