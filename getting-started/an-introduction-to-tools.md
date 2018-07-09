# An Introduction to Tools

The Duet Web Console includes a tool system. Tools allow you to quickly change between different extruder configurations. For example, if you were printing with your right K'Tana nozzle but wanted to start printing with your left K'Tana nozzle, you can change tools. The default SD configurations released by M3D on the [Promega GitHub repository](https://github.com/PrintM3D/Promega) enable a number of tools depending on your mounted extruder head \(K'tana or Compound\). The guide below includes an introduction to tools and how to use them.

### What are tools?

A tool is a defined extruder setup. A tool will be configurated to use a specific extruder motor or motors at specific speeds. If you are printing with the compound hotend, you will have a tool that allows for mixing 50% on each side as well as two tools that extrude with only one extruder \(left and right\). If you perform the correct setup in your slicer, you can switch between these tools while printing. In order to switch between tools you can enter the command `Tnnn`, where `nnn` is the tool number. If you wanted to switch to tool 1, you can enter the command `T1` in the G-code Console. The tools can be viewed in the top right corner of the Duet Web Console. An underline will indicate which tool is currently selected.

> Before you can start heating up a hotend you will have to select the appropriate tool. Read the _Tools and Temperature_ section below for more information.

### Default Tools

#### K'Tana Tools

The K'Tana extruder head features two different filament inputs and outputs. This allows you to print with two different materials and switch while printing. This allows for some really neat and complicated prints. Below is a list of the predefined tools 1. Tool 0: "Ktana Single Right": Uses just the right extruder to print 2. Tool 1: "Ktana Single Left": Uses just the left extruder to print

#### Compound Tools

The compound extruder allows you to mix two different filaments coming in. There are three different default tools for the mixing configuration. 1. Tool 0: "Mixing": A Tool that prints with both extruders at a 1:1 ratio. 2. Tool 1: "Mixing as Single Right": A tool that prints with just the right extruder. 3. Tool 2: "Mixing as Single Left": A tool that prints with just the left extruder.

### Tools & Temperature

The temperature table on the Duet Web Console includes textfields for both Active and Standby temperatures of the extruder. The active temperature represents the temperature, in degrees Celsius, that the tool will go to when it is selected. **If no tool is selected, no nozzle will heat up**. This is the case whenever a print is cancelled. The firmware will deselect all tools. To gain temperature control again, select your desired tool. The standby temperature is the temperature the tool will go to when it is not selected, but was previously selected. This is useful for printing with the K'tana to avoid long heat-up times in between filament switches or collisions with the print.

> Currently there is a bug in RepRap firmware with extruder movement. The feedrate of a 50/50 mixing extrude only move will extrude sqrt\(2\) slower than the given `F` parameter.

Continue on to the [Important G-Code Commands](http://promega.printm3d.com/books/user-manual/page/important-g-code-commands-394), the next chapter in the [Getting Started](http://promega.printm3d.com/books/user-manual/chapter/getting-started) guide.

