# Randomly replace materials

**command_type value: material_replace**

Requirements and background:

The main logic is a function that implements three related functions:

1. Enter CCInstance to randomly replace the material corresponding to each part (each part is sampled separately from the preset material library).
2. Enter CCInstance and the designated material category, and randomly replace the material of each part to the material of the corresponding material category. (Each part is sampled separately from the designated category of the preset material library)
3. Enter the CCInstance and the specified material id list, and randomly replace the material of each part to the material in the list.

## parameter list

| First name | Required or not | Value | Remarks |
| :--------------- | :------------------------------- ------- | :----------------------------------------- ----------------- | :--------------------- |
| id | Yes | String | Identifies the CCInstance to be modified |
| type | yes | REPLACE_ALL \| REPLACE_BY_CATEGORY \| REPLACE_TO_GIVEN_LIST | replacement type |
| category | Required when type=REPLACE_BY_CATEGORY | String | Category name to be replaced |
|ids|type=REPLACE_TO_GIVEN_LIST Required when |List of String|ID list to be replaced|

example
```python
class ReplaceMaterial(EntityProcessor):
    def process(self, *args, **kwargs):
        for instance in self.shader.world.instances:
            self.shader.world.replace_material(
                id=instance.id,
                type='REPLACE_BY_CATEGORY',
                category='METAL'
            )
```

# Randomly replace the parameter list of the model

**command_type value: model_replace**

## Needs and background

The main function is: input a CCInstance and randomly select a label with the same label from our preset model library to replace the CCInstance.

Random replacement is valid for a given CCInstance (type=Asset only takes effect), other types of CCInstance may be ignored or an error may be reported. Then there are currently the following constraints (this part of the constraints can be gradually released with subsequent function development):

1. The size of the furniture before and after the replacement is kept the same (aligned by the scale parameter)
2. A furniture library needs to be preset, and only the model in the preset furniture library will be replaced. (This logic will be used as a bottom-up logic to ensure the robustness of the service)
   1. Models whose categories are not in the preset furniture library cannot be replaced.

## parameter list

| First name | Required or not | Value | Remarks |
| :--------- | :------- | :----- | :--------------------- |
| id | Yes | String | Identifies the CCInstance to be replaced |

example:
```python
class ReplaceModel(EntityProcessor):
    def process(self, *args, **kwargs):
        for instance in self.shader.world.instances:
            self.shader.world.replace_model(
                id=instance.id
            )
```