# Model
In our system, the CAD model of each object in the scene can be easily replaced by user. 
The category of object remains the same for reasonable result.
Since the mesh is the core asset of the database, we only explore its index in the database and do not allow users to access the raw data.
<!-- ## Randomly replace the model -->
## Domain randomization - Model sampler

<!-- **command_type value: model_replace** -->

<!-- Requirements and background: -->
<!-- <span style="color:blue">*Comments:* CCInstance? Unify the name across the doc.</span>. -->

MINERVAS provides `replace_model` method, which will provides following functionality:

 The input the `id` of an `Instance` object and randomly replace the model of this object with a new model with the same semantic.

<!-- Random replacement is valid for a given CCInstance (type=Asset only takes effect), other types of CCInstance may be ignored or an error may be reported. Then there are currently the following constraints (this part of the constraints can be gradually released with subsequent function development):

1. The size of the furniture before and after the replacement is kept the same (aligned by the scale parameter)
2. A furniture library needs to be preset, and only the model in the preset furniture library will be replaced. (This logic will be used as a bottom-up logic to ensure the robustness of the service)
   1. Models whose categories are not in the preset furniture library cannot be replaced. -->

### Function parameters

| First name | Required or not | Type | Description |
| :--------- | :------- | :----- | :--------------------- |
| id | Yes | String | Identifies the instance to be replaced |

<!-- example:
```python
class ReplaceModel(EntityProcessor):
    def process(self, *args, **kwargs):
        for instance in self.shader.world.instances:
            self.shader.world.replace_model(
                id=instance.id
            )
``` -->

### Example
Now, we show a DSL code which randomly replace the model of sofa and table.
```python
class MeshSampler(EntityProcessor):
    def process(self):
        for instance in self.shader.world.instances:
            # table category_id: 1032
            # sofa category_id: 1068 
            if instance.type == 'ASSET' and instance.label in [1032, 1068]:
                self.shader.world.replace_model(id=instance.id)
```
![mesh_sampler](../examples_figs/mesh_sampler.png)