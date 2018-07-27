---
description: How to home the Crane.
---

# Changing Homing Offsets

Before you start printing or moving any component of the Crane, we recommend homing the printer. Follow the steps below in order to home your printer. Prior to homing your printer check that the gantry and bed are able to move freely and access the limit switch. This guide assumes you have connected to the Crane as outlined in [Network Setup](network-setup.md).

## Printer Axes

![](../.gitbook/assets/promegacoordinateaxes.jpg)

In order to control the Crane it is important to understand the axes of the printer and their orientation. As you can see in the image above the X axis spans across the front of the printer from left to right if you are facing the front of the printer. The Y axis is pointing from the front to the back and the z-axis is pointing down. Remember these axes directions as you jog the printer with the _Machine Control_ tab in the [Duet Web Console](https://m3d.gitbook.io/promega-docs/getting-started/accessing-web-interface). **Positive Z is down and negative Z is up!**

The origin of this coordinate frame is in the top-front-left corner of the printer. This can be seen at the intersection of the three red axes of the 3D printer in the image above.

## The Homing Process

Follow the steps below to correctly home your printer.

### Checking the path

1. To ensure that the printer homes correctly, we recommend moving the coreXY gantry manually to the limit switches located in the back right corner when the motors are not powered. If you need to unpower the motors you can use the G-code command `M84` to stop the idle hold of the motors. Watch out as this will disable **all** motors, and could cause the bed to drop. Remove all items from inside of the printer before homing. The PTFE filament tubes on the extruder carriage cable assembly should be clicked in place \(shown in the image below\), or they could cause problems when homing the X-axis.

   ![tXK2bR1RP6wPsEGA-PTFECheck.jpg](../.gitbook/assets/txk2br1rp6wpsega-ptfecheck.jpg)

2. Move the coreXY gantry against the Y-limit switch, listen for the click of the limit switch. **Warning: when manually moving the gantry be careful not to move the extruder carriage past the limit switch tab as you can easily break it off**.

   ![90nsbbYgUkrZWDvj-Y-limit.gif](../.gitbook/assets/90nsbbygukrzwdvj-y-limit.gif)

3. Then move the coreXY gantry against the X-limit switch.

   ![deUkxjexf1j1MZLn-X-Limit.gif](../.gitbook/assets/deukxjexf1j1mzln-x-limit.gif)

4. Make sure the bed is resting on the Z-limit switch and that there is nothing underneath the bed.

### Homing the Printer

1. You are now ready to home the printer. There are multiple ways to initiate the homing process. You can press the _Home All_ button located in the _Machine Control_ tab of the Duet Web Console. You can also send the G-code command G28. These two operations will both execute the same file _homeall.g_, located on the microSD card.

   ![vMOKr4toGvCnhyX8-homeallbutton.png](../.gitbook/assets/vmokr4togvcnhyx8-homeallbutton.png)

2. The coreXY gantry should move toward the Y-limit switch located at the back of the printer first. Once it has hit that limit switch, it will move toward the x-limit switch. Next, the bed will lift itself up and back down slowly, until it has hit its limit switch.
3. Now all axes are homed. Remember that your motors are now powered and you will not be able to move any of the assemblies by hand. Use the `M84` command to temporarily disable idle hold current on your stepper motors, allowing you to move the motors. Your \(0,0,0\) is located at the top-front-left of the printer. 

## Tuning the Z-homing Procedure

**Because the distance between the bed and the nozzle depends on your Crane configuration \(K'tana vs. Compound, Glass vs. no glass\). You will have to tune** _**machine\_zendstop.g**_ **for Z0 to line up.**

Ideally whenever you home the printer and send the command `G1 X0 Y0 Z0` \(telling the printer to go to \(0,0,0\)\) the print bed will touch the nozzle. However, as outlined above, the difference between the bed and the nozzle varies depending on your setup. Follow the steps below to update your _machine\_zendstop.g_ file.

1. Home the printer if you have not already done so in the section above.
2. Send the command `G29 S2` , this will disable bed leveling. Bed leveling can conflict with your homing value.
3. Move the printer to Z10 with the command `G1 Z10`
4. Move the printer head to the center with `G1 X200 Y200`
5. Jog the bed up the nozzle with the buttons in machine control until the bed is touching the nozzle. Use the _Z1mm_ and _Z0.1mm_ buttons. Remember that you are about 10mm away from the nozzle.

   ![](../.gitbook/assets/machinecontrol-1.png)

6. Once the bed is properly touching the nozzle record the Z-value in _Machine Status_ on the Duet Web Console_._ This value will be used in the next step.
7. Open the _machine\_zendstop.g_ file in the _Settings_ tab of the Duet Web Console. This file is called during the homing process of the Z-axis. Find the `G92` command at the end of the file. This command sets the z-axis height.
8. Update this value with the following formula:  $$new value = old value - step6value$$  For example: if the _machine\_zendstop.g_ file currently contains the command  `G92 Z376.4` and I obtained a value of -0.6. My new value would be 377mm, and I would remove the current command and enter `G92 Z377`
9. Save the file and home the printer again. Although you should now be able to enter the command `G1 Z0` , I don't recommend it. Manually jog your bed to the nozzle again to ensure that Z0 is when the bed is touching the nozzle.

Continue on to the [Heating the Bed and Nozzles](https://m3d.gitbook.io/promega-docs/getting-started/heating-the-bed-and-nozzles), the next chapter in the [Getting Started](https://m3d.gitbook.io/promega-docs/getting-started) guide.

