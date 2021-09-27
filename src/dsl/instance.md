# Instance

<!-- <span style="color:blue">*Comments:* Add more introduction of `Instance`</span>. -->

Each object in the scene is an `Instance`. User can add/delete some instance, or changing the transformation/scale for each instance.

## Attributes
| Attribute |Type| Description | Default value | Required |
| --------- |- | -| ------ | -------- |
| id |str| Instance ID, users need to add their own prefix to ensure that the ID is unique |-| Yes |
| label |int| The label of the instance, indicating the category to which the instance belongs |-| Yes |
| transform |list| The transformation matrix of the instance, which is a list type of a 4 x 4 matrix transformed according to **row first** |-| Yes |
| type |str| Possible values are MESH \| ASSET\| COMPOSITE |-| Yes |
<!-- |size|list|Properties only available when type is ASSET<span style="color:blue">*Comments:* more description here.</span>.||| -->

## Function
|Function   |Description    |
|---    |---    |
|set_attr({attr_name}, *args, **kwargs)|Set the attributes of the instance, see the name of the instance attributes|
|set_rotation(rotation_list)|Set rotation of instance. rotation_list: `list`. 3 x 3 matrix converted according to row first list.|
|set_scale(scale_list)|Set scale of instance. scale_list: `list`. a list of scaling factors|
|set_position(position_list)|Set position of instance. position_list: `list`. a list of position coordinates.|

<!-- <span style="color:blue">*Comments:* `set_attr` not supported? </span>. -->

## Get the instance and its attributes
<!-- Function Description
* ```self.shader.world.instances```: Get a list of instances of the scene
* ```instance.{attr_name}```: Get the attributes of the instance, see the name of the instance attribute: [Instance](../dsl/instance.md) -->

Example
```python
class ReadInstanceDsl(EntityProcessor):
    def process(self):
        # loop all instances
        for instance in self.shader.world.instances:
            label = instance.label
```

## Add instance
Function Description

```self.shader.world.add_instance({attr_name}={attr_value})```: Create a new instance and add it to the scene

Example:

```python
class AddInstance(EntityProcessor):
    def process(self, *args, **kwargs):
        ins = self.shader.world.add_instance(
            id="test", label=1107, path="meshId", type="ASSET",
            transform=[1.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 1.0]
        )
```


<!-- <span style="color:blue">*Comments:* Delete `Instance`. Unified for entities.</span>. -->
## Modify instance properties
### Modify the instance transformation matrix
When modifying this attribute, it is achieved by rotating, panning and zooming, and one or more of the following operations can be performed
<!-- #### Rotation example -->
<!-- `instance.set_rotation(rotation_list)` -->
<!-- *rotation_list: 3 x 3 matrix converted according to **row first** list* -->

<!-- #### Scaling example -->
<!-- `instance.set_scale(scale_list)` -->
<!-- *scale_list: a list of scaling factors* -->

<!-- #### Translation example -->
<!-- `instance.set_position(position_list)` -->
<!-- *position_list: a list of position coordinates* -->

example:
```python
class SetInstance(EntityProcessor):
    def process(self, *args, **kwargs):
        for ins in self.shader.world.instances():
            ins.set_position(
                [0, 0, 50]
            ).set_rotation(
                [1, 0, 0, 0, 1, 0, 0, 0, 1]
            ).set_scale([1, 1, 1])

```

For some cases, users want to generate scenes with disorder objects for exploring the generalizations of CV models. This can be easily achieved by using these interfaces, we show an example code below.

```python
import numpy as np
from scipy.spatial.transform import Rotation as R
class DisorderInstance(EntityProcessor):
    def process(self, *args, **kwargs):
        for ins in self.shader.world.instances():
            random_pos = np.array([ins.transform[i] for i in [3, 7, 11]]) + np.random.uniform(-1, 1, size=3) * 10
            random_pos[2] = np.random.random() * self.shader.world.levels[0].height
            ins.set_position(
                random_pos.tolist()
            ).set_rotation(
                np.concatenate(R.random().as_matrix()).tolist()
            ).set_scale(np.random.random(3).tolist())

```