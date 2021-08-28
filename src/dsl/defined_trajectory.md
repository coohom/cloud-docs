# CustomizedTrajectory

## Attributes
<!-- <span style="color:blue">*Comments:* This parameter list needs revision (e.g., description of keyPoints is incorrect).</span>.  -->

|Attribute|Type|Description|Required|Remark|
|---|---|---|---|---|
|pitch|float| The angle of pitch |Yes||
|height|float| The height of camera. The unit is mm.|Yes||
|imageWidth|int|The width of rendered image|Yes||
|imageHeight|int|The height of rendered image|Yes||
|keyPoints|list| (Key points in image space. pixel indicies: [[[[x1, y1], [x2, y2], ...]]]) | Yes | Three dimensional list. 1. list of keypoints set 2. list of pixel coordinates. 3. pixel coordinates|
|fps|int| Frames per second | - | Required if `frameCount` is not specified |
|speed|float| trajectory speed (the unit is mm/s) | - | Required if `frameCount` is not specified|
|speedMode|int| Mode for randomized speed, 0: initial randomization 1: procedual randomization | - | Required if `speed` is specified |
|frameCount|int| Total frame count | - | Required if `fps` is not specified |
|pitchMode|int| Mode of pitch randomization, 0: initial randomization, 1: procedual randomization | Yes ||
|hfow|float| Horizontal field of view (the unit is degree) | - | Required if camera type is default or 'PERSPECTIVE' |
|vfow|float| Vertical field of view (the unit is degree) | - | Required if camera type is default or 'PERSPECTIVE' |
|orthoWidth|float| horizontal field of view (the unit is mm) | - | Required if camera type is default or 'PERSPECTIVE' |
|orthoHeight|float| vertical field of view (the unit is mm) | - | Required if camera type is default or 'PERSPECTIVE' |
|heightMode|int| Mode of camera height, 0: initial randomization, 1: procedual randomization | Yes ||
