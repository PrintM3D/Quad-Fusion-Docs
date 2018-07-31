---
description: An explanation behind the wiring of the Crane.
---

# \*The Electrical Standard

This guide serves to describe the standard for the electrical system of the Quad Fusion and the reasoning behind it.

## The Standard

For all the electrical components of the Quad Fusion, when facing the front \(from left to right\) the motors \(or filament entry points\) are Drive 1, Drive 0, Drive 3, and Drive 2. 

## Reasoning

The Duet board features two different ports for the extruders, thermistors and heaters. Additionally, the extruder assembly wiring features different connectors for all of these components. On top of that, you can configure the software settings of each of the tools in order to use particular heaters or extruders. This all combined allows you to create a large number of configurations for the extruder wiring. This standard is meant to explain and standardize that wiring.

## Explanation

### Extruder Drives

The Duet Maestro board has two different ports for the extruder, often referred to as E0 and E1. With this standard, the E0 port will power Drive 0 and E1 will power Drive 1, always. Additionally, with the extension board added, External Driver 2 will power Drive 2 and External Driver 3 will power Drive 3, always. 

### Heaters

The Duet Maestro has two different heater ports labeled E0 HEAT and E1 HEAT. These are also noted as H1 and H2, because the heated bed is H0. With the standard, H1 will correspond to the extruder's heater and H2 will not be bothered.

## Thermistor

The thermistor's ports on the Duet Maestro are referred to as E0 TEMP and E1 TEMP. In the firmware of the Duet, E0 TEMP is always bound to E0 HEAT and E1 TEMP is bound to E1 HEAT. Therefore, E0 TEMP corresponds to the bed heater and E1 TEMP corresponds to the extruder heater.

## Tools

The Quad Fusion has a minimum of four tools, thus the drives previously mentioned will correspond to the tools. Such as, Drive 0 will be Tool 0, Drive 1 will be Tool 1, and so on. 

## Deviating from the Standard

In the configuration files and the wiring of the Quad Fusion you can deviate from this standard. To change the tool definition in the configuration files, read the [Help! My Extruders are Backwards](https://promega.printm3d.com/~/edit/drafts/-LHcd83qhBiRw2GAgwN_/firmware-guides/help-my-extruders-are-backwards) guide. For wiring read [Duet Maestro Wiring](https://promega.printm3d.com/~/edit/drafts/-LHcd83qhBiRw2GAgwN_/electrical-guides/duet-maestro-wiring) and [Extruder Assembly Wiring](https://promega.printm3d.com/~/edit/drafts/-LHcd83qhBiRw2GAgwN_/electrical-guides/extruder-assembly-wiring).

