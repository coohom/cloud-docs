# Material 
## Randomly replace materials

**command_type value: material_replace**

Requirements and background:

The main logic is a function that implements three related functions:

1. Enter CCInstance to randomly replace the material corresponding to each part (each part is sampled separately from the preset material library).
2. Enter CCInstance and the designated material category, and randomly replace the material of each part to the material of the corresponding material category. (Each part is sampled separately from the designated category of the preset material library)
3. Enter the CCInstance and the specified material id list, and randomly replace the material of each part to the material in the list.

## Parameter list
<span style="color:blue">*Comments:* Candidate mateiral categories need to be provided.</span>.

| First name | Required or not | Value | Remarks |
| :--------------- | :------------------------------- ------- | :----------------------------------------- ----------------- | :--------------------- |
| id | Yes | String | Identifies the CCInstance to be modified |
| type | Yes | REPLACE_ALL \| REPLACE_BY_CATEGORY \| REPLACE_TO_GIVEN_LIST | replacement type |
| category | Required when type=REPLACE_BY_CATEGORY | String | Category name to be replaced |
|ids|Required when type=REPLACE_TO_GIVEN_LIST |List of String|ID list to be replaced|

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

## Example

<span style="color:blue">*Comments:* TODO(@xuanfeng) Add information about material list api</span>.

<span style="color:blue">*Comments:* Code needs revision</span>.
```python
class MaterialSampler(EntityProcessor):
    def process(self):
        for instance in self.shader.world.instances:
            # floor category_id: 1227
            # sofa category_id: 1068 
            # carpet category_id: 1080
            if instance.label in [1227, 1068, 1080]:
                self.shader.world.replace_material(
                    id=instance.id,
                    # TODO: 选更合适的方式
                    # type='REPLACE_TO_GIVEN_LIST',
                    # ids=['5be44369c3f6261793457411'], # Get material list from API.
                    type='REPLACE_BY_CATEGORY',
                    category='METAL'
                )
```
![material_sampler](../examples_figs/material_sampler.png)