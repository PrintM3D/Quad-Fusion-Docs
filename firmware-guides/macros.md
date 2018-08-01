---
description: This page will go over how Macros are used with the QuadFusion.
---

# \*Macros

The QuadFusion has an input of four filaments and the ability to mix those filaments. This ability comes with a need to define the tools you wish to use for certain parts of your print. The purpose of defining these tools is if you have a predetermined ratio of these four filament that will create a desired color. 

The Macros come into play when you want to define these tools. You can create a Macro in the Duet Web Control:  


![](../.gitbook/assets/image%20%288%29.png)

![](../.gitbook/assets/image%20%286%29.png)

Since the QuadFusion can mix any colors that you want, it is recommended that you write your own Macro. This way you can customize the colors mix ratios to suit your preferences. 

The way you create a tool is the same as making one in your config.g \(Check that out in the [Tool Definitions](tool-definitions.md) guide!\)

Type in a `M563` command and add a `M567` command to define the mix ratio you want for this particular tool.

![](../.gitbook/assets/image%20%2823%29.png)



