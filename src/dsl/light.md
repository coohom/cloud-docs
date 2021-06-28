# Light
DSL supports four types of lights. There are PointLight, RectangleLight, Sunlight, IESspotLight.

<!-- Each type of light has its own parameters which we list in the following. -->

The SDK provides the adjustment of lighting effects in the form of interfaces, so the attributes that can be directly adjusted are only the following list

<span style="color:blue">*Comments:* **emission** attrubtion is missing?</span>.

## General parameters
|Attribute|Description|
|---|---|
|lightType|PointLight, RectangleLight, SunLight, IESspotLight|

## Specific parameters

### RectangleLight
The size of rectangel light is determined by U and V vectors. The normal direction is a unit vector with the direction of cross prodcut of U and V vector.

|Attribute|Description|
|---|---|
|directionU|The format is {"x": 0.0, "y": -291.0, "z": 0.0}|
|normalDirection|The format is {"x": -0.0, "y": -0.0, "z": -1.0}|
|position|The format is {"x": 191.20065,"y": 9078.513,"z": 69.999985}, the unit is mm|

### PointLight
Point light radiates illumination into all directions uniformly.

|Attribute|Description|
|---|---|
|position|The format is {"x": 191.20065,"y": 9078.513,"z": 69.999985}|

### SunLight
Sun light is direction light. It radiates a specified power per unit area along a fixed direction.

|Attribute|Description|
|---|---|
|direction|The format is {"x": -0.57735026, "y": 0.57735026, "z": 0.57735026}|

### IESspotLight
IESspotlight is a spotlight with IES profile.
<span style="color:blue">*Comments:* IES profile can be selected? Or it always remains the default IES profile.</span>.

|Attribute|Description|
|---|---|
|direction|The format is {"x": -0.57735026, "y": 0.57735026, "z": 0.57735026}|
|position|The format is {"x": 191.20065,"y": 9078.513,"z": 69.999985}, the unit is mm|


# Light operation

<!-- toc -->

## Get the light and the attributes of the light

Function Description

* ```self.shader.world.lights```: Get the light list of the scene
* ```light.{attr_name}```: Get the attributes of the light. For the name of the light attribute, see: [Light](../dsl/light.md)

example
```python
class ReadLightDsl(EntityProcessor):
    def process(self):
        # loop all lights
        for light in self.shader.world.lights:
            position = light.position
```
## Modify the lighting attributes directly
Function Description
`light.set_attr({attr_name}, **kwargs)`[^args description]: modify light attributes

example
```python
class SetLightDsl(EntityProcessor):
    def process(self):
        for light in self.shader.world.lights:
            # set light attr
            light.set_attr('position', x=100, y=0, z=1000)
```
[^args description]: `**kwargs` is used for attributes of dictionary type, such as position, etc.

## Illumination adjustment interface
### Single light adjustment

#### tune_temp

-Function: adjust color temperature
-Entry: delta

#### tune_random

-Function: Random light, 50% probability attenuates according to ratio, 50% probability is uniformly sampled from the interval [0.1, 0.3] to get the attenuation coefficient.
-Entry: ratio, see above for usage

#### tune_intensity

-Function: adjust brightness
-Input parameters: ratio, brightness adjustment multiple

Example of use:

```python
class TuneLight(EntityProcessor):
    def process(self, *args, **kwargs):
        for light in self.shader.world.lights:
            # Adjust color temperature
            light.tune_temp(1)
            # Randomly adjust the light
            light.tune_random(0.5)
            # Randomly adjust the light intensity
            light.tune_intensity(0.2)
```

### The overall light intensity adjustment of the scene

#### tune_brightness__all_lights

-Function: adjust the brightness of all lights in the scene
-Input parameters: ratio, brightness adjustment multiple

#### tune_brightness__sunlight

-Function: adjust the multiple of natural light and turn off other light sources
-Input parameters: ratio, brightness adjustment multiple

Example of use:
```python
class TuneLights(EntityProcessor):
    def process(self, *args, **kwargs):
        self.tune_brightness__all_lights(0.8)
```

## Example
```python
class LightSampler(EntityProcessor):
    def process(self):
        for light in self.shader.world.lights:
            # K值，可以根据K与rgb的map来设置，行业标准，越小越暖，越大越冷
            light.tune_temp(5000)
```
![light_sampler](./../examples_figs/light_sampler.png)