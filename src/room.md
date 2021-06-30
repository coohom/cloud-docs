# Room

## Description

The room's information is encapsulated as `Room`.
<!-- Users could sample furniture layout using function `sample()`. -->
<!-- Also, users could use functions, such as `get_polygon()`, to get room polygon for further processing. -->

<span style="color:blue">*Comments:* More info about `room` needs here.</span>
### Function

|Function   |Description    |
|---    |---    |
<!-- |get_height()   |return the height of the room  |
|get_floor_corners()    |return the floor corners of the room   |
|get_ceiling_corners()  |return the ceiling corners of the room | -->
<!-- |get_polygon()  |return the polygon of the rooom using `shapely`| -->

### Attributes

|Function   |Description    |
|---    |---    |
<!-- |height |height of the room (`int`)  |
|id     |id of the room (`str`)   |
|type   |type name of the room (`str`) | -->

# Room Sampler

## Features

<span style="color:blue">*Comments:* `World/ccworld` and `Instance/CCInstance` should be consistent across the doc.</span>

For a given ccworld room, transform the space position of the CCInstance in the room to randomly generate a room layout. The new layout satisfies certain constraints and rules.

## Usage

```python
class RandomizeLayout(SceneProcessor):
     def process(self):
         room = self.shader.world.get_room("room_id")
         room.randomize_layout(self.shader.world)
```

## Use constraints

The main limitation at present is that it can only take effect for scenarios where the label is KJL. There are two main reasons:

1. At present, only the instance with type=Asset supports modification of transform to render on the server side, and currently only the furniture instance of the scene with the KJL tag satisfies the conditions.
2. In the logic implemented by layout_sampler, a large number of Kujiale categories are used to make logical judgments (such as judging whether furniture should be posted on the wall according to the category). This point needs to be improved in the future, adding related attributes in CCInstance.


## Example
```python
class RoomSampler(SceneProcessor):
    def process(self):
        for room in self.shader.world.rooms:
            room.randomize_layout(self.shader.world)
```
![room_sampler](./examples_figs/layout_sampler.png)