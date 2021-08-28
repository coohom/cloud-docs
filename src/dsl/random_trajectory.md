# RandomTrajectory

## Attributes
|Attribute|Type|Description|Default value|Required|
|---|---|---|---|---|
|pitch|float| The angle of pitch |-|Yes|
|height|float| The height of camera. The unit is mm.|-|Yes|
|initCamera|`Camera`|Initialize camera. Input arguments are the same as [Camera](dsl/camera.md). |-|Yes|
|fps|int| Frames per second |-|Yes|
|speed|float| trajectory speed (the unit is mm/s) |-|Yes|
|colisionPadding|float| The radius of collision detection |-|Yes|
|time|float|duration of time (the unit is s)|-|Yes|