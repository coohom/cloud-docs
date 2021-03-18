# Camera Operations

<!-- toc -->
## Get the camera and its attributes
Function Description
* ```self.shader.world.cameras```: Get the camera list of the scene
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
        camera = self.shader.world.add_camera(id="test_camera",
                                              cameraType="PERSPECTIVE",
                                              position={'x':0,'y':0,'z':1000},
                                              lookAt={'x':100,'y':0,'z':1000},
                                              imageWidth=1280,
                                              imageHeight=720,
                                              vfov=90)
```


## Modify camera
Function Description
* ```camera.set_attr({attr_name}, {attr_value})```: modify the attributes of the camera

example
```python
class KwsEntityDsl(EntityProcessor):
    def process(self):
        for camera in self.shader.world.cameras:
            # set camera attr
            camera.set_attr('position', {'x':100,'y':0,'z':1000})
            camera.set_attr('lookAt', {'x':200,'y':0,'z':1000})
```