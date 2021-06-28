# Scene Processor

## Description

The scene process stage takes
the scene database as input and allows users
to filter desired scenes and modify the room layout of selected scenes from the database. 
Users can implement a `SceneProcessor` to control the scene process stage.

Each room is an instance of the `class Room`.
Based on these, users could filter scenes and modify the furniture layout of a room.


|Function   |Description    |
|---    |---    |
|get_rooms()  |return the room list (list of `class Room`)|

More description about [Room](./room.md)

## Example

Filter a scene according to its room type. In this example, we filter scenes with kitchen.

```python
class SceneExample(SceneProcessor):
    def process(self):
        roomList = self.get_rooms()
        filter = False
        for room in roomList:
            if room.type == "kitchen":
                filter = True
        return filter
```
