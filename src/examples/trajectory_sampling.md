# SLAM
## Introduction

## DSL code

First, we import some necessary packages.
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
from ksecs.ECS.processors.entity_processor import EntityProcessor
from ksecs.ECS.processors.structure_processor import StructureProcessor
import copy
import glm
```

The ECS-D architecture and basic sam
pler give users the ability to create their scene sample strategy. Figure 12 shows an example of custom trajectory sam
pler DSL. We can further use this sampler for vision tasks, e.g., SLAM as Figure 13.

```python
class CustomTrajectorySampler(EntityProcessor):

    def calculate_vel(self, velocity, step_time):
        mu = glm.normalize(glm.vec3(np.random.normal(0, 1, size=3)))
        FORCE = 100
        f = FORCE * mu
        PHI, A, C_D, M = 1.204, 0.09, 0.1, 1.0
        d = -0.5 * glm.normalize(velocity) * PHI * A * C_D * glm.dot(velocity, velocity)
        velocity = velocity + (d + f) * M * step_time
        S_MAX = 10
        if S_MAX < sqrt(glm.dot(velocity, velocity)):
            velocity = S_MAX * glm.normalize(velocity)
        return velocity

    def process(self):
        for camera in self.shader.world.cameras:
            self.shader.world.delete_entity(camera)

        # FIXME: 还是相同的层高的问题
        level = self.shader.world.levels[0].height
        for room in self.shader.world.rooms:
            # init
            room_polygon = room.gen_polygon()
            camera_vel = glm.normalize(glm.vec3(np.random.normal(0, 1, size=3)))
            viewpoint_vel = glm.normalize(glm.vec3(np.random.normal(0, 1, size=3)))
            camera_pos = glm.vec3(room.position + [level / 2])
            viewpoint_pos = glm.vec3(room.position + [level / 2])
            # calcaulate road points
            length_of_trajectory, delta_time, scale = 100, 0.03, 1000
            for i in range(length_of_trajectory):
                # Camera
                camera_vel = self.calculate_vel(camera_vel, delta_time)
                camera_vel.z = 0
                new_position = camera_pos + scale * camera_vel * delta_time
                next_camera_point = Point(tuple(new_position.xy))
                if not next_camera_point.within(room_polygon):
                    p1, p2 = nearest_points(room_polygon, next_camera_point)
                    # print(p1, p2)
                    normal = glm.normalize(glm.vec3(p1.x - p2.x, p1.y - p2.y, 0))
                    camera_vel = glm.reflect(camera_vel, normal)
                camera_pos = camera_pos + scale * camera_vel * delta_time
                # View point
                viewpoint_vel = self.calculate_vel(viewpoint_vel, delta_time)
                new_position = viewpoint_pos + scale * viewpoint_vel * delta_time
                viewpoint_point = Point(tuple(new_position.xy))
                if not viewpoint_point.within(room_polygon):
                    p1, p2 = nearest_points(room_polygon, viewpoint_point)
                    # print(p1, p2)
                    normal = glm.normalize(glm.vec3(p1.x - p2.x, p1.y - p2.y, 0))
                    viewpoint_vel = glm.reflect(viewpoint_vel, normal)
                if new_position.z < 0:
                    viewpoint_vel = glm.reflect(viewpoint_vel, glm.vec3(0, 0, 1))
                if new_position.z > level:
                    viewpoint_vel = glm.reflect(viewpoint_vel, glm.vec3(0, 0, -1))
                viewpoint_pos = viewpoint_pos + scale * viewpoint_vel * delta_time
                worldUp = glm.normalize(glm.vec3(0.2 * (random.random() - 0.5),
                                                0.2 * (random.random() - 0.5), 1))
                self.shader.world.add_camera(
                    id=f"{room.roomId}_{i}",
                    hfov=70,
                    vfov=55,
                    imageWidth=640,
                    imageHeight=480,
                    position=list(camera_pos.xyz),
                    lookat=list(viewpoint_pos.xyz),
                    up=list(worldUp)
                )
```

## Minervas output sample
![trajectory_output](./../examples_figs/trajectory.png)


## Experimental Setup
3D reconstruction result by BundleFusion [[1]](#1).
## Result
![trajectory_output](./../examples_figs/fig_3d_reconstruction.png)

## References
<a id="1">[1]</a> 
Angela Dai, Matthias Nießner, Michael Zollh{\"o}fer, Shahram Izadi, and Christian Theobalt. Bundlefusion: Real-time globally consistent 3d reconstruction using on-the-fly surface reintegration. ACM Transactions on Graphics (TOG), 36(4):1, 2017.