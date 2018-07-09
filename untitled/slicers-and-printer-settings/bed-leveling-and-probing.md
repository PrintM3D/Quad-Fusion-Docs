# Bed Leveling & Probing



This page serves as an indepth guide to bed leveling. A good bed level will allow you to print a consistent first layer across the entire bed.

### Z-Probes

The Promega is equipped with two different Z-probes, an IR \(infra-red\) probe and a deployable endstop limitswitch. The default config.g file is set up to use the limit switch. This section covers the two different probes, their settings and how to use them. We recommend using the limit switch for less experienced users as it has proven to be more robust under many different circumstances.

#### Probing Commands

* `G30`: Commands the printer to perform a single z-probe. The z-height of your printer will then be set to the Z-offset as defined in `G31`. Sending `G30 S-1` will cause the printer to perform a z-probe and print the trigger height but will not change the z-height of the printer, this can be used to find probe offset.
* `G31`: Sets the z-probe status and offset, this changes depending on which probe you wish to use.
* `M558`: Defines the z-probe type.
* `G29`: Executes bed leveling as defined by `M557`
* `M557 Pnnn Xmmm Ylll`: Defines the pattern that will be probed when `G29` is sent. `nnn` represents the point number if you wish to perform single point probing. A better option is to define a mesh with `Xnnn:mmm`, `Ylll:kkk` and `Sjjj`. Where `nnn` and `lll` are the minimum values for each axis and `mmm` and `kkk` are the maximum values. `jjj` represents the interval over the area you just defined. A working `M557` command for the Promega is: `M557 X50:370 Y10:350 S30`.
* `G32` will execute the _bed.g_ file located in _sys/_ on the microSD card.

#### The Limit Switch Probe

> Warning: This limit switch is manually deployable. Remember to put the limit switch on the mount prior to probing, and remove the limit switch prior to printing or moving the bed to the nozzle.

**Mounting the Limit Switch Probe**

1. When mounted, the limit switch magnet should be firmly attached to the bottom of the mount as shown in the picture below.

   ![BlabOuIBSjcY3Gkg-zlimitmount.png](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/BlabOuIBSjcY3Gkg-zlimitmount.png)

2. Connect to the Duet Web Console. In the _Machine Status_ table observe the Z-probe cell. Press the Z-probe switch and you should see this value change from 0 to 1000. If this is not happening, it indicates a problem with the wiring of the limit switch. Stop and fix the wiring before continuing with this guide.
3. In order to unmount the limit switch simply remove it from its mount and stick it above the nozzle. Stick the limit switch against the metal mount so that the limit switch is pressed down. Now if you accidentally send the command `G30` with an unmounted z-probe, you will get an error: _"Error: Probe already triggered during move_" instead of a crash of the bed against the nozzle.

   ![EJqnEtlnpFIpXnQb-Unmountedswitch.jpg](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/EJqnEtlnpFIpXnQb-Unmountedswitch.jpg)

**Limit Switch Configuration Settings**

In the _config.g_ configuration file you can set certain properties of the Z-limit switch. The commands `M558` and `G31` are the most important here. If you wish to enable the limit switch as your z-probe you have to enter the following commands into your _config.g_ file:

```text
    M558 P4 I1 X0 Y0 Z1 H5 F100 T5000 ; Set Z probe type -- SET AS LIMIT SWITCH
    G31 P999 X40 Y-28.5 Z5.8 ; Set Z probe (limit switch) trigger value, offset
```

These two commands enable and configure the Duet board z-probe. Remember that you must comment all other M558 and G31 commands in order for these commands to take effect. If you enter these commands in the configuration file and then enter the same commands for the IR probe 10 lines below, the board will be configured to use the IR board.

The `M558` command above sets the Z-probe type.

* The `P4` parameter informs the firmware that the z-probe is a switch that is connected to the E0 endstop detection port. 
* `I1` inverts the reading on this port, the switch is wired as normally closed and therefore always outputs a value of 1000. 
* `X0 Y0 Z1` ensures that this limit switch is only used for homing the z-axis. Any non-zero value will enable homing on that axis. 
* `H5` sets the dive height of the probe. This defines the distance in mm that the probe will move after contact.
* `F100` is the feedrate of the homed axis. Reduce this value to slow down the bed more as it moves to make contact with the limit switch.
* `T5000` is the travel speed between probe points.

