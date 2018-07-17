---
description: An explanation behind the wiring of the Promega.
---

# The Electrical Standard

This guide serves to describe the standard for the electrical system of the Promega and the reasoning behind it.

## The Standard

For all electrical components of the Promega, when facing the front, left should indicate 0, or a lower number and right should indicate 1 or a higher number.

For example: The right K'tana tool uses extruder drive 1 and heater 2 to work.

## Reasoning

The Duet board features two different ports for the extruders, thermistors and heaters. Additionally, the extruder assembly wiring features different connectors for all of these components. On top of that, you can configure the software settings of each of the tools in order to use particular heaters or extruders. This all combined allows you to create a large number of configurations for the extruder wiring. This standard is meant to explain and standardize that wiring.

## Explanation

### Extruder Drives

The Duet Maestro board has two different ports for the extruder, often referred to as E0 and E1. With this standard, the E0 port will power the left extruder and E1 will power the right extruder, always.

### Heaters

The Duet Maestro has two different heater ports labeled E0 HEAT and E1 HEAT. These are also noted as H1 and H2, because the heated bed is H0. With the standard, H1 will correspond to the left heater and H2 to the right heater.

## Thermistor

The thermistors ports on the Duet Maestro are referred to as E0 TEMP and E1 TEMP. In the firmware of the Duet, E0 TEMP is always bound to E0 HEAT and E1 TEMP is bound to E1 HEAT. Therefore, E0 TEMP corresponds to the left extruder and heater and E1 TEMP corresponds to the right extruder and heater.

## Tools

The lower tool number will apply to the left extruder and heater and the higher tool number to the right extruder and heater.

## Deviating from the Standard

In the configuration files and the wiring of the Promega you can deviate from this standard. To change the tool definition in the configuration files, read the [Help! My Extruders are Backwards](https://promega.printm3d.com/~/edit/drafts/-LHcd83qhBiRw2GAgwN_/firmware-guides/help-my-extruders-are-backwards) guide. For wiring read [Duet Maestro Wiring](https://promega.printm3d.com/~/edit/drafts/-LHcd83qhBiRw2GAgwN_/electrical-guides/duet-maestro-wiring) and [Extruder Assembly Wiring](https://promega.printm3d.com/~/edit/drafts/-LHcd83qhBiRw2GAgwN_/electrical-guides/extruder-assembly-wiring).

