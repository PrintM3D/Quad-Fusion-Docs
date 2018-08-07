---
description: Beginner guide focusing on moving the motors.
---

# Beginner: Moving the Motors

Before you power on your motors you can manually move the extruder head around the printer. Follow the steps below in order to start moving the printer.

1. Move the extruder head to the center of the printer by hand. This should not take a lot of effort to do as long as the motors are not powered. Once you move the motors, the motors will be powered and resist any force acted on them.
2. Go to the _Machine Control_ tab of the Duet Web Console.

![Machine Control Tab in Duet Web Console](../.gitbook/assets/z81qrjdadnqori0d-machinecontrol-1.PNG)

1. Press _Home All_, this will home all the axes of the printer and ensure that the origin of the printer is located at the front-left corner of the 3D printer. After the homing process is complete, you can see that the position of the 3D printer is updated in the _Machine Status_ tab on the Duet Web Console.
2. Press the X-10 button in the _Head Movement_ window. This will move the extruder carriage of the printer 10mm in the negative X direction, this should be towards the left if you are facing the front of the printer. Now press the Y-10 button, this will move the printer -10 mm in the Y-direction. If you are facing the front of the printer, this should send the bed carriage away you.  Press the Z-10 button in order to move the extruder down 10 mm.
3. You can keep pressing the buttons to move the extruder carriage to become more familiar with the directions and coordinate system of the Crane.

**Absolute vs. Relative**

A 3D printer movement allows for two different modes, absolute and relative. These two terms are also used frequently in machining and other engineering processes. Absolute describes a position or command with respect to the origin or zero position. Remember that for the Crane the origin is located in the top-left-front corner. Relative describes the position of a 3D printer relative to the previous point the printer was located at. For example, if you tell the printer to move \(20,20,20\). Absolute mode will send the printer to the point where X = 20mm, Y = 20mm and Z = 20mm, relative to the origin. While relative will send the printer 20 mm in the X-direction, Y-direction and Z-direction relative to its previous position. This means your printer will go to two completely different places depending on if you are in relative or absolute mode.

If you were to tell the printer to go to \(20,20,20\) while the printer was in absolute mode, it would result in the printer first moving to \(20,20,20\). If you told it again to go to \(20,20,20\) it would just stay there. The Duet would say: I am already there! If you told the printer to move \(20,20,20\) twice while the printer was in relative mode. The printer would move 20mm in the X, Y and Z directions the first time. And then move 20mm in the X, Y and Z directions for the second time as well. This is the difference between absolute and relative.

