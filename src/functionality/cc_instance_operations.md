# Example operation

<!-- toc -->

## Get the instance and its attributes
Function Description
* ```self.shader.world.instances```: Get a list of instances of the scene
* ```instance.{attr_name}```: Get the attributes of the instance, see the name of the instance attribute: [Instance](../dsl/instance.md)

example
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

example:

```python
class AddInstance(EntityProcessor):
    def process(self, *args, **kwargs):
        ins = self.shader.world.add_instance(
            id="test", label=1107, path="meshId", type="ASSET",
            transform=[1.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 0.0, 1.0]
        )
```
## Modify instance properties
### Modify the instance transformation matrix
When modifying this attribute, it is achieved by rotating, panning and zooming, and one or more of the following operations can be performed
#### Rotation example
`instance.set_rotation(rotation_list)`
*rotation_list: 3 x 3 matrix converted according to **row first** list*

#### Scaling example
`instance.set_scale(scale_list)`
*scale_list: a list of scaling factors*

#### Translation example
`instance.set_position(position_list)`
*position_list: a list of position coordinates*

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
