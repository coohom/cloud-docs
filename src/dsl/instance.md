# Instance

## General parameters
| Property | Description | Default value | Required |
| --------- | --------------------------------------- ---------------- | ------ | -------- |
| id | Instance ID, users need to add their own prefix to ensure that the ID is unique | | Yes |
| label | The label of the instance, indicating the category to which the instance belongs | | Yes |
| transform | The transformation matrix of the instance, which is a list type of a 4 x 4 matrix transformed according to **row first** | | Yes |
| type | Possible values are MESH \| ASSET\| CC_OBJECT\| COMPOSITE | | Yes |
|size|Properties only available when type is ASSET|||