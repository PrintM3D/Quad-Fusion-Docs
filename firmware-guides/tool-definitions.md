# \*Tool Definitions

This guide will explains the default tool definitions for the Quad Fusion and explains how to change tools. This can be useful to create complex mixing and switching prints. This guide is not for beginners

## Default Tool Definitions

Quad Fusion Tools:

* `T0`: Top Left
  * Extruder Drive 0 
  * Heater 1
* `T1`: Bottom Left
  * Extruder Drive 1
  * Heater 1
* `T2`: Bottom Right
  * Extruder Drive 2
  * Heater 1
* `T3`: Top Right 
  * Extruder Drive 3
  * Heater 1

![](../.gitbook/assets/image%20%2830%29.png)

As seen above, the Crane has four different extruder drives and two heaters. The current configuration is set-up to make all tools heated by Heater 1, while the Bed will be heated by Heater 0.

## Tool Definition Command `M563`

The `M563` command allows you to define a tool, it has the following parameters:

* `Pnnn` : The tool number
* `S"toolname"`: The tool name
* `Dnnn` : The assigned extruder drive
* `Hnnn` : The assigned heater number
* `Fnnn` : The fans mapped to the tool.

The extruder drive numbers start from 0 and immediately follow the X, Y and Z axes stepper motor drives on the Duet Board. You can configure the order of these drives with the `M584` command. If you were looking at your tools in the config.g, they would look like this:

![](../.gitbook/assets/image%20%2824%29.png)

## Defining Your Own Tools

Defining your own tools is useful to create prints that switch colors in the middle of a print. This is more applicable to the compound tool than the K'tana. To define a new tool enter the `M563` command in the configuration file, then follow it with the extruder drive and heater number that you would like to use. Such as:

![](../.gitbook/assets/image%20%289%29.png)

## Mixing Ratios

To enable mixing rations for ta specific tool. Enter the `M568` command with the tool number \(`Pnnn` \) and the enable parameter \(`Snnn` \). For example, if I wanted to enable tool mixing for tool 3 I would enter the command `M568 P3 S1` .

To configure the actual tool mixing ratio, use the `M567` command. This will tell the firmware to use one stepper motor drive to move more than the other one when handling an extruder move. `M567 Pnnn Emmm:kkk:llll:iii` where `nnn` represents the tool number. And the rest of the letters the tool ratios of the specific extruder drives. The total of the `mmm, kkk, llll and iii` parameters should add up to 1 in order to produce a normal and expected extrusion flow rate.

## Additional Resources

* [Duet 3D Wiki `M563` ](https://duet3d.dozuki.com/Wiki/Gcode#Section_M563_Define_or_remove_a_tool)
* [Duet 3D Wiki `M567`](https://duet3d.dozuki.com/Wiki/Gcode#Section_M567_Set_tool_mix_ratios) 
* [Duet 3D Wiki `M568`](https://duet3d.dozuki.com/Wiki/Gcode#Section_M568_Turn_off_on_tool_mix_ratios) 

