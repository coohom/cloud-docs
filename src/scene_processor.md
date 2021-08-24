# Scene Processor

<!-- ## Description -->

The scene process stage takes
the scene database as input and allows users
to filter desired scenes and modify the room layout of selected scenes from the database. 
Users need to implement a class inherite from `SceneProcessor` to control the scene process stage.

Each room is an instance of the `class Room`.
Based on these, users could filter scenes and modify the furniture layout of a room.

|Attributes |Type | Description    |
|---    |---    |--- |
| -|-|- |

|Function   |Description    |
|---    |---    |
<!-- |get_rooms()  |return the room list (list of `class Room`)| -->

More description about [Room](./room.md)

## Scene filtering

In `SceneProcessor`, user can customize their rules for filtering scenes from the database. For example, the room type, the number of rooms, the number of furniture in the room, etc.
<!-- Filter a scene according to its room type. In this example, we filter scenes with kitchen. -->

In the following, we provide a DSL code for generating scenes which have more than three rooms and has at least two bedrooms.

```python
from ksecs.ECS.processors.scene_processor import SceneProcessor
class SceneFilterExample(SceneProcessor):
    def process(self):
        if len(self.shader.world.rooms) <= 3:
            sys.exit(7)
        bedroom_count = 0
        for room in self.shader.world.rooms:
            if room.type == "bedroom":
                bedroom_count += 1
        if bedroom_count < 2:
            sys.exit(7)
```

Note that exit value 7 represents the exit is caused by unstatisfying scene.

For some simple filtering rules, we recommed users to use a more user-friendly [GUI mode](https://www.kujiale.com/coohomcloud/kloudscene#/).

<!-- A [Web GUI](https://www.kujiale.com/coohomcloud/kloudscene#/) for scene filtering is more user-friendly. We recommend users to use filtering GUI instead of filtering in `SceneProcessor`. The `SceneProcessor` is optional. -->