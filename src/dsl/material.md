# Material 

Material is an important component for every object in the scene. Our DSL also supports sampling new materials for each object for domain randomization.

Since the material is the core asset of the database, we only explore its index in the database and do not allow users to access the raw data.

## Domain randomization - Material Sampler
<!-- ## Material Replacement API -->

MINERVAS provides `replace_material` method, which will provides following functionality:

1. `REPLACE_ALL`: Given a `Model` to randomly replace the material corresponding to each part (each part is sampled separately from the preset material library).
2. `REPLACE_BY_CATEGORY`: Given a `Model` and the desired material category, and randomly replace the material of each part to the material of the corresponding material category. (Each part is sampled separately from the desired category of the preset material library)
3. `REPLACE_TO_GIVEN_LIST`: Given a `Model` and the specified material id list, and randomly replace the material of each part to the material in the list.

### Function parameters

<span style="color:blue">*Comments:* Candidate mateiral categories need to be provided.</span>.

| First name | Required or not | Type | Description |
| :--------------- | :------------------------------- ------- | :----------------------------------------- ----------------- | :--------------------- |
| id | Yes | String | Identifies the `Model` to be modified |
| type | Yes | `REPLACE_ALL` \| `REPLACE_BY_CATEGORY` \| `REPLACE_TO_GIVEN_LIST` | replacement type |
| category | Required when type=`REPLACE_BY_CATEGORY` | String | Category name to be replaced |
|ids|Required when type=`REPLACE_TO_GIVEN_LIST` |List of String|ID list to be replaced|

<!-- Usage:

```python
class ReplaceMaterial(EntityProcessor):
    def process(self, *args, **kwargs):
        for instance in self.shader.world.instances:
            self.shader.world.replace_material(
                id=instance.id,
                type='REPLACE_BY_CATEGORY',
                category='METAL'
            )
``` -->

### Example

<!-- <span style="color:blue">*Comments:* TODO(@xuanfeng) Add information about material list api</span>. -->

<!-- <span style="color:blue">*Comments:* Code needs revision</span>. -->
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
                    type='REPLACE_ALL',
                )
```
![material_sampler](../examples_figs/material_sampler.png)