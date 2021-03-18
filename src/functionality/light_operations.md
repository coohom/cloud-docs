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