The G31 command sets certain z-probe settings such as offset and trigger height.

* `P999` sets the trigger value to 999. Whenever the z-probe trigger value is reached the board will register a detection. For the limit switch this value should not need to change.
* `X40 Y-28.5 Z5.8` Represents the offset of the z-probe to the nozzle, this value changes depending on which extruder you have mounted. If you have the K'Tana, the offsets of the z-probe to the nozzle are going to be different than the compound nozzle. It is also worth noting that the offset for the K'Tana nozzle is based on the right nozzle. The Z-offset to the z-limit switch varies per printer. We recommend that you tune your z-probe Z offset before printing. Follow the section below for calibrating the Z-offset of the limit switch.

**Calibrating the Limit Switch**

To find out the z-offset of the limit switch to the nozzle, follow the steps below. 1. Home the printer again, just to ensure you do not crash the printer throughout this process. 2. Print head to the center of the build plate by sending the command `G1 X200 Y200` 3. Heat up the bed to the preferred printing temperature. You can do this by sending the command `M140 Snnn` where `nnn` is your temperature in °C. You can always look up the recommended bed temperatures for specific materials online. For PLA, a bed temperature of 50°C will work well. For ABS-R, a bed temperature of 60°C is recommended. 4. Wait until the heated bed has reached temperature before continuing. 5. Set the Z-probe offset to 0 by entering the command `G31 G31 P999 X-40 Y28.5 Z0`. This will make it easier to gauge the distance between the Z-probe and the nozzle in the following steps. 6. Run the command `G29 S2`. This clears any active bed leveling compensation. This is **very** important as it will conflict with your updated Z-probe offset and induce a 0.1 - 0.3mm error depending on the magnitude of your bed leveling compensation at that point. 7. Deploy your Z-probe 8. Check whether the Z-probe is functioning correctly. This is a great step to perform before using your Z-probe in order to prevent crashes. Press your Z-probe limit switch and observe the change in value from 0 to 1000 in the Duet Web Console _Machine Status_ table in the _Z-Probe_ box. If the value does not change the Z-probe is wired or configured wrong, do not continue to the next step!

```text
![KWL6DTK3l4pAmrPv-zprobemachinestatus.png](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/KWL6DTK3l4pAmrPv-zprobemachinestatus.png)
```

1. Move the bed towards the nozzle by sending the command `G1 Z20`. When you send the command `G30` the bed will move slowly and precisely to the Z-probe, if you send `G30` while the bed is at `Z100` or greater you will have to wait for a long time for the Z-probe to trigger.
2. Run the command `G30`. This will move the bed toward the z-probe until the limit switch triggers.
3. Now your Z0 is set to your Z-probe limit switches trigger height. This is because the Z-probe limit switch offset is 0mm. Now that we have set our Z0 to the trigger height we can move the bed toward the nozzle in order to find the distance between the trigger height of the Z-probe and the nozzle!
4. Retract the Z-probe.
5. Jog the bed up slowly toward the nozzle using the negative Z buttons in _Machine Control_ on the Duet Web Console. Read the next step!

   ![Z81QrJdADnqOrI0d-MachineControl.PNG](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/Z81QrJdADnqOrI0d-MachineControl.PNG)

