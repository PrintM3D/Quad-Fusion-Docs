---
description: A guide to calibration of the Z-probe and bed leveling.
---

# Z-Probe Calibration & Bed Leveling

This guide will walk you through setting the Z-offset of a Z-probe sensor. This is necessary in order to allow you to probe the bed accurately. The Promega comes equipped with two different Z-probes, the limit switch and the IR probe. This guide can be followed to configure either one. Whenever you home the printer, the current Z-value of the printer is set based on the limit switch on the bottom of the printer. Whenever you "probe" the bed, meaning you touch the bed against the limit switch probe on the extruder or the IR probe on the extruder, the Z-value will now be based on that probe move. However, in order to do this accurately, you will have to configure the distance between the nozzle and the trigger height of the Z-probe. This is because the firmware will set the Z-value of the printer to the Z-probe offset, as configured in this guide, whenever the Z-probe is triggered during a probe move. 

## Calibrating the Limit Switch

To find out the z-offset of the limit switch to the nozzle, follow the steps below. 

1. Home the printer again, just to ensure you do not stall the printer throughout this process. 
2. Print head to the center of the build plate by sending the command `G1 X200 Y200` 
3. Heat up the bed to the preferred printing temperature. You can do this by sending the command `M140 Snnn` where `nnn` is your temperature in °C. You can always look up the recommended bed temperatures for specific materials online. For PLA, a bed temperature of 50°C will work well. For ABS-R, a bed temperature of 60°C is recommended. 
4. Wait until the heated bed has reached temperature before continuing. 
5. Set the Z-probe offset to 0 by entering the command `G31 P999 X-40 Y28.5 Z0`. This will make it easier to gauge the distance between the Z-probe and the nozzle in the following steps. 
6. Run the command `G29 S2`. This clears any active bed leveling compensation. This is **very** important as it will conflict with your updated Z-probe offset and induce a 0.1 - 0.3mm error depending on the magnitude of your bed leveling compensation at that point. 
7. Deploy your Z-probe!  ![](../.gitbook/assets/deployingtheprobe%20%282%29.gif) 
8. Check whether the Z-probe is functioning correctly. This is a great step to perform before using your Z-probe in order to prevent crashes. Press your Z-probe limit switch and observe the change in value from 0 to 1000 in the Duet Web Console _Machine Status_ table in the _Z-Probe_ box. If the value does not change the Z-probe is wired or configured wrong, do not continue to the next step!  ![](../.gitbook/assets/zprobemachinestatus.png) 
9. Move the bed towards the nozzle by sending the command `G1 Z20`. When you send the command `G30` the bed will move slowly and precisely to the Z-probe, if you send `G30` while the bed is at `Z100` or greater you will have to wait for a long time for the Z-probe to trigger.
10. Run the command `G30`. This will move the bed toward the z-probe until the limit switch triggers.
11. Now your Z0 is set to your Z-probe limit switches trigger height. This means that if you go to Z0 with the command `G1 Z0` it will send the bed to the trigger height of the limit switch. This is because the Z-probe limit switch offset is 0mm, and the firmware sets the Z-height of the printer to the Z-probe offset whenever the probe is triggered during the probe move.
12. Now that we have set our Z0 to the trigger height we can move the bed toward the nozzle in order to find the distance between the trigger height of the Z-probe and the nozzle!
13. Retract the Z-probe.
14. Jog the bed up slowly toward the nozzle using the negative Z buttons in _Machine Control_ on the Duet Web Console. Read the next step!

    ![Z81QrJdADnqOrI0d-MachineControl.PNG](../.gitbook/assets/z81qrjdadnqori0d-machinecontrol%20%282%29.PNG)

