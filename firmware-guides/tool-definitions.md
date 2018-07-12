# Tool Definitions

This guide will explains the default tool definitions for both the K'Tana and the Compound and explains how to change tools. This can be useful to create complex mixing and switching prints. This guide is not for beginners. Read the [Introduction to Tools](../getting-started/an-introduction-to-tools.md) guide in order to better understand the tool system.

## Default Tool Definitions

Compound Tools:

* `T0`: Mixing tool
  * Extruder Drive 0 \(Left\) & Extruder Drive 1 \(Right\)
  * Heater 2
  * Allows for extruding two filaments and combining them at a 1:1 ratio
* `T1`: Single Left
  * Extruder 0 \(Left\)
  * Heater 2
  * Extrudes with only the right extruder
* `T2`: Single Right
  * Extruder 1 \(Right\)
  * Heater 2
  * Extrudes with only the left extruder

K'Tana Tools:

* `T0`: K'tana Single Left
  * Extruder Drive 0 \(Left\)
  * Heater 1
* `T1`: K'tana Single Right
  * Extruder Drive 1 \(Right\)
  * Heater 2

As seen above, the Promega has two different extruder drives and two heaters. The current configuration is set-up to make everything on the left a lower number than everything on the right. For example if you were using the left K'tana extruder tool it would:

* Be called `T0` 
* Use extruder drive `D0` which is plugged into extruder motor port 0 on the Duet Maestro
* Use heater `H1` \(remember that `H0` is reserved for the heated bed\)

This same concept is applied throughout all the different tools with one exception. The compound uses Heater 2 or `H2` . The reason for this is that the compound wiring comes around the right side of the extruder, hence we found it logical to assign this to heater 2. All wiring and configuration can be changed to your personal preference.

## Tool Definition Command `M563`

The `M563` command allows you to define a tool, it has the following parameters:

* `Pnnn` : The tool number
* `S"toolname"`: The tool name
* `Dnnn` : The assigned extruder drive
* `Hnnn` : The assigned heater number
* `Fnnn` : The fans mapped to the tool.

The extruder drive numbers start from 0 and immediately follow the X, Y and Z axes stepper motor drives on the Duet Board. You can configure the order of these drives with the `M584` command.

The heater number is usually higher than 1 since 0 is the heated bed.

The nozzle fans are mapped to port 2 on the Duet Maestro. So configuring `F2` in the tool definitions will allow you to turn on the fans with the `M106 Snnn` command instead of the `M106 P2 Snnn` command.

## Defining Your Own Tools

Defining your own tools is useful to create prints that switch colors in the middle of a print. This is more applicable to the compound tool than the K'tana. To define a new tool enter the `M563` command in the configuration file, then follow it with the extruder drive and heater number that you would like to use.

## Mixing Ratios

To enable mixing rations for ta specific tool. Enter the `M568` command with the tool number \(`Pnnn` \) and the enable parameter \(`Snnn` \). For example, if I wanted to enable tool mixing for tool 3 I would enter the command `M568 P3 S1` . 

To configure the actual tool mixing ratio, use the `M567` command. This will tell the firmware to use one stepper motor drive to move more than the other one when handling an extruder move. `M567 Pnnn Emmm:kkk:llll:iii` where `nnn` represents the tool number. And the rest of the letters the tool ratios of the specific extruder drives.  The total of the `mmm, kkk, llll and iii` parameters should add up to 1 in order to produce a normal and expected extrusion flow rate.

## Additional Resources

* [Duet 3D Wiki `M563` ](https://duet3d.dozuki.com/Wiki/Gcode#Section_M563_Define_or_remove_a_tool)
* [Duet 3D Wiki `M567`](https://duet3d.dozuki.com/Wiki/Gcode#Section_M567_Set_tool_mix_ratios) 
* [Duet 3D Wiki `M568`](https://duet3d.dozuki.com/Wiki/Gcode#Section_M568_Turn_off_on_tool_mix_ratios) 





