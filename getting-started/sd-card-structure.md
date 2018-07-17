---
description: An explanation of the SD card files.
---

# SD Card Structure

One of the first steps of setting up your printer is getting access to and understanding the files stored on the microSD card. This guide will cover the basic structure of the files on the SD card. Follow the [Accessing Your SD Card](https://m3d.gitbook.io/promega-docs/getting-started/accessing-your-sd-card) guide for more assistance on how to get to the files located on the microSD card.

## File Structure

On the microSD card there are four different folders: _gcodes_, _macros_, _sys_ and _www_. These folders contain all the information the Duet board needs to operate properly. Below is a list of the folders and their purpose.

* _**gcodes**_: This folder contains _.gcode_ files that can be run by the Duet. If you upload print files through the Duet Web Console or via a microSD card they should be placed in this folder.
* _**macros**_: Any macro files that you create should be located in this folder. Macros are _.gcode_ files that can be executed to perform a repetetive task more quickly.
* _**sys**_: Configuration files of the printer. Contains important _.gcode_ files such as _config.g_ which are executed on startup. You will need to change files in this folder regularly.
* _**www**_: Holds all files necessary for the operation of the Duet Web Console. It is recommended not to mess with the files here unless you are familiar with web development.

## Sys Organization

As mentioned before, the _sys/_ folder contains all sorts of system files. The most important file is _config.g_. This file is executed on the start-up of the Duet Maestro board in order to configure the Promega settings. If you wanted to add a command to the start-up sequence, you should insert it in _config.g_. In the _sys/_ folder you will also notice a handful of other files with the _machine_ prefix. These files are called from _config.g_ with the `M98` command and they represent part of the start-up sequence. The _sys/_ folder is structured to indicate which files are recommended to be changed and which are not.

**Machine Files**

Below is a list of files with the _machine_ prefix. **This prefix indicates that they should be opened and can be changed to your preferences**.

* _A Instructions.txt:_ This file contains a further explanation and instructions of the files on the SD card.
* _machine\_access.g_: This file contains G-code commands to properly setup the network settings. Open and change this file in order to allow the Duet Maestro to connect to your local network. Follow the [Network Setup](https://m3d.gitbook.io/promega-docs/getting-started/network-setup) guide in order to setup your network.
* _machine\_axisdimensions.g_: This file contains G-code commands to initialize the minimum and the maximum values of the coordinate axes. Change the values in this file in order to allow your gantry to move to the absolute limits of your buildspace. Use caution when changing the axes limits.
* _machine\_axissteps.g_: The axis steps per millimeter for the stepper motors are placed here. Changing these values should not be necessary as they are already properly configured.
* _machine\_bedmesh.g_: This file initializes the bed leveling mesh.
* _machine\_extruderstep.g_: Configure your extruder steps per millimeter here.
* _machine\_maxtemp.g_: Change the maximum temperature of your extruder in this file.
* _machine\_steppercurrent.g_: The stepper motor current is configured here. Changing stepper motor current is not without risk, riasing the current too high can cause damage to the stepper motors and the printer.
* _machine\_stepperspeed.g_: Contains the maximum speed, acceleration and jerk settings of the printer.
* _machine\_zendstop.g_: Change the offset of the Z-endstop on the bottom printer. This file must be manually configured for each printer depending on the printers configuration.
* _machine\_zprobe.g_: Change the Z-probe settings here. This file allows you to select the IR or limit switch probe and configure the offsets of the probes.

## **Other Files**

In the _sys_ folder you will find many other files which handle other important aspects of the printer. Observe the list below for an explanation of the different files.

* _config.g_: This file is called upon the boot-up of the Duet board. Place G-code commands here in order for them to be executed on start-up. This file calls multiple machine files listed above with the `M98` command.
* _homex.g_, _homey.g_, _homez.g_ and _homeall.g_: These files operate the homing procedure. Follow [Homing the Printer](https://m3d.gitbook.io/promega-docs/getting-started/homing-the-printer) for more help on homing the printer, and [Adjusting Homing Macros](https://m3d.gitbook.io/promega-docs/firmware-guides/adjusting-homing-macros) in order to adjust the homing macros.

Continue on to the [Homing the Printer](https://m3d.gitbook.io/promega-docs/getting-started/homing-the-printer), the next chapter in the [Getting Started](https://m3d.gitbook.io/promega-docs/getting-started) guide.

