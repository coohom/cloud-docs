# Light
DSL supports four types of lights. There are PointLight, RectangleLight, Sunlight, IESspotLight.

<!-- Each type of light has its own parameters which we list in the following. -->

<!-- The SDK provides the adjustment of lighting effects in the form of interfaces, so the attributes that can be directly adjusted are only the following list -->

<!-- <span style="color:blue">*Comments:* **emission (intensity, color temperature)** attribute is missing?</span>. -->

## Attributes
<!-- ### General attributes -->
|Attribute|Type|Description|
|---|---|---|
|lightType|str|PointLight, RectangleLight, SunLight, IESspotLight|
|energy|float|The intensity of light.|
|color|dict|The color of light. The format is {x": 3.4734852, "y": 6.955175, "z": 6.3826585}. It is the normalized rgb multipled by the energy.|


<!-- ### Specific attributes -->
<!-- 
#### RectangleLight
The size of rectangel light is determined by U and V vectors. The normal direction is a unit vector with the direction of cross prodcut of U and V vector.

|Attribute|Description|
|---|---|
|directionU|The format is {"x": 0.0, "y": -291.0, "z": 0.0}|
|normalDirection|The format is {"x": -0.0, "y": -0.0, "z": -1.0}|
|position|The format is {"x": 191.20065,"y": 9078.513,"z": 69.999985}, the unit is mm| -->

<!-- #### PointLight
Point light radiates illumination into all directions uniformly.

|Attribute|Description|
|---|---|
|position|The format is {"x": 191.20065,"y": 9078.513,"z": 69.999985}| -->

<!-- #### SunLight
Sun light is direction light. It radiates a specified power per unit area along a fixed direction.

|Attribute|Description|
|---|---|
|direction|The format is {"x": -0.57735026, "y": 0.57735026, "z": 0.57735026}| -->

<!-- #### IESspotLight -->
<!-- IESspotlight is a spotlight with measured IES profile, which can provide realistic lighting effect. -->
<!-- <span style="color:blue">*Comments:* IES profile can be selected? Or it always uses a default IES profile. More discussion about IES may be added here.</span>. -->

<!-- |Attribute|Description| -->
<!-- |---|---| -->
<!-- |direction|The format is {"x": -0.57735026, "y": 0.57735026, "z": 0.57735026}| -->
<!-- |position|The format is {"x": 191.20065,"y": 9078.513,"z": 69.999985}, the unit is mm| -->

### Access the attributes of light

<!-- Function Description -->
<!-- * ```self.shader.world.lights```: Get the light list of the scene -->
<!-- * ```light.{attr_name}```: Get the attributes of the light. For the name of the light attribute, see: [Light](../dsl/light.md) -->

example DSL:
```python
class ReadLightDsl(EntityProcessor):
    def process(self):
        # loop all lights
        for light in self.shader.world.lights:
            position = light.position
```
<!-- # Light operation -->
## Function

|Function|Description|
|---|---|
|set_attr({attr_name}, **kwargs)| modify light attributes. `**kwargs` is used for attributes of dictionary type, such as position, etc. |
|_tune_temp(delta) | Random adjust color temperature. (delta: weight for tuned color temperature) (1 - delta) * orig + delta * tuned|
| tune_random(ratio) | Random light intensity. 50% probability attenuates according to ratio, 50% probability is uniformly sampled from the interval [0.1, 0.3] to get the attenuation coefficient.|
| tune_intensity(ratio) | Set brightness attenutation. (ratio: brightness adjustment multiple)|
<!-- toc -->

<!-- <span style="color:blue">*Comments:* Any function for creating a new light?</span>. -->
### Modify the lighting attributes directly
<!-- Function Description
`light.set_attr({attr_name}, **kwargs)`[^args description]: modify light attributes -->

example DSL:
```python
class SetLightDsl(EntityProcessor):
    def process(self):
        for light in self.shader.world.lights:
            # set light attr
            light.set_attr('position', x=100, y=0, z=1000)
```
<!-- [^args description]: `**kwargs` is used for attributes of dictionary type, such as position, etc. -->

<!-- ## Illumination adjustment interface -->
<!-- ### Single light adjustment -->

<!-- #### tune_temp -->

<!-- -Function: adjust color temperature -->
<!-- -Entry: delta -->

<!-- #### tune_random -->
<!-- 
-Function: Random light, 50% probability attenuates according to ratio, 50% probability is uniformly sampled from the interval [0.1, 0.3] to get the attenuation coefficient.
-Entry: ratio, see above for usage -->

<!-- #### tune_intensity -->

<!-- -Function: adjust brightness -->
<!-- -Input parameters: ratio, brightness adjustment multiple -->


### The overall light intensity adjustment of the scene
There are two built-in function of `EntityProcessor` which can tune intensity of all lights.


|Function|Description|
|---|---|
|tune_brightness__all_lights(ratio) | adjust the brightness of all lights in the scene(ratio: brightness adjustment multiple)|
|tune_brightness__sunlight(ratio) | adjust the multiple of natural light and turn off other light sources. (ratio: brightness adjustment multiple) |


<!-- #### tune_brightness__all_lights -->

<!-- -Function: adjust the brightness of all lights in the scene -->
<!-- -Input parameters: ratio, brightness adjustment multiple -->

<!-- #### tune_brightness__sunlight -->

<!-- -Function: adjust the multiple of natural light and turn off other light sources -->
<!-- -Input parameters: ratio, brightness adjustment multiple -->

Example of use:
```python
class TuneLights(EntityProcessor):
    def process(self, *args, **kwargs):
        self.tune_brightness__all_lights(0.8)
```

## Domain randomization - Light Sampler
Example DSL:
<!-- ## Example -->
<!-- <span style="color:blue">*Comments:* `tune_temp` is not consistent with API above. Use color temperature or delta? </span>. -->
<!-- ```python
class LightSampler(EntityProcessor):
    def process(self):
        for light in self.shader.world.lights:
            # K值，可以根据K与rgb的map来设置，行业标准，越小越暖，越大越冷
            light.tune_temp(5000)
``` -->
<!-- Example of use: -->

```python
class LightsSampler(EntityProcessor):
    def process(self, *args, **kwargs):
        for light in self.shader.world.lights:
            # Adjust the color temperature randomly
            light._tune_temp(1)
            # Adjust the light intensity randomly
            light.tune_random(0.5)
            # Use lower light intensity
            light.tune_intensity(0.8)
```
![light_sampler](./../examples_figs/light_sampler.png)