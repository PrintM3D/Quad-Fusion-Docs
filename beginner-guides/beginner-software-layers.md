---
description: A guide covering the different software layers of the Crane.
---

# \*Beginner: Software Layers

This guide is intended to explain all the different software levels that takes a model to a final printed form on the Crane. We will start at a model on a modelling software on a computer and go all the way down to the RepRap firmware that runs on the Duet Maestro.

## Software Layers

| Layer | Purpose |
| :--- | :--- |
| Model Software | Create _.STL_ models of prints |
| Slicing Software | Convert _.STL_ files to ._gcode_ files while incorporating printer and print settings |
| Duet Web Interface | A web server running on the Duet Maestro that connects to your local network in order to allow for control and monitor of a 3D printer |
| Configuration Settings | G-code files on the microSD card which are loaded upon the boot-up of the Duet board in order to properly configure the board for the printer |
| Firmware | Software running on the Duet Maestro that handles G-code and other operations. Can not be configured. |

## Model Software

If you want to print something on a Crane you will first have to create or find a model of what you plan to print. Creating and designing a model is currently done with CAD \(Computer Aided Design\) software such as SolidWorks or TinkerCAD. SolidWorks offers a more technical and precise solution to designing models, while TinkerCAD represents an easier and faster solution. Aside from creating your own models you can find many models online. These models exist on websites such as [Thingiverse](https://www.thingiverse.com/), [Pinshape,](https://pinshape.com/) [MyMiniFactory](https://www.myminifactory.com/) and many others! In the next step you will see that you need slicing software and slicing software will require a specific file type. That file type is called a ._STL_ file or [stereolithography](https://en.wikipedia.org/wiki/STL_%28file_format%29) file. This file type stores the outside shell of a model, which is typically all the slicer needs. Whenever you design or find a model to print it you will have to convert it to a ._STL_ file in order to slice it.

## Slicing Software

Slicer software fills the void between the model and the 3D printer. The 3D printer can only understand G-code commands and the modeling software can only generate models. Slicer software allows you to convert a model to G-code that will allow a 3D printer to create a print. Incorporated into the slicer software are many different print and printer settings. Print settings refer to the things such as extrusion, cooling and print temperature. Printer settings configure things such as the build volume of the printer or the starting and ending G-code for a print. This software is called a slicer as it typically converts a model into many different layers to print one at a time. The slicing software creates a file type called a _.gcode_ file. This is a long list of commands that can be interpreted by the Duet Board. The G-code commands in this file are exactly the same as the ones you would enter in manually, such as `G1` , but just in a long list.

## Duet Web Interface

To allow control of the Crane you have the Duet Web Console. This is a simple web server that runs on the Duet Maestro and connects to your local network. Aside from control the Duet Web Console allow you to observe various different statistics, status tables and values of the Crane. This allows you to troubleshoot problems much easier with more feedback. You can start and end prints from here. The Duet Web Console also allows you to configure certain settings on the Crane.

## Configuration Settings

The SD card stores files that allow for the operation of the Duet Web Server as well as configure the board, the settings that configure the board can be referred to as the configuration settings. The microSD card has four different folders that each handle a certain part of the Duet board operation \(look in [SD Card Structure](https://m3d.gitbook.io/promega-docs/getting-started/sd-card-structure)\). The SD card files operate on a higher level. The files located in the _sys/_ folder, configure the board. They can be changed by the user at any time, either through the Duet Web Console or by changing the files from your computer. The configuration files often simply represent a grouping of G-code commands that are run upon the boot of the Duet board. Whenever the Duet Board is booted up, it will have no settings loaded. So whenever _config.g_ is run on the start, it gets configured with the settings inside. These configuration files are in the form of G-code files. When you download the SD card file from the M3D Github Repository, you are just taking the M3D preferred settings for the Crane.

## Firmware

The firmware on the board is a version of RepRap released by DC42. The firmware is released on his [GitHub Releases](https://github.com/dc42/RepRapFirmware/releases). If you want to update your firmware, you can follow the [Updating Firmware](https://m3d.gitbook.io/promega-docs/firmware-guides/updating-firmware) guide. The RepRap firmware on the board interprets all the G-code commands sent to the board. It is stored on the micro-processor on the Duet Maestro and required for the board to operate. The firmware handles low-level operation such as controlling the stepper motor drivers or processing G-code commands. Changing the firmware directly is not possible, you will have to update the firmware using the guide above.

The next guide: [What is Slicing?](beginner-what-is-slicing.md) will cover how slicing works and helps you configure your slicer.

