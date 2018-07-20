# \(Edit details\) Help! My Extruders are Backwards

Whenever you are changing or updating configuration files it is possible that your heaters or extruders will be wrongly configured. This could result in your extruder drivers going the wrong way, or the left extruder spinning when you want the right extruder to spin.

## Flipping Extruder Directions

This will fix extruder drives that are going backwards. For example if you pressed the button _Extrude_ on the Duet Web Console it will result in the drive pushing filament back out of the extruder hole as if you were retracting. **Heads-up read the information box below.** If you implement this fix, and in the future update to new configuration files, it will undo these changes.

{% hint style="info" %}
It is possible that your extruder directions are flipped because the extruder drives are flipped, meaning left is wired to right and right is wired to left. Check that your left extruder \(drive 0\) does actually move the left extruder and that the right extruder \(drive 1\) actually moves the right extruder.
{% endhint %}

1. Connect to the Crane's Duet Web Console
2. To check your extruder directions go to the _Machine Control_ tab in the Duet Web Console and select drive 0 or 1 in _Extruder Control._ Then try to feed filament into the extruder and see if your directions are correct. It is also possible to change the extruder drives in the section below. If your filament is being pushed out of the top of the extruder when you press extrude, follow the steps below.  ![](../.gitbook/assets/machinecontrol%20%281%29.png) 
3. Go to the _Settings_ tab of the Duet Web Console and then to the _System Editor._  ![](../.gitbook/assets/settingsssytemeditor%20%281%29.png) 
4. Open the _config.g_ file. Find the block with the following commands:  
   `; --- SECTION: DRIVES (MOVEMENT SECTION) & ENDSTOPS ---`

   `M667 S1 ; Enable coreXY mode    
   M569 P0 S0 ; Drive 0 goes forwards, CoreXY_1    
   M569 P1 S1 ; Drive 1 goes forwards, CoreXY_2    
   M569 P2 S1 ; Drive 2 goes forwards, Z Motor    
   M569 P3 S0 ; Drive 3 goes forwards, Left Extruder    
   M569 P4 S1 ; Drive 4 goes forwards, Right Extruder`

5. Change the `P3` and `P4` drive directions with the `S` parameter. For example, if my left extruder was going backwards, I would change the command to go from `M569 P3 S0`

   to`M569 P3 S1.`

6. Save the file and reboot the system. Repeat step 2 to confirm that the directions are correct.

## Flipping Extruder Drives

This section will fix extruder drives that are flipped. If you actuate what you think is the right drive and it results in the left drive spinning and vice versa. **The inherent problem here lies in wiring, so be aware, the fix you are applying is temporary.** The wiring is intended to have the left extruder wired to extruder drive 0 and the right extruder to extruder drive 1. If you implement this fix, and in the future update to new configuration files, it will undo these changes. To fix this permanently fix the wiring of your Crane in the [Extruder Wiring](../electrical-guides/extruder-assembly-wiring.md) guide. The fix below is fine to implement, but will provide a temporary solution.

1. Connect to the Crane's Duet Web Console
2. To check your extruder drives go to the _Machine Control_ tab in the Duet Web Console and select drive 0 or 1 in _Extruder Control._ If you have extruder drive 0 selected and press extrude it should move the left extruder. For extruder drive 1, the right extruder should move.  It is also possible to change the extruder drives in the section below.   ![](../.gitbook/assets/machinecontrol.png) 
3. Go to the _Settings_ tab of the Duet Web Console and then to the _System Editor._  ![](../.gitbook/assets/settingsssytemeditor%20%282%29.png) 
4. Open the _machine\_compound\_tools.g_ \(or _machine\_ktana\_tools.g_\) \_\_file. And find the `M563` commands, this configures the tool:  
   `M563 P0 D0:1 H2 F2 S"Mixing" ; Define mixing tool`

   `M563 P1 D0 H2 F2 S"Mixing as Single Left" ; mixing nozzle only using left extruder motor    
   M563 P2 D1 H2 F2 S"Mixing as Single Right" ; mixing nozzle only using right extruder motor`

5. For the tools with only one drive \(the `D` parameter\) you will have to change the drive. If it was using `D1` change it to `D0` and vice versa. You are telling the firmware to use drive for 0 or 1 for specific tools.
6. Save the file and reboot your printer.
7. Check the direction of the drives now as you might have to now flip the directions of the extruder drives.

## Changing Tool Heaters

Just like in the section above, you can use the `M563` command in order to change which tool uses which heater. This section will fix a heater that is wired to the wrong port of the Crane, or configured wrong. This will present itself in the form of a heater fault, or a thermistor error value of 2000°C.The Crane configuration expects heater 1 to be assigned to the left tools and left extruder, and heater 2 to be assigned to the right tools and right extruder. Remember that heater 0 is the heated bed in the configuration files.

1. Connect to the Crane's Duet Web Console   
2. Go to the _Settings_ tab of the Duet Web Console and then to the _System Editor._  ![](../.gitbook/assets/settingsssytemeditor.png) 
3. Open the _machine\_compound\_tools.g_ \(or _machine\_ktana\_tools.g_\) \_\_file. And find the `M563` commands, this configures the tool:  
   `M563 P0 D0:1 H2 F2 S"Mixing" ; Define mixing tool`

   `M563 P1 D0 H2 F2 S"Mixing as Single Left" ; mixing nozzle only using left extruder motor    
   M563 P2 D1 H2 F2 S"Mixing as Single Right" ; mixing nozzle only using right extruder motor`

4. Change the heater number \(`H` parameter\) assigned to the tools above. It should be either `H1` or `H2` .
5. Save the file and reboot the Duet.
6. Look for a change in temperature reading on the Duet Web Console. If it is displaying a proper value, you can try to heat up the heater.

