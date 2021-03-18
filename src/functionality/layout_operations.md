# Room Sampler

## Features

For a given ccworld room, transform the space position of the CCInstance in the room to randomly generate a room layout. The new layout satisfies certain constraints and rules.

## Use

```python
class RandomizeLayout(EntityProcessor):
     def process(self):
         room = self.shader.world.get_room("room_id")
         room.randomize_layout(self.shader.world)
```

## Use constraints

The main limitation at present is that it can only take effect for scenarios where the label is KJL. There are two main reasons:

1. At present, only the instance with type=Asset supports modification of transform to render on the server side, and currently only the furniture instance of the scene with the KJL tag satisfies the conditions.
2. In the logic implemented by layout_sampler, a large number of Kujiale categories are used to make logical judgments (such as judging whether furniture should be posted on the wall according to the category). This point needs to be improved in the future, adding related attributes in CCInstance.