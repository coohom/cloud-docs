# DSL Description

<!-- toc -->

## Introduction to DSL

## Processor
There are currently three types of EntityProcessor, PixelProcessor, and StructureProcessor, which provide
CC world data, rasterized image results and other editing capabilities are supported.

The custom classes in the DSL should inherit from the above three categories, and use the interface provided by the SDK to complete the custom editing function.

### EntityProcessor

### PixelProcessor

### StructureProcessor


## World&Element
The "database" used to store the input data of CC world is composed of various entities of Elment

Currently supports six elements Instance, Light, Room, Level, Trajectory, Camera