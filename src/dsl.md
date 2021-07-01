# DSL description

Minervas has a programmable dataset generation pipeline with Domain-Specific Language. As the main interface for users to cutomize the dataset generation for different task, we describe our DSL in this section.

<span style="color:blue">*Comments:* Many formats in DSL description is not unified. </span>
<!-- toc -->

## Introduction to DSL

The essence of DSL writing is that the user customizes one or more subclasses in the py file. The subclasses:
* Three subclasses of the Processor class inherited from KsSDK
- Borrow the interface provided by the SDK and inherited attributes to implement custom functions in the `process()` function

## Four types

1. SceneProcessor, provides custom filtering and editing of CC world data in scene-level.
```python
from ksecs.ECS.processors.scene_processor import SceneProcessor
class sceneDsl(SceneProcessor):
	def process(self, *args, **kwargs):
		pass
```
2. EntityProcessor, provides custom editing of CC world data in entity-level.
```python
from ksecs.ECS.processors.entity_processor import EntityProcessor
class entityDsl(EntityProcessor):
	def process(self, *args, **kwargs):
		pass
```
3. PixelProcessor, provides custom editing of rasterized image results
```python
from ksecs.ECS.processors.pixel_processor import PixelProcessor
class pixelDsl(PixelProcessor):
	def process(self, *args, **kwargs):
		pass
```
4. StructureProcessor, edit the output structured data
```python
from ksecs.ECS.processors.structure_processor import StructureProcessor
class structureDsl(StructureProcessor):
	def process(self, *args, **kwargs):
		pass
```

## An attribute - shader

The user-defined class inherits the attribute shader, which connects to the underlying data structure of the SDK.
Shader is an instantiated object of class `Shader`, which has attributes world and image_handler


<span style="color:blue">*Comments:* More details (e.g. function list.) may be added for `World`, `Element` and `ImageHandler`.</span>
### World

World is an instantiated object of class World, which is used to store the "database" of the input data of CC world, which is composed of various entities of Elment.

#### Element
Currently supports six elements `Instance`, `Light`, `Room`, `Level`, `Trajectory`, and `Camera`.
Each element corresponds to a class, with its own attributes and methods

### ImageHandler

image_handler is an instantiated object of class ImageHandler, mainly used to process image-related operations