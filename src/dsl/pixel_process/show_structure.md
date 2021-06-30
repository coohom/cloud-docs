# Room Structure Visualization

Minvervas also support visualize structure of room (wall, floor and ceiling) in rgb rendering image using lines.

* Note that this function are only supported under perspective camera.

Usage:
```python
class ShowStructureDsl(PixelProcessor):
    def process(self, **kwargs):
        gen_rgb(distort=0, noise=0, _struc=True)
```

Notes:
`_struc` is boolean value.
* False: Default. Don't visualize room structure.
* True: Enable room structure visualization.