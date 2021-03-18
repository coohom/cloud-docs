# Camera

DSL supports the addition of three types of cameras, including perspective cameras, orthographic cameras, and panoramic cameras.

When adding a camera, you need to set the camera's parameters, including the common parameters of all types of cameras and the unique parameters of specific types of cameras.

### General parameters
|Attribute|Description|Default value|Required|
|---|---|---|---|
|id|Camera ID, users need to add a prefix to ensure that the ID is unique| |Yes|
|cameraType|Camera type, support PERSPECTIVE (perspective camera), ORTHO (orthogonal camera), PANORAMA (panoramic camera)|"PERSPECTIVE"|
|position|Camera coordinates, the format is {'x':1,'y':2,'z':3}, the unit is mm| |Yes|
|lookAt|Target coordinates, the format is {'x':1,'y':2,'z':3}, the unit is mm|position+{'x':1,'y':0,'z': 0}|
|up|Camera up direction, the format is {'x':1,'y':2,'z':3}, the unit is mm|{'x':0,'y':0,'z': 1}|
|imageWidth|Width of the image| |Yes|
|imageHeight|The height of the image| |Yes|
|near|Cut plane near| 200|
|far|Cut plane far|2000000|
|iso|Indicates the sensitivity of the camera||
|fnumber|f value, indicating the aperture size||
|shutterSpeed|The shutter speed of the camera, the unit is s^-1||
### PERSPECTIVE specific parameters
|Attribute|Description|Default value|Required|
|---|---|---|---|
|vfov|Vertical fov, that is, fov in OpenGL, angle value|none|yes|
|hfov|Horizontal fov, when it coexists with vfov, vfov shall prevail, the angle value|none||

### ORTHO specific parameters
|Attribute|Description|Default value|Required|
|---|---|---|---|
|orthoWidth|The width of the camera displayed in the model space, in millimeters|none|yes|
|orthoHeight|The height displayed by the camera in the model space, in millimeters|none|yes|