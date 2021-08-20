# Camera

DSL supports the addition of three types of cameras, including perspective cameras, orthographic cameras, and panoramic cameras.

When adding a camera, you need to set the camera's parameters, including the common parameters of all types of cameras and the unique parameters of specific types of cameras.

## Attributes
### General attributes
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

### Specific attributes
#### PERSPECTIVE camera
|Attribute|Description|Default value|Required|
|---|---|---|---|
|vfov|Vertical fov, that is, fov in OpenGL, angle value|none|yes|
|hfov|Horizontal fov, when it coexists with vfov, vfov shall prevail, the angle value|none||

#### ORTHO camera
|Attribute|Description|Default value|Required|
|---|---|---|---|
|orthoWidth|The width of the camera displayed in the model space, in millimeters|none|yes|
|orthoHeight|The height displayed by the camera in the model space, in millimeters|none|yes|


<!-- # Camera operations -->
## Function

<!-- toc -->
## Get the camera and its attributes
Function Description
* ```self.shader.world.cameras```: Get the camera list of the scene
* `self.shader.world.camera_ids`: get a list of camera ids of the scene
* ```camera.{attr_name}```: Get the attributes of the camera, see the name of the camera attribute: [Camera](../dsl/camera.md)

example
```python
class ReadCameraDsl(EntityProcessor):
    def process(self):
        # loop all camera
        for camera in self.shader.world.cameras:
            cameraType = camera.cameraType
```

## Create/Add Camera
Function Description
* ```self.shader.world.add_camera({attr_name}={attr_value})```: create a new camera and add it to the scene
* ```self.shader.world.create_camera({attr_name}={attr_value})```: create a camera

example
```python
class CreateCameraDsl(EntityProcessor):
    def process(self):
        # add camera
        camera = self.shader.world.add_camera(
        id="test_camera",
        cameraType="PERSPECTIVE",
        position={'x':0,'y':0,'z':1000},
        lookAt={'x':100,'y':0,'z':1000},
        imageWidth=1280,
        imageHeight=720,
        vfov=90
        hfov=105
        )
```


## Modify camera
Function Description
* ```camera.set_attr({attr_name}, *args, **kwargs)```[^args description]: modify the attributes of the camera
example
```python
class SetCameraDsl(EntityProcessor):
    def process(self):
        for camera in self.shader.world.cameras:
            # set camera attr
            camera.set_attr('position', x=100, y=0, z=1000)
            camera.set_attr('imageWidth', 1280)
            camera.set_attr('hfov', 90, "degree")
```
[^args description]: `*args` may have multiple input parameters, in addition to the value of hfov, vfov, you can also specify the unit as `"degree"`/`"rad"`; `**kwargs` is used as a dictionary Type of attributes, such as position, etc.


## Viewport selection

Our system also provide some pre-defined viewport for users.
<span style="color:blue">*Comments:* Any more view? </span>

### Top-down view
Usage:
```python
class TopView(EntityProcessor):
    def process(self):
        self.gen_topview(width, height)
```

## Domain randomization - Camera Sampler