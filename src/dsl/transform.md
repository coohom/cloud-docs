# Transform Component

## Description

DSL supports changing the transform of an entity to move the entity. 

### Function

|Function   |Description    |
|---    |---    |
|set_position(position)   |set the position (position : `tuple of 3 float`)  |
|get_position()   |get the position (position : `tuple of 3 float`)  |
|set_angles(angles)   |set the angles of three main axes (angles : `tuple of 3 float`)  |
|get_angles()   |get the angles of three main axes (angles : `tuple of 3 float`)  |
|rotate(angle, axis)   |rotate around a specific axis (angle: `float`, axis : `tuple of 3 float`) |
|translate(distance)   |tranlate along x-y-z axes (distance : `tuple of 3 float`)  |
|sample(translate, pitch, yaw)   |sample the transform within given distance or angle (translate : `tuple of 3 float`, pitch : `float`, yaw : `float`)  |

## Example

Sampling a random transform along z-axis within `0.1m` (`100mm` in the system), and pitch within `180` degrees.

```python
class TransformSampler(EntityProcessor):
    def process(self):
        for entity, (transformComp, semanticComp, furnitureComp) in \
            self.world.get_components(TransformComponent, SemanticComponent, FurnitureComponent):
            if semanticComp.get_category_name() == "Toy":
                transformComp.sample(translate=(1000, 1000, 0), pitch=pi, yaw=0)
```