15. As you are moving the bed up towards the nozzle you will encounter an axis limit. These axes limits are set for the X, Y and Z axes and will stop you from moving past a certain coordinate. This will make it harder to stall the printer. However, in this case we know what we are doing so we can disable the axes limits. Send the command `M564 S0` to disable the axis limits. To learn more about this command visit the [RepRap G-code wiki](https://reprap.org/wiki/G-code#M564:_Limit_axes).
16. **Be careful when moving the bed close to the nozzle. Use the 0.1mm buttons.** Determining when the bed is touching the nozzle can be difficult. Heat up the nozzle as you learned before in order to ensure that none of the filament from the hot-end gets in the way. Using a piece of paper to determine when the nozzle is touching the bed is also helpful. Grab a sticky-note or small piece of paper and place it under the nozzle. Then carefully jog the bed into the nozzle, move the paper back and forth. When you feel the nozzle grab the paper your nozzle is touching the bed!. 
17. Record the Z-value that the printer is currently displaying in _Machine Status_. The absolute \(non-negative\) of this value is your Z-probe offset. It might be a good idea to write down this value.
18. Enter the command `G31 P999 X-40 Y28.5 Znnn` where `nnn` is your Z-probe offset.
19. Enter the command `M564 S1` in order to re-enable your axes limits.
20. Move the bed away from the nozzle `G1 Z20`.
21. Deploy your Z-probe!  ![](../.gitbook/assets/deployingtheprobe%20%281%29.gif) 
22. Send the command `G30`.
23. Move the bed back up to the nozzle as described in the steps above. Your Z value should be 0 when the bed is touching the nozzle. If it is not you might need to tune the Z-probe offset or repeat the process.
24. In order for these changes to take effect permanently, you will have to open up your _config.g_ file and update the Z-offset of this command there. If you have the newer version of the SD card, you will have to find _machine\_zprobe.g_ and open that instead.
25. Find the un-commented `G31` command and change the `Z` parameter value to the value you just found.
26. Save the file, now if you reboot your Duet the Z-probe offset will be saved. If you ever make a mechanical change to the printer, skip the bed and so on, you will have to recalibrate your Z-probe following the steps above.

## Automatic Bed Leveling Compensation

To accommodate for small discrepancies in the bed level of the Promega, you can enable bed leveling with `G29` , however, this command will require a _heightmap.csv_ file. Each _heightmap.csv_ file will be unique to your Promega, and sometime even unique to a specific time. If you stall your printer or otherwise misalign your bed, you will have to re-run mesh bed leveling. Bed leveling compensation can compensate for about 2mm of error. If your error is greater, follow the [mechanical leveling guide](../repair-guides/repairing-broken-belt-clamps.md#leveling-the-bed) via skipping. Follow the steps below to generate a _heightmap.csv_ file and enable bed leveling compensation. 

1. Home the printer if you have not already done so.
2. Heat up the print bed to your preferred printing temperature. The Promega's bed will warp differently depending on what temperature it is heated up to.
3. Wait until the bed has reached its temperature before continuing. This could take a few minutes.
4. Deploy the Z-probe.
5. Send the command `G29` , this will start the mesh bed leveling process. The mesh is defined in the configuration files on the SD card, and should not need to be changed.
6. Wait for the mesh probing to complete. This could take a while as it probes over 100 points on the bed.
7. Once the leveling completes, it will generate the _heightmap.csv_ file in the _sys/_ folder on the microSD card. It will also display the heightmap on the Duet Web Console. This is a great tool to observe and visualize any error in the levelness of your bed. Remember that this graph is inflated **massively** and represents a 400mm by 400mm area**.** A height difference of  ± 1mm between the corners of the print bed is expected. Below you can see heightmaps. The one on the left is a normal heightmap, the one on the right is a good heightmap \(courtesy of @talrynn\(John\) on discord\). With mesh bed leveling compensation, there should be no difference in print quality or ability.  ![](../.gitbook/assets/heightmapvisual.PNG) ![](../.gitbook/assets/goodheightmapvisual%20%281%29.png) 
8. Bed leveling compensation will be automatically enabled once bed leveling completes. It is important to **remember to disable bed leveling compensation whenever you are finding constants and offsets on the Z axis**. Otherwise the bed leveling compensation will conflict with the offset you obtain. If you want to disable bed leveling compensation send the command `G29 S2` , to enable bed leveling compensation after disabling it, send the command `G29 S1`

Continue on to the [Preparing a Print](https://m3d.gitbook.io/promega-docs/getting-started/preparing-a-print) guide, the next chapter in the [Getting Started](https://m3d.gitbook.io/promega-docs/getting-started) guide.

