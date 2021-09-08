# Trajectory
DSL supports adding trajectory to the entity. Trajectory is an important component especially for robotic related tasks. In the MINERVAS system, users could sample a random trajectory or add a handcrafted trajectory to the camera.

There are three types of trajectories:
* [Random Trajectory](../dsl/random_trajectory.md)
* [Coverage Trajectory](../dsl/converage_trajectory.md)
* [Defined Trajectory](../dsl/defined_trajectory.md)

## Attributes
<!-- ## Trajectory types
Two type of trajectory are supported in the DSL.
1. Random trajectory. It can also be classified by the shape of trajectory.
* Bow-shape trajectory
* Pure random trajectory
2. Customized trajectory. User can generate the customize trajectory by tapping the key frame in the scene. -->

<!-- <span style="color:blue">*Comments:* Default values are missing in the following forms.</span>. -->

<!-- ### General attributes -->
|Attribute|Type|Description|Default value|Required|
|---|---|---|---|---|
|type|str|RANDOM (random trajectory); COVERAGE (bow-shape trajectory); DEFINED (user customized trajectory, usually by tapping the key frame in the scene).|-|Yes|
|pitch|float| The angle of pitch |-|Yes|
|height|float| The height of camera. The unit is mm.|-|Yes|

<!-- ### General attributes for RANDOM and COVERAGE type trajectory
|Attribute|Description|
|---|---|
|initCamera|Initialize camera. Input arguments are the same as [Camera](dsl/camera.md). |
|fps| Frames per second |
|speed| trajectory speed (the unit is mm/s) |
|colisionPadding| The radius of collision detection |

#### Specific attributes for RANDOM type trajectory
|Attribute|Description|
|---|---|
|time|duration of time (the unit is s)|

#### Specific attributes for COVERAGE type trajectory
|Attribute|Description|
|---|---|
|boundary|Restriction range of trajectory| -->
<!-- ### Specific attributes for DEFINED type trajectory -->
<!-- <span style="color:blue">*Comments:* This parameter list needs revision (e.g., description of keyPoints is incorrect).</span>.  -->

<!-- |Attribute|Description|Default value|Required|Remark|
|---|---|---|---|---|
|imageWidth|The width of rendered image||Yes||
|imageHeight|The height of rendered image||Yes||
|keyPoints| (Key points in image space. pixel indicies: [[[[x1, y1], [x2, y2], ...]]]) | | Yes | Three dimensional list. 1. list of keypoints set 2. list of pixel coordinates. 3. pixel coordinates|
|fps| Frames per second | | No | Required if `frameCount` is not specified |
|speed| trajectory speed (the unit is mm/s) | | No | Required if `frameCount` is not specified|
|speedMode| Mode for randomized speed, 0: initial randomization 1: procedual randomization | | No | Required if `speed` is specified |
|frameCount| Total frame count | | No | Required if `fps` is not specified |
|pitchMode| Mode of pitch randomization, 0: initial randomization, 1: procedual randomization | | Yes ||
|hfow| Horizontal field of view (the unit is degree) | | No | Required if camera type is default or 'PERSPECTIVE' |
|vfow| Vertical field of view (the unit is degree) | | No | Required if camera type is default or 'PERSPECTIVE' |
|orthoWidth| horizontal field of view (the unit is mm) | | No | Required if camera type is default or 'PERSPECTIVE' |
|orthoHeight| vertical field of view (the unit is mm) | | No | Required if camera type is default or 'PERSPECTIVE' |
|heightMode| Mode of camera height, 0: initial randomization, 1: procedual randomization | | Yes || -->

<!-- ## Function
|Function   |Description    |
|---    |---    |
|{attr_name}| Get attributes of trajectory.| -->

### Get trajectory and its attributes

Function explanation
* `self.shader.world.trajectories`: Get trajectory list in the scene.
* `trajectory.{attr_name}`: Get attributes of trajectory.

example:
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
class ReadTrajDsl(EntityProcessor):
    def process(self):
        # loop all trajectories
        for traj in self.shader.world.trajectories:
            cameraHeight = traj.height
```

## Add trajectory
### Add coverage trajectory
* `self.shader.world.add_trajectory({attr_name}={attr_value})`: create a new trajectory and add to the scene.

example:
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
class CreateTrajDsl(EntityProcessor):
  def process(self):
    for room in self.shader.world.rooms:

            # Get room center
            room_center_x, room_center_y = room.position

            # Create trajectory of initial camera
            camera = self.shader.world.create_camera(
                id=room.id,

                hfov=110,
                vfov=125,

                imageWidth=1280,
                imageHeight=720,

                position=[room_center_x, room_center_y, 70],

                fnumber=8,
                iso=100,
                shutterSpeed=2
            )

            self.shader.world.add_trajectory(
                id=room.id,

                initCamera=camera,

                fps=3,

                speed=1500,

                pitch=0,

                height=70,

                collisionPadding=350,

                boundary=room.boundary,

                type="COVERAGE"
            )
```

### Add Customized trajectory

```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
class CreateTrajDsl(EntityProcessor):
    def process(self):
        self.make_traj(**param)
```

<!-- Explanation of **param: See attributes of Customized trajectory above. -->

## Example
The example for customized trajectory is shown in [SLAM](../examples/trajectory_sampling.md) section.
<!-- <span style="color:blue">*Comments:* Default values are missing in the following forms.</span>. -->