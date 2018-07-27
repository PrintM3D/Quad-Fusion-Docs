---
description: Setting up your control board to operate the QuadFusion 3D Print Head
---

# Updating your Control Board Settings

The QuadFusion requires printer electronics capable of running four independent extruder motor channels, either natively via the printer's control board or with an attached expansion board.

If you are running your QuadFusion from a Duet 2 Maestro plus Extruder Expansion Board, configuration files are available for several printers on which we've tested the QuadFusion.  These files can be found in [GitHub](https://github.com/PrintM3D/QuadFusion).  Be careful when first using these files!  While they have common settings for printer geometry, end stops, etc. these settings may not correspond to your printer exactly, and using the files without reviewing the settings could damage your printer or the QuadFusion head.  For a walk through on adjusting necessary settings before running your printer, see our [Firmware Guides](https://quadfusion.printm3d.com/firmware-guides).

If you are setting up a Duet 2 Maestro manually or running your QuadFusion from alternate electronics, here are the basics of the QuadFusion design you'll need to get up and running:

* Motor current: 500 mA peak The motors are designed for the best combination of extrusion force and thermal performance when operating in the range 480 - 525 mA.  We suggest setting your extruder motor current \(all four channels!\) at 500 mA as a starting point.  Do not run your motors above 525 mA as they will self-heat and can cause damage to themselves or the rest of your printer. 
* Extruder steps per millimeter: 984 microsteps/mm at a microstep setting of 8x We recommend getting started at 8x microstepping.  Higher microstepping can offer some benefits to print quality when mixing at disparate ratios, but may present difficulty for control boards with low maximum step rates.  For more information on the step rates achievable on various electronics, see [this article](https://reprap.org/wiki/Step_rates) on the RepRap wiki. 
* Temperature sensor: PT1000, resistance at room temperature is 1050 Ω In addition, if you are setting up the QuadFusion on a Duet 2 Maestro, note that the series resistance \(of voltage divider feeding the chip's ADC for temperature reading purposes\) is 2200 Ω.





