# Trajectory

## Trajectory types
Two type of trajectory are supported in the DSL.
1. Random trajectory. It can also be classified by the shape of trajectory.
* Bow-shape trajectory
* Pure random trajectory
2. Customized trajectory. User can generate the customize trajectory by tapping the key frame in the scene.

<span style="color:blue">*Comments:* Defualt values are missing.</span>.

## General parameters
|Attribute|Description|Default value|Required|
|---|---|---|---|
|type|RANDOM; COVERAGE; DEFINED||Yes|
|pitch| The angle of pitch | | Yes |
|height| The height of camera. The unit is mm.|| Yes |

## General parameters for Random trajectory
|Attribute|Description|Default value|Required|
|---|---|---|---|
|initCamera|Initialize camera. Input arguments are the same as [Camera](dsl/camera.md). | | Yes |
|fps| Frames per second | | Yes |
|speed| trajectory speed (the unit is mm/s) | | Yes |
|colisionPadding| The radius of collision detection | | Yes |

### Bow-shape trajectory
|Attribute|Description|Default value|Required|
|---|---|---|---|
|boundary|Restriction range of trajectory|provided by SDK|Yes|

### Pure random trajectory
|Attribute|Description|Default value|Required|
|---|---|---|---|
|time|duration of time (the unit is s)||Yes|

## Specific parameters for Customized trajectory
|Attribute|Description|Default value|Required|Remark|
|---|---|---|---|---|
|imageWidth|The width of rendered image||Yes||
|imageHeight|The height of rendered image||Yes||
|keyPoints| ? (关键帧位置信息，实为图像向上的pixel index，格式：[[[[x1, y1], [x2, y2], ...]]]) | | Yes | Three layer architecture. <span style="color:blue">*Comments:* TBD Not understand.</span>.|
|fps| Frames per second | | No | Required if <span style="color:blue">*Comments:* TBD Not understand.</span>. |
|speed| trajectory speed (the unit is mm/s) | | No | <span style="color:blue">*Comments:* TBD Not understand.</span>. |
|speedMode| Mode for randomized speed, 0: initial randomization 1: procedual randomization | | No | Required if has speed |
|frameCount| Total frame count | | No | ? |
|pitchMode| Mode of pitch randomization, 0: initial randomization, 1: procedual randomization | | Yes ||
|hfow| Horizontal field of view (the unit is degree) | | No | Required if camera type is default or 'PERSPECTIVE' |
|vfow| Vertical field of view (the unit is degree) | | No | Required if camera type is default or 'PERSPECTIVE' |
|orthoWidth| horizontal field of view (the unit is mm) | | No | Required if camera type is default or 'PERSPECTIVE' |
|orthoHeight| vertical field of view (the unit is mm) | | No | Required if camera type is default or 'PERSPECTIVE' |
|heightMode| Mode of camera height, 0: initial randomization, 1: procedual randomization | | Yes ||

example:
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
class CreateTrajDsl(EntityProcessor):
  def process(self):
    for room in self.shader.world.rooms:

            # 获取房间中心
            room_center_x, room_center_y = room.position

            # 创建轨迹初始相机
            camera = self.shader.world.create_camera(

                # id必填
                id=room.id,

                # 设置视场
                hfov=110,
                vfov=125,

                # 设置图片大小
                imageWidth=1280,
                imageHeight=720,

                # 设置相机位置
                position=[room_center_x, room_center_y, 70],

                # 设置图片亮度
                # f值 --> 光圈大小
                # ISO --> 相机的感光度
                # ShutterSpeed --> 相机的快门速度。 曝光时间 = 1/快门速度（单位秒）。例如，shutterSpeed=2表示，暴光时间=1/2秒
                fnumber=8,
                iso=100,
                shutterSpeed=2
            )

            # 添加轨迹
            self.shader.world.add_trajectory(
                # 轨迹id
                id=room.id,

                # 初始相机
                initCamera=camera,

                # 每秒帧数
                fps=3,

                # 轨迹速度(单位mm/s)
                speed=1500,

                # 轨迹俯仰角(角度值)
                pitch=0,

                # 相机高度(mm)
                height=70,

                # 碰撞检测半径(mm)
                collisionPadding=350,

                # 轨迹的限制范围
                boundary=room.boundary,

                # 轨迹类型为弓字型
                type="COVERAGE"
            )
```