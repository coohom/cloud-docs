# Entity Operation

## Get Entity
TODO

## Delete Entity
Function Description
* ```self.shader.world.delete_entity((entity))```: delete entity from the scene

example
```python
class DeleteCameraDsl(EntityProcessor):
     def process(self):
         # loop all camera
         for camera in self.shader.world.cameras:
             # delete camera
             entityId = self.shader.world.delete_entity(camera)
```

## Create Entity