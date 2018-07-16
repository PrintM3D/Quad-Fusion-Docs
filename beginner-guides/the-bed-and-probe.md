# Beginner: The Bed & Probe

The print bed is a very crucial piece on the Promega. When printing on a 3D printer it is important to have an even and level bed relative to your nozzle. This means that your print bed should not have bumps and should be parallel to the plane that the coreXY moves along. This is extremely hard to maintain across a print bed that is almost 400mm x 400mm! When you heat up your heated bed the bed will warp and your print surface will not be level or even. It is important to have a level bed because a 3D printer has to be able to get it's filament to stick to the bed. If the bed is 0.2mm too high the extruder will end up printing in air, and if the bed is 0.2mm too low the nozzle could crash into the bed. So the tolerances are extremely tight! There are multiple things you can do in order to ensure that your bed is as level as possible. First of all you can mechanically level your bed by skipping bed teeth. But this will only get you an accuracy of ~1mm, and that is not enough. Duet Firmware has a bed leveling compensation process that is supported. This is highly recommended for printing large prints! A heated bed is very important to prevent warping of a print and ease first layer adhesion to the build plate. A hot bed can prevent print warping as it keeps the temperature of the first layer at a consistent temperature. A warping print can peel off the heated bed and ruin your print.

## Z-probe Offset

As you might have read previously, the extruder assembly contains two Z-probes. The IR probe, located on the right of the extruder assembly and the Z-probe limit switch on the right side of the extruder. Both of these Z-probes serve the same purpose, zero-ing the Z-axis and leveling the bed. This beginners guide will cover only how to calibrate and use the Z-probe limit switch. **The IR probe is recommended for more advanced users as it tends to be more noisy and inconsistent under the wrong conditions.** The Z-probe limit switch is easier to produce consistent and reliable results with.

**The Limit Switch**

![Z-Probe Deployed \(Left\) and Retracted \(Right\)](../.gitbook/assets/5q6vwqbr3pbij3yk-newzprobe_deployed_not_deployed.jpg)

Z-probes are extremely useful to zero the Z-axis. This is because the Z-probes typically have a reliable and constant offset from the nozzle. Once you find that offset, you run a G-code command in order to ensure that your print will be successful. The limit switch Z-probe is simply an end-stop attached to a deployable 3D printed mount. In the picture above you can see the limit switch in the deployed state on the left and the non-deployed state on the right. Deploy the limit switch by pressing down on the 3D printed tab and retract the probe by pulling the switch up. It is important for the limit switch to be deployable because the limit switch needs to make contact with the bed whenever you are probing, but it should be out of the way whenever you are printing. Whenever you send the probe command `G30` the bed will move up toward the nozzle until the Z-probe is triggered. When the Z-probe is triggered, the Z-value of the printer is set to the Z-offset of the Z-probe. You can set the Z-offset of the Z-probe with the `G31` command and its parameters.

**Always deploy the switch before probing with commands `G30` and `G29`**. This is extremely important, otherwise you **will** crash the nozzle into the print bed as the Z-probe will never be triggered.

**Setting the Limit Switch Offset**

1. Home the printer again, just to ensure you do not crash the printer throughout this process.
2. Print head to the center of the build plate by sending the command `G1 X200 Y200`
3. Heat up the bed to the preferred printing temperature. You can do this by sending the command `M140 Snnn` where `nnn` is your temperature in °C. You can always look up the recommended bed temperatures for specific materials online. For PLA, a bed temperature of 50°C will work well. For ABS-R, a bed temperature of 60°C is recommended. 
4. Wait until the heated bed has reached temperature before continuing.
5. Set the Z-probe offset to 0 by entering the command `G31 P999 X-40 Y28.5 Z0`. This will make it easier to gauge the distance between the Z-probe and the nozzle in the following steps.
6. Run the command `G29 S2`. This clears any active bed leveling compensation. This is **very** important as it will conflict with your updated Z-probe offset and induce a 0.1 - 0.3mm error depending on the magnitude of your bed leveling compensation at that point. This will be explained in the section below.
7. Deploy your Z-probe  ![](../.gitbook/assets/deployingtheprobe%20%284%29.gif) 
8. Check whether the Z-probe is functioning correctly. This is a great step to perform before using your Z-probe in order to prevent crashes. Press your Z-probe limit switch and observe the change in value from 0 to 1000 in the Duet Web Console _Machine Status_ table in the _Z-Probe_ box. If the value does not change the Z-probe is wired or configured wrong, do not continue to the next step!

   ![KWL6DTK3l4pAmrPv-zprobemachinestatus.png](../.gitbook/assets/kwl6dtk3l4pamrpv-zprobemachinestatus.png)

