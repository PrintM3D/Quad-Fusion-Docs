---
description: This page will go over how Macros are used with the QuadFusion.
---

# \*Macros

The QuadFusion has an input of four filaments and the ability to mix those filaments. This ability comes with a need to define the tools you wish to use for certain parts of your print. The purpose of defining these tools is if you have a predetermined ratio of these four filament that will create a desired color. 

The Macros come into play when you want to define these tools. You can create a Macro in the Duet Web Control:  


![](../.gitbook/assets/image%20%289%29.png)

![](../.gitbook/assets/image%20%287%29.png)

Since the QuadFusion can mix any colors that you want, it is recommended that you write your own Macro. This way you can customize the colors mix ratios to suit your preferences. 

The way you create a tool is the same as making one in your config.g \(Check that out in the [Tool Definitions](tool-definitions.md) guide!\)

Type in a `M563` command and add a `M567` command to define the mix ratio you want for this particular tool.

![This example is of a Brick Tile ](../.gitbook/assets/image%20%2839%29.png)

Now that you have a new Macro filled with all the tools for a specific print, you can now use it! 

You should now see your newly made Macro listed in the Macro section. 

![](../.gitbook/assets/image%20%2842%29.png)

If you click your Macro's title it will be enabled.

![](../.gitbook/assets/image%20%2817%29.png)

Enable the Macro you have created. You should now see that your tool settings have changed to suit the Macro you have just enabled. 

If you wish to test to see if your Macro is enabled, go to the Gcode Command section and type in:  
`M567 P0`

![](../.gitbook/assets/image%20%2831%29.png)

Now you will be able to see the mix ratio you have designated Tool 0 to have

The purpose of doing this is if you have a specific print that requires different colors with specific tools, you can create these tools in a Macro and when you're printing the printer will have the proper tools with the proper mix ratios. 

