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