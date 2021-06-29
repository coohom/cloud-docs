# Scene Processor

## Description

The scene process stage takes
the scene database as input and allows users
to filter desired scenes and modify the room layout of selected scenes from the database. 
Users can implement a `SceneProcessor` to control the scene process stage.

Each room is an instance of the `class Room`.
Based on these, users could filter scenes and modify the furniture layout of a room.


<!-- |Function   |Description    |
|---    |---    |
|get_rooms()  |return the room list (list of `class Room`)| -->

More description about [Room](./room.md)

## Example

Filter a scene according to its room type. In this example, we filter scenes with kitchen.

```python
class SceneFilterExample(SceneProcessor):
    def process(self):
        for room in self.shader.world.rooms:
            # FIXME: How to check the type of room?
            if room.type == "kitchen":
                pass
            else:
                sys.exit(7)
```

Note that exit value 7 represents the exit is caused by unstatisfying scene.

A [web GUI](https://www.kujiale.com/coohomcloud/kloudscene#/) for scene filtering is more user-friendly. We recommend users to use filtering GUI instead of filtering in `SceneProcessor`. The `SceneProcessor` is optional.