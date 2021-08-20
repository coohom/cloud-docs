# Entity Processor

<!-- ## Description -->

The entity process stage is designed for batch processing entities in the scene set. 
Users can implement an `EntityProcessor` to control the entity process stage.

Also, attributes (component) of each object (entity) can be manipulated in this processor, including:
- [Camera](dsl/camera.md)
- [Light](dsl/light.md)
- [Material](dsl/material.md)
- [Mesh](dsl/mesh.md)
- [Trajectory](dsl/trajectory.md)
- [Instance](dsl/instance.md)

<!-- ### Function

|Function   |Description    |
|---    |---    |
|delete(enitiy) |delete an entity in the scene|
|copy(entity)   |copy an entity in the scene|
|get_rooms()    |return the room list (list of `class Room`)|

Also, many components can be manipulated, including:

- [Camera Component](./camera.md)
- [Trajectory Component](./trajectory.md)
- [Light Component](./light.md)
- [Material Component](./material.md)
- [Mesh Component](./mesh.md)
- [Transform Component](./transform.md)
- [Other Component](./other.md)

## Example

Delete an entity in the scene according to its type.

```python
class EntityExample(EntityProcessor):
    def process(self):
        for entity, (furnitureComp, semanticComp) in self.world.get_components(FurnitureComponent, SemanticComponent):
            if semanticComp.get_category() == "Desk":
                self.delete(entity)
``` -->

## Entity operation

<span style="color:blue">*Comments:* Need more details.</span>
## Get Entity
TODO

### Delete Entity
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

### Create Entity

## Entity filtering
We filter out cameras in the room with few furniture.
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
from shapely.geometry import Point
class CameraFilterProcessor(EntityProcessor):
    def process(self):
        for room in self.shader.world.rooms:
            polygon = room.gen_polygon()
            furniture_count = 0
            for ins in self.shader.world.instances:
                if not ins.type == 'ASSET':
                    continue
                if polygon.contains(Point([ins.transform[i] for i in [3, 7, 11]])):
                    furniture_count += 1
            if furniture_count < 5: # We only use room with more than or equal to 5 assets
                for camera in self.shader.world.cameras:
                    if polygon.contains(Point([camera.position[axis] for axis in "xyz"])):
                        self.shader.world.delete_entity(camera)
```
