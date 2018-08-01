# \*Filament Extrusion Rate

The extrusion system on the QuadFusion is designed to print at specific speeds at certain temperatures. Printing at the proper filament extrusion rate is essential to provide a good print. The QuadFusion is designed to extrude at a rate of 5.7 mm^3/s. This number can change significantly depending on your printer and slicer settings and material.

## Calculating Filament Flow Rate

Calculating the flow rate of your extruder is typically very easy. The equations you can use to calculate filament flow rate depends on your print settings and whether you are printing or not. Follow the _Extruding in Air_ section to calculate the flow rate while extruding filament in the air and the _Printing Flow Rate_ section in order to find the filament flow rate while printing.

### Extruding in Air

When the extruder is printing filament into air, we can assume that the extruder is creating a steady stream of filament at a slightly larger diameter than the diameter of the nozzle. If the extruder is not skipping, you can use the feedrate of the extruder move and the cross-section of the filament to calculate the flow rate. Because, all the filament that is being pushed by the extruder is pushed through the nozzle. Follow the equation below:

_Flow Rate \(mm^3/s\) = Feedrate \(mm/s\)_ \(Filament Cross-section\) \(mm^2\)\*

_Filament Cross-section = pi_ \(\(Filament Diameter\) / 2\)^2 \_\_Filament Cross-section for 1.75mm filament: 2.405 mm^2\*

**For Example:** You send the command `G1 E100 F200`, where you extrude 100mm of filament at 200 mm/min. You are using 1.75 mm filament.

_Flow Rate = 8 mm/s = pi_ \(1.75 / 2\)^2 _\(200 / 60\) = 2.405_ 3.333\*

Remember that the `G1` move command feedrate parameter, `F`, uses mm per minute. So divide the feedrate by 60 to obtain the feedrate in mm per second.

### Printing Flow Rate

When printing, the flow rate depends on your layer height, nozzle diameter and print speed.

_Flow Rate \(mm^3/s\) = \(Extrusion Width\)\(mm\)_ \(Layer Height\)\(mm\) _Print Speed \(mm/s\)_ _Extrusion Width is ~120% of nozzle diameter_

**For Example:** You have a 0.5 mm nozzle mounted and you are printing at 0.25mm layer height at a print speed of 30 mm/s.

_Extrusion Width = 0.6 mm = 1.2_ 0.5 _Flow Rate = 4.5 mm^3/s = 0.6_ 0.25 \* 30

## QuadFusion Flow Rate

The QuadFusion is designed to extrude filament at 5.7 mm^3/s. If you find your extruder skipping or notice print quality problems, do a filament flow calculation to determine the extrusion rate you are printing at. The extrusion rate of the QuadFusion can be increased significantly depending on material, printing temperature and other factors. Feel free to experiment and push the extruder to its limits! But remember to calculate the filament flow rate to determine whether your goal is realistic.