9. Move the bed towards the nozzle by sending the command `G1 Z20`. When you send the command `G30` the bed will move slowly and precisely to the Z-probe, if you send `G30` while the bed is at `Z100` or greater you will have to wait for a long time for the Z-probe to trigger.
10. Run the command `G30`. This will move the bed toward the z-probe until the limit switch triggers. If you don't deploy your limit switch probe, it will never trigger because the bed hits the nozzle. The bed hitting the nozzle is called a crash, if this happens it might misalign your bed and you will have to follow a separate guide to fix the problem.
11. Now your Z0 is set to your Z-probe limit switches trigger height. This is because the Z-probe limit switch offset is 0mm. Now that we have set our Z0 to the trigger height we can move the bed toward the nozzle in order to find the distance between the trigger height of the Z-probe and the nozzle!
12. Retract the Z-probe.
13. Jog the bed up slowly toward the nozzle using the negative Z buttons in _Machine Control_ on the Duet Web Console. Read the next step!

    ![Z81QrJdADnqOrI0d-MachineControl.PNG](../.gitbook/assets/z81qrjdadnqori0d-machinecontrol.PNG)

14. As you are moving the bed up towards the nozzle you will encounter an axis limit. These axes limits are set for the X, Y and Z axes and will stop you from moving past a certain coordinate. This will make it harder to crash the printer. However, in this case we know what we are doing so we can disable the axes limits. Send the command `M564 S0` to disable the axis limits. To learn more about this command visit the [RepRap G-code wiki](https://reprap.org/wiki/G-code#M564:_Limit_axes).
15. **Be careful when moving the bed close to the nozzle. Use the 1mm and 0.1mm buttons.** Determining when the bed is touching the nozzle can be difficult. You might have to heat up the nozzle as you learned before in order to ensure that none of the filament from the hot-end gets in the way. Using a piece of paper to determine when the nozzle is touching the bed is also helpful. Grab a sticky-note or small piece of paper and place it under the nozzle. Then carefully jog the bed into the nozzle, move the paper back and forth. When you feel the nozzle grab the paper your nozzle is touching the bed!. 
16. Record the Z-value that the printer is currently displaying in _Machine Status_. The absolute \(non-negative\) of this value is your Z-probe offset. It might be a good idea to write down this value.
17. Enter the command `G31 P999 X-40 Y28.5 Znnn` where `nnn` is your Z-probe offset.
18. Reinstate your axes limits with the command `M564 S1` . This will prevent you from crossing the axes limits again.
19. Move the bed away from the nozzle `G1 Z20`.
20. Deploy your Z-probe!  ![](../.gitbook/assets/deployingtheprobe.gif) 
21. Send the command `G30`.
22. Move the bed back up to the nozzle as described in the steps above. Your Z value should be 0 when the bed is touching the nozzle. If it is not you might need to tune the Z-probe offset or repeat the process.
23. In order for these changes to take effect permanently, you will have to open up your _machine\_zprobe.g_ file and update the Z-offset of the `G31` command there, just like you did in the . Follow the steps below to make this change.
24. Whenever you power your printer on and off, it will wipe all commands previously entered on the board. Whenever you start the Duet board, it will run a file called _config.g._ This file contains all kinds of different commands and settings that it has to load on start-up in order to work. You want your `G31` command with your offset to be added to this start-up sequence. This will prevent you from having to follow the steps above continuously. 
25. Go to the _System Editor_ in the _Settings_ tab on the Duet Web Console and open the _machine\_zprobe.g_ file and find the `G31` commands. You will note that there are two of them.
26. One of the commands will have a `;` in front. This denotes a comment, and thus that command will not take effect when the file is run. One of the `G31` commands configures the offsets for the IR Z-probe and the other for the limit switch Z-probe. The comments should indicate which one is what. Fix the Z-probe Z-offset of the limit switch. Your `G31` command might look like the command below \(`nnn` represents your Z-probe Z-offset,  \):  `G31 P999 X-43 Y25 Znnn ; Set Z probe (limit switch) trigger value, offset`

**Your Z-probe offset will not change unless you make changes that can affect the distance between your Z-probe trigger height and your nozzle such as crashing the bed, or changing your Z-probe mount.**

## Bed Leveling

As mentioned at the beginning of this article, bed leveling on the Promega is very important to be able to print large first layers properly. This would be difficult to do without proper bed leveling compensation. Follow the steps below to enable bed leveling.

1. These steps assume you have properly homed your printer, if you have not done so, please do so now.
2. These steps also assume you have properly set your Z-probe height with the steps above. If you have not done so now, please do so.
3. Heat up the bed to your printing temperature. If you are not yet familiar with different 3D printing materials and their bed temperature preferences, 60°C is a good starting point. 
4. Wait for the bed to reach temperature. This could take a few minutes as the heat disperses over the bed. Remember that you can see the bed approach temperature in the Duet Web Console on the graph and in the table.  ![](../.gitbook/assets/settingbedtemperature.png) 
5. When the bed has reached temperature, deploy the Z-probe. ![](../.gitbook/assets/deployingtheprobe%20%283%29.gif)
6. Send the command `G29 S2` , this will disable any current bed leveling compensation.
7. Send the command `G29` , this will engage the bed leveling process. The extruder carriage will move over the entire build plate and probe bed. This can take a few minutes, so continue on to the next step where I explain what bed leveling does.
8. The bed leveling procedure will carefully probe each location on the bed once in a grid pattern. This pattern is configurable and is defined in _machine\_bedmesh.g._ The pattern is defined in that file with the `M557` command. Check it out on the [RepRap wiki](https://reprap.org/wiki/G-code#M557:_Set_Z_probe_point_or_define_probing_grid) for more information. It shouldn't need to change, but you can reduce it if you want to sacrifice accuracy for a shorter wait time. The bed leveling procedure will generate a heightmap file called _heightmap.csv_ on the SD card_._ This file stores the data for the bed leveling compensation. Whenever the bed leveling procedure finishes, you will see this heightmap file visualized on the screen. If you ever want to see the heightmap again in the future you can select _Show Mesh Grid Heightmap_ in the _Auto Bed Compensation_ tab of the _Machine Control_ tab on the Duet Web Console \(shown in the image below\). ![](../.gitbook/assets/showmeshgridheightmap.png)  Whenever you enable mesh bed leveling compensation, your Z-height will be adjusted based on the values in the heightmap. So when the Duet is printing a file and gives the command to go to `G1 Z0.2` for the first layer, it will be compensated for by the local and interpolated value obtained from the heightmap. So the board might actually go to `Z-0.3` depending on the local heightmap value. 
9. When the bed leveling procedure completes it will display the heightmap as mentioned in the previous step. In the pictures below, the heightmap on the left is average and the heightmap on the right is good \(Courtesy of @Talrynn\(John\) on M3D's Discord Server\). Based on this heightmap display you can tune your bed to become flatter. But whatever bed you have, automatic bed compensation will try and compensate for whatever error you have.  ![](../.gitbook/assets/heightmapvisual%20%281%29.PNG) ![](../.gitbook/assets/goodheightmapvisual.png) 
10. Once bed leveling completes it will automatically enable. If you ever want to disable bed leveling enter the command `G29 S2` , if you want to re-enable bed leveling without running the bed leveling procedure, send the command `G29 S1` . 
11. Just like with the Z-probe offset, you should never have to change your heightmap unless you have a mechanical change to it. If you skip a belt or crash your printer, it is recommended you create a new heightmap. Running `G29` again will overwrite the previous heightmap. 

## The Conflicts of Mesh Bed Leveling

Mesh bed leveling can affect the value of any Z-axis constant you find. To avoid this, it is the best practice to disable bed leveling with `G29 S2` in order to avoid the propagation of heightmap values. Things that can be affected:

* The Z-probe offset
* The Z-endstop homing value offset
* Another heightmap

If you tried to find the Z-probe offset of the Z-probe with mesh bed leveling compensation enabled, the Duet board will add the heightmap compensation on top of what you think is 0. So, when the bed is touching the nozzle in one of the steps above, and the _Machine Status_ tab displays a value of -9.4. Due to a local heightmap compensation value, the actual value might be -9.2. But you would have no way of knowing this. Therefore, it is important to disable the bed leveling compensation. RepRap firmware already has a few safeguards in place to prevent conflicts such as these when running `G29` multiple times in succession, but these are known to have bus. We recommend running `G29 S2` before doing any of the actions in the list above. **If you forget to disable mesh bed leveling, you will not have catastrophic results, just an error of around 0.5mm or so. Just barely enough to mess up your print.**



