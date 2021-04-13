# DSL Sample Code
## Code description

This example simulates a sweeping robot traveling in a room with a bow-shaped trajectory at a fixed rate, and it takes 3 sets of pictures per second.



## Sample code

```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
from ksecs.ECS.processors.entity_processor import EntityProcessor
from ksecs.ECS.processors.structure_processor import StructureProcessor
 
ID_PREFIX = 'USER'
 
class TestPixelDsl(PixelProcessor):
    def process(self, **kwargs):
        self.gen_instance(normal_threshold=230, merge_bias=30)
        self.gen_semantic(normal_threshold=230)
 
 
class TestEntityDsl(EntityProcessor):
    def process(self):
        for camera in self.shader.world.cameras:
            self.shader.world.delete_entity(camera)
 
        for room in self.shader.world.rooms:
            # Get room center
            room_center_x, room_center_y = room.position
            traj_id = '_'.join([ID_PREFIX, 'TRAJ', room.id])
            # Create track initial camera
            camera = self.shader.world.create_camera(
 
                # id required
                id=traj_id+'_INIT',
 
                # Set the field of view
                hfov=110,
                vfov=125,
 
                # Set picture size
                imageWidth=512,
                imageHeight=512,
 
                # Set camera position
                position={'x':room_center_x, 'y':room_center_y, 'z':60},
 
                # Set picture brightness
                # fnumber --> Aperture size
                # ISO --> Camera sensitivity
                # ShutterSpeed --> The shutter speed of the camera.Exposure time = 1/shutter speed（s）.For example，shutterSpeed=2，means the exposure time=1/2s
                fnumber=8,
                iso=100,
                shutterSpeed=2
            )
 
            # Add track
            self.shader.world.add_trajectory(
                # Track id
                id=traj_id,
 
                # Initial camera
                initCamera=camera,
 
                # Frames per second
                fps=3,
 
                # Track speed (unit mm/s)
                speed=1200,
 
                # Track pitch angle (angle value)
                pitch=0,
 
                # Camera height (mm)
                height=60,
 
                # Collision detection radius (mm)
                collisionPadding=300,
 
                # Limit range of trajectory
                boundary=room.boundary,
 
                # The trajectory type is bow font
                type="COVERAGE"
            )

class TestStructureDSL(StructureProcessor):

    def process(self):

        for camera in self.shader.world.cameras:

            self.shader.world.pick(

                id=camera.id,

                # Output the two-dimensional trajectory coordinates of the camera
                location=[camera.position['x'], camera.position['y']]

            )
```
