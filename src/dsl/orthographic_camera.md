# OrthographicCamera
## Attributes
<!-- ### General attributes -->
|Attribute|Type|Description|Default value|Required|
|---|---|---|---|---|
|id|str|Camera ID, users need to add a prefix to ensure that the ID is unique|-|Yes|
|position|dict|Camera coordinates, the format is {'x':1,'y':2,'z':3}, the unit is mm|-|Yes|
|lookAt|dict|Target coordinates, the format is {'x':1,'y':2,'z':3}, the unit is mm|position+{'x':1,'y':0,'z': 0}|
|up|dict|Camera up direction, the format is {'x':1,'y':2,'z':3}, the unit is mm|{'x':0,'y':0,'z': 1}|
|imageWidth|float|Width of the image|-|Yes|
|imageHeight|float|The height of the image|-|Yes|
|near|float|Cut plane near| 200|
|far|float|Cut plane far|2000000|
|orthoWidth|float|The width of the camera displayed in the model space, in millimeters|-|yes|
|orthoHeight|float|The height displayed by the camera in the model space, in millimeters|-|yes|

<!-- |cameraType|str|Camera type, support PERSPECTIVE (perspective camera), ORTHO (orthogonal camera), PANORAMA (panoramic camera)|"PERSPECTIVE"| -->
<!-- |iso|float|Indicates the sensitivity of the camera|| -->
<!-- |fnumber||f value, indicating the aperture size|| -->
<!-- |shutterSpeed||The shutter speed of the camera, the unit is s^-1|| -->