6. As you are moving the bed up towards the nozzle you will encounter an axis limit. These axes limits are set for the X, Y and Z axes and will stop you from moving past a certain coordinate. This will make it harder to crash the printer. However, in this case we know what we are doing so we can disable the axes limits. Send the command `M564 S0` to disable the axis limits. To learn more about this command visit the [RepRap G-code wiki](https://reprap.org/wiki/G-code#M564:_Limit_axes).
7. **Be careful when moving the bed close to the nozzle. Use the 1mm and 0.1mm buttons.** Determining when the bed is touching the nozzle can be difficult. You might have to heat up the nozzle as you learned before in order to ensure that none of the filament from the hot-end gets in the way. Using a piece of paper to determine when the nozzle is touching the bed is also helpful. Grab a sticky-note or small piece of paper and place it under the nozzle. Then carefully jog the bed into the nozzle, move the paper back and forth. When you feel the nozzle grab the paper your nozzle is touching the bed!. 
8. Record the Z-value that the printer is currently displaying in _Machine Status_. The absolute \(non-negative\) of this value is your Z-probe offset. It might be a good idea to write down this value.
9. Enter the command `G31 P999 X-40 Y28.5 Znnn` where `nnn` is your Z-probe offset.
10. Move the bed away from the nozzle `G1 Z20`.
11. Deploy your Z-probe!
12. Send the command `G30`.
13. Move the bed back up to the nozzle as described in the steps above. Your Z value should be 0 when the bed is touching the nozzle. If it is not you might need to tune the Z-probe offset or repeat the process.
14. In order for these changes to take effect permenantly, you will have to open up your _config.g_ file and update the Z-offset of this command there. Follow the section below.

**Troubleshooting the Limitswitch**

#### The IR Probe

The IR probe is located on the right side of the nozzle fan duct. The IR probe should be as parallel to the bed as possible. The IR probe functions by emitting Infra-Red rays \(hence the name IR probe\) at the bed and receiving them when they are reflected off a surface at a specific distance. Because not every surface is consistant, this detection height changes per surface. However, even variations within one surface can cause a difference in detection height. For example, glue from your previous print or a dirty print surface. This will all cause error and noise within your eventual bed level. We have found that this z-probe is very precise, but not always accurate. You will find that the limit switch is sometimes much better suited for some situations, such as a glass bed. While the IR probe is sufficient for others. For the best results we recommend a clean and dark surface such as a black print bed sheet. Follow the guide below for configuring your printer to use the IR probe.

**Configuring the IR Probe**

To use the IR probe a number of settings have to be changed in _config.g_. Ensure that the IR probe is parallel to the bed before using it. The following code should be entered or uncommented in _config.g_:

```text
    M558 P1 X0 Y0 Z1 H5 F120 T5000 ; Set Z probe type -- SET AS IR_PROBE
    G31 P450 X-30.4 Y-30.7 Z2.6 ; Set Z probe (IR) trigger value and offset
```

Remember that it is best practice to comment or remove all other instances of these commands in the configuration file, this will prevent you from mistakenly configuring and enabling the other z-probe. This code is for the compound nozzle, to obtain this code for the K'Tana nozzle visit the [M3D Promega GitHub Repository](https://github.com/PrintM3D/Promega).

The `M558` command above sets the z-probe type:

* `P1` sets the z-probe type.
* `X0 Y0 Z1` defines which axis this probe homes, any non-zero value enables that axis. In this case this probe only zeroes the z-axis.
* `H5` configures the dive height to 5mm. The dive height is the vertical distance the bed moves between probe moves
* `F120` sets the feedrate of the probe move.
* `T5000` sets the travel feedrate, the speed of travel in between probe moves.

The `G31` command sets the z-probe status:

* `P450` sets the trigger value, for the IR probe this **has** to be less than ~500 or the z-probe will not trigger. Manually test the z-probe trigger value before changing!
* `X-30.4 Y-30.7` defines the offset from the nozzle to the IR probe.
* `Z2.6` sets the z offset of the IR probe. This will have to be changed whenever you change the mounting height of the z-probe or whenever you change print bed material.

**Calibrating the IR Probe**

To discover the z-offset of the IR probe to the nozzle follow the steps below: 1. Home the printer and move to `X200 Y200 Z50`, probing in the center of the bed is the best idea as that is where the most printing occurs. 2. Heat up your bed and wait for it to reach temperature. Ensure that your print bed is clean. 3. Heat up your nozzle in order to remove any filament or debris on the nozzle tip. 3. Turn off bed leveling with `G29 S2`, bed leveling can interfere with probing the bed.

> Always disable bed leveling before probing or bed leveling, they will interfere with each other!!! 4. Check that the z-probe is functioning correctly by **manually** jogging the bed to the nozzle. You should see the Z-probe value in the Duet Web Console _Machine Status_ table change **before** the nozzle hits the bed. Remember the trigger value of the z-probe, this will vary per print surface. 5. Enter the command `G31 Pn Z1.0` where `n` is a value less than what you recorded in the previous step. The z-probe will trigger whenever it detects a value greater than `n`. `Z1.0` represents a stop gap to prevent a crash if you do send `G30`. 5. Jog the bed up until the bed is touching the nozzle, a piece of paper can help to determine when the nozzle is touching the bed. When the nozzle and bed are touching send command `G92 Z0`. This will set the current z-height of the printer to 0. 6. Move the bed to `Z20` with `G1 Z20`. 7. Send the command `G30 S-1` this will print out the z-height of the bed when the probe is triggered. It will **not** update your z-height value. Record the value that is printed out. To ensure that you are getting consistent values, you can repeat this step multiple times. Move the bed to `Z20` between every probe or you will get an error. 8. Send the `G31` command with your z-probe offset value set to the value you obtained in the step above. `G31 P450 X-30.4 Y-30.7 Znnn`, `nnn` is the value from the step above. 10. If you want these changes to affect your board permenantly, then copy and paste the command above into your _config.g_ file. Be sure to remove all other `G31` commands or comment them. 11. You have now successfully calibrated your IR probe. Send the command `G30` in order to probe the z axis. You can then move your bed up to your nozzle manually and verify that at `Z0` the nozzle is touching the bed.

### Bed Leveling

#### Skipping the Bed

If you crash the bed into the nozzle it will cause the bed to skip and fall. After this happens your bed might no longer be level. Follow the steps below to skip a tooth on the bed in order to level it. Once the bed is level within ~3mm you can allow Mesh Bed Leveling to complete the rest.

1. Power cycle the printer and then turn it on. This will make it easier to manually move the motors.
2. Move the bed up to the nozzle. The best way to move the bed of the Promega is by holding the bed with both hands on either side in the center as shown below. If you want to stop your bed from falling down you can place a binder clip on the z-motor belt as pictured below.

   ![4qdhdUQzgRlqtZuL-wheretoholdbed.jpg](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/4qdhdUQzgRlqtZuL-wheretoholdbed.jpg)

   ![2dmrbcxPSLMjnGwW-beltclip.jpg](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/2dmrbcxPSLMjnGwW-beltclip.jpg)

3. Once the bed is at the nozzle, gauge the distance between the Z-slider and the top z-belt clamp as shown in the picture below. If one of these distances is greater than the other four it means your bed is not level. If you have a caliper you can measure the distance between the bed and each belt clamp corner.

   ![7uGDRPPGzf2X74tx-distancezclampbed.jpg](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/7uGDRPPGzf2X74tx-distancezclampbed.jpg)

   ![ZVLNWJ7ERVNSrBPG-distancebedcorners.jpg](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/ZVLNWJ7ERVNSrBPG-distancebedcorners.jpg)

4. Move the bed halfway down the printer. Hold the bed in place while gently pulling up on one corner. Keep pulling up until you hear a loud click and feel the bed move in that one corner.

   > Be careful with the amount of force you apply as you can break the belts or belt clamps.

5. Repeat step 3 in order to check that your bed is now level. If it is not skip another corner of the bed.

#### Mesh Bed Leveling

1. Home the printer and heat up the bed to printing temperature. When the bed warms up it warps slightly. However, bed leveling compensation can compensate for this.
2. Define your mesh bed leveling grid with the `M557` command. The _config.g_ file should already have configured a working mesh: `M557 X50:370 Y10:350 S30`. You can change the maximum and minimum values of the mesh as well as the interval but be careful as running G29 with a wrong mesh can crash your printer. Be sure to take the offsets of the z-probe as defined in `G31` into account.
3. Disable any previous bed leveling compensation with the command `G29 S2` or `M561`, they accomplish the same goal. If you do not disable previous bed leveling you will find that your next heightmap will be off by around +- 0.3mm.
4. Ensure that you have properly configured your z-probe as in the sections above. Test your z-probe before probing by triggering the sensor and observing a change in the _Machine Status_ tab.
5. Make sure your bed is as level as possible. While bed leveling compensation can account for small variations in bed height it can't account for greater than 2-3mm.
6. If you are currently using the limit switch be sure to place it on its mount. If you are using the IR probe ensure that your bed is squeaky clean.
7. Send the command `G29 S0` to execute bed leveling immediately or `G32` which will execute _bed.g_. _bed.g_ can be a simpler option in the long run as it can automatically heat up your nozzle and bed and define your mesh grid before.
8. The bed leveling procedure will generate a _heightmap.csv_ file located in the _sys/_ folder. Once the bed leveling procedure completes it should display the heightmap. If this is not the case you can always go to _Settings &gt; System Editor_ and then click _heightmap.csv_ in order to see your heightmap.
9. Once bed leveling completes it should have already enabled the compensation. `G29 S1` enables compensation from _heightmap.csv_ by default and `G29 S2` disables compensation. In _config.g_ you should have the command `G29 S1` which enables bed compensation so you don't have to re-run the bed leveling procedure everytime.

