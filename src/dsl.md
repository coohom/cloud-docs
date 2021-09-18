# DSL Programming Guide

MINERVAS has a programmable dataset generation pipeline with Domain-Specific Language. As the main interface for users to cutomize the dataset generation for different task, we describe our DSL in this section.

<!-- <span style="color:blue">*Comments:* Many formats in DSL description is not unified. </span> -->
<!-- toc -->

## Introduction to DSL of MINERVAS

The DSL (Domain-Specific Language) of MINERVAS is a kind of internal DSL, it is based on the Python programming language. 

Each DSL file submitted to MINERVAS system is a Python file ended with `.py`. 

In the Python file, users need to:
* Declare one or more classes inheriting from corresponding built-in processor class.
- Implement the cutomized operation in the `process()` function.
<!-- The essence of DSL writing is that the user customizes one or more subclasses in the py file. 
The subclasses:
* Three subclasses of the Processor class inherited from KsSDK
- Borrow the interface provided by the SDK and inherited attributes to implement custom functions in the `process()` function -->

## Processor classes
There are currently four processor classes in MINERVAS system, which reflect different stages of the dataset generation pipeline.

<!-- <span style="color:blue">TODO: Need updates. </span> -->

1. SceneProcessor, provides custom filtering and modifying 3D scenes in scene-level.
```python
from ksecs.ECS.processors.scene_processor import SceneProcessor
class sceneDsl(SceneProcessor):
	def process(self, *args, **kwargs):
		pass
```
2. EntityProcessor, provides custom modifying of each attributes of objects in entity-level.
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
class entityDsl(EntityProcessor):
	def process(self, *args, **kwargs):
		pass
```
3. RenderProcessor, provides customization in the rendering process. 
```python
from ksecs.ECS.processors.render_processor import RenderProcessor
class renderDsl(RenderProcessor):
	def process(self, *args, **kwargs):
		pass
```
4. PixelProcessor, provides customed post-processing of rendered image results
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class pixelDsl(PixelProcessor):
	def process(self, *args, **kwargs):
		pass
```
<!-- 5. StructureProcessor, edit the output structured data
```python
from ksecs.ECS.processors.structure_processor import StructureProcessor
class structureDsl(StructureProcessor):
	def process(self, *args, **kwargs):
		pass
``` -->
> **Tips**: Don't forget to import the corresponding processor class from `ksces.ECS.processors` before use.

<!-- ## An attribute - shader -->
## Attribute: shader
`shader` is a common attribute of all `Processor` classes. It is an instance of class `Shader`, which provides interface for accessing all 3D data assets and built-in function.

<!-- Concretly, the class `Shader` has two attributes: `world` and `image_handler` which are instances of class `World` and class `ImageHandler`.

<span style="color:blue">*Comments:* `Shader` has any functions? </span> -->
### `World` class

<!-- The user-defined class inherits the attribute shader, which connects to the underlying data structure of the SDK. -->
<!-- Shader is an instantiated object of class `Shader`, which has attributes world and image_handler -->


<!-- <span style="color:blue">*Comments:* More details (e.g. function list.) may be added for `World`, `Element` and `ImageHandler`.</span> -->

<!-- World is an instantiated object of class World, which is used to store the "database" of the input data of CC world, which is composed of various entities of Elment. -->

The class `Shader` has an attribute: `world`.
`world` object is an instance of class `World`. The `World` class is an interface for a whole 3D scene in the database. It contains serveral elements:

| Attribute | Type | Description    |
|---    |---  |---   |
| instances | list of `Instance` | All objects (furniture) in the scene |
| lights | list of `Light` | All lights in the scene |
| rooms | list of `Room` | All rooms in the scene (whole floorplan) |
| levels | list of `Level` | Information for each level floors in the scene|
| trajectories | list of `Trajectory` | All trajectories in the scene |
| cameras | list of `Camera` | All exist cameras in the scene |

We will introduce each class in the following parts.
<!-- #### Element
Currently supports six elements `Instance`, `Light`, `Room`, `Level`, `Trajectory`, and `Camera`.
Each element corresponds to a class, with its own attributes and methods -->

|Function|Description|
|---|---|
|delete_entity((entity)) |delete entity from the scene.|
|add_camera({attr_name}={attr_value})|create a new camera and add it to the scene|
|tune_brightness__all_lights(ratio) | adjust the brightness of all lights in the scene(ratio: brightness adjustment multiple)|
|tune_brightness__sunlight(ratio) | adjust the multiple of natural light and turn off other light sources. (ratio: brightness adjustment multiple) |
|replace_material(id, type, category) |domain randomization for materials. See [Material](./dsl/material.md)|
|replace_model(id)|domain randomization for models. See [Model](./dsl/mesh.md)|
|add_trajectory({attr_name}={attr_value})| create a new trajectory and add to the scene. See [Trajectory](./dsl/trajectory.md)|
|pick(**kwargs)|Save customized attributes as output. See example in [Layout Estimation](./examples/layout_estimation.md). This function is encouraged to be called in `StructureProcessor` for robustness.|
<!-- |(TBD)|-| -->

<!-- ### `ImageHandler` class

`image_handler` object is an instance of class `ImageHandler`. This class contains severl image-related operations which we will introduce in [Noise Simulation](dsl/pixel_process/noise.md).

| Attribute | Type | Description    |
|---    |---  |---   |
| (TBD) | - | - |

| Function | Description    |
|---    |---   |
| save_files(cid, content, suffix, name) | - |
|(TBD)|-| -->

## ECS-D
Since our system supports customization to the scene, the user should easily access the scene with a suitable 3D scene representation. Thus, we employ the Entity Component System (ECS) architecture to represent and organize the 3D scene in our system. Additionally, to facilitate the randomness of scene synthesis, we integrate random distributions into the original ECS architecture, ie, attaching a distribution to depict each component. The newly proposed architecture is named as ECS-D, where D denotes distributions on components.