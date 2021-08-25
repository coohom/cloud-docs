# DefinedTrajectory

## Attributes
<!-- <span style="color:blue">*Comments:* This parameter list needs revision (e.g., description of keyPoints is incorrect).</span>.  -->

|Attribute||Description|Default value|Required|Remark|
|---|---|---|---|---|---|
|type||RANDOM (random trajectory); COVERAGE (bow-shape trajectory); DEFINED (user customized trajectory, usually by tapping the key frame in the scene).||||
|pitch|| The angle of pitch ||||
|height|| The height of camera. The unit is mm.||||
|imageWidth||The width of rendered image||Yes||
|imageHeight||The height of rendered image||Yes||
|keyPoints|| (Key points in image space. pixel indicies: [[[[x1, y1], [x2, y2], ...]]]) | | Yes | Three dimensional list. 1. list of keypoints set 2. list of pixel coordinates. 3. pixel coordinates|
|fps|| Frames per second | | No | Required if `frameCount` is not specified |
|speed|| trajectory speed (the unit is mm/s) | | No | Required if `frameCount` is not specified|
|speedMode|| Mode for randomized speed, 0: initial randomization 1: procedual randomization | | No | Required if `speed` is specified |
|frameCount|| Total frame count | | No | Required if `fps` is not specified |
|pitchMode|| Mode of pitch randomization, 0: initial randomization, 1: procedual randomization | | Yes ||
|hfow|| Horizontal field of view (the unit is degree) | | No | Required if camera type is default or 'PERSPECTIVE' |
|vfow|| Vertical field of view (the unit is degree) | | No | Required if camera type is default or 'PERSPECTIVE' |
|orthoWidth|| horizontal field of view (the unit is mm) | | No | Required if camera type is default or 'PERSPECTIVE' |
|orthoHeight|| vertical field of view (the unit is mm) | | No | Required if camera type is default or 'PERSPECTIVE' |
|heightMode|| Mode of camera height, 0: initial randomization, 1: procedual randomization | | Yes ||
