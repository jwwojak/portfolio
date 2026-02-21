---
title: "API Documentation"
---

Intro goes here.

## Robotics API content

Written for the Opentrons Python API. These may have been revised since their initial publication.

## Tutorial conent

[//]: <> (My changes in https://github.com/Opentrons/opentrons/pull/13046)

Use changes to the intro tutorial.

## Liquid handling methods

[//]: <> (My changes in https://github.com/Opentrons/opentrons/pull/15695)
[//]: <> (And in https://github.com/Opentrons/opentrons/pull/12251)

Examples of foo

### Define and load liquids

Labeling Liquids in Wells
Optionally, you can specify the liquids that should be in various wells at the beginning of your protocol. Doing so helps you identify well contents by name and volume, and adds corresponding labels to a single well, or group of wells, in well plates and reservoirs. Viewing the initial liquid setup in a Python protocol is available in the Opentrons App v6.3.0 or higher.

To use these optional methods, first create a liquid object with :py:meth:`.ProtocolContext.define_liquid` and then label individual wells by calling :py:meth:`.Well.load_liquid`, both within the run() function of your Python protocol.

Let's examine how these two methods work. The following examples demonstrate how to define colored water samples for a well plate and reservoir.

Defining Liquids
This example uses define_liquid to create two liquid objects and instantiates them with the variables greenWater and blueWater, respectively. The arguments for define_liquid are all required, and let you name the liquid, describe it, and assign it a color:

greenWater = protocol.define_liquid(
    name="Green water",
    description="Green colored water for demo",
    display_color="#00FF00",
)
blueWater = protocol.define_liquid(
    name="Blue water",
    description="Blue colored water for demo",
    display_color="#0000FF",
)
.. versionadded:: 2.14

The display_color parameter accepts a hex color code, which adds a color to that liquid's label when you import your protocol into the Opentrons App. The define_liquid method accepts standard 3-, 4-, 6-, and 8-character hex color codes.

Labeling Wells and Reservoirs
This example uses load_liquid to label the initial well location, contents, and volume (in µL) for the liquid objects created by define_liquid. Notice how values of the liquid argument use the variable names greenWater and blueWater (defined above) to associate each well with a particular liquid:

well_plate["A1"].load_liquid(liquid=greenWater, volume=50)
well_plate["A2"].load_liquid(greenWater, volume=50)
well_plate["B1"].load_liquid(blueWater, volume=50)
well_plate["B2"].load_liquid(blueWater, volume=50)
reservoir["A1"].load_liquid(greenWater, volume=200)
reservoir["A2"].load_liquid(blueWater, volume=200)
.. versionadded:: 2.14

This information shows up in the Opentrons App (v6.3.0 or higher) after you import your protocol. A summary of liquids is available on the protocol detail page, and well-by-well detail is available in the Initial Liquid Setup section of the run setup page.

Note

load_liquid does not validate volume for your labware nor does it prevent you from adding multiple liquids to each well. For example, you could label a 40 µL well plate with greenWater, volume=50, and then also add blue water to the well. The API won't stop you. It's your responsibility to ensure the labels you use accurately reflect the amounts and types of liquid you plan to place into wells and reservoirs.

Labeling vs Handling Liquids
The load_liquid arguments include a volume amount (volume=n in µL). This amount is just a label. It isn't a command or function that manipulates liquids. It only tells you how much liquid should be in a well at the start of the protocol. You need to use a method like :py:meth:`.transfer` to physically move liquids from a source to a destination.

### Detect lquids

The `InstrumentContext.detect_liquid_presence` method tells a Flex pipette to check for liquid in a well. It returns `True` if the pressure sensors in the pipette detect a liquid and `False` if the sensors do not. 

Aspiration isn't required to use `detect_liquid_presence()`. This is a standalone method that can be called when you want the robot to record the presence or absence of a liquid. When `detect_liquid_presence()` finds an empty well it won't raise an error or stop your protocol.

A potential use of liquid detection is to try aspirating from another well if the first well is found to contain no liquid.

```python
if pipette.detect_liquid_presence(reservoir["A1"]):
    pipette.aspirate(100, reservoir["A1"])
else:
    pipette.aspirate(100, reservoir["A2"])

## Require Liquids

The InstrumentContext.require_liquid_presence method tells a Flex pipette to check for and require liquid in a well.

Aspiration isn't required to use require_liquid_presence(). This is a standalone method that can be called when you want the robot to react to a missing liquid or empty well. When require_liquid_presence() finds an empty well, it raises an error and pauses the protocol to let you resolve the problem. See also lpd.

```python
 pipette.require_liquid_presence(reservoir["A1"])
    pipette.aspirate(100, reservoir["A1"])  # only occurs if liquid found
```