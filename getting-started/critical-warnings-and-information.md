# \(Edit details\) Critical Warnings & Information

The M3D Crane is an industrial product. The user assumes all responsibility for proper operation and acknowledges that they understand the operation and standard practices of additive manufacturing. The user assumes all responsibility for its proper use and agrees to follow the directives below to ensure a safe and working unit before any other operation.

## Warnings

1. DO NOT TOUCH PRINTER WHILE OPERATING The Crane is a powerful industrial machine. While the Crane is moving or printing you should not reach into the buildspace.
2. DO NOT MOVE THE BED WITHOUT POWER

   The belts on the printer bed can skip, causing a 2mm shift in your bed level, which will need to be fixed. There is a small but real chance it may damage the Duet board. Do not place heavy items or lean on the bed as it can also skip it.

3. MOVE MOTORS SLOWLY

   Moving motors generates power on all printers and can damage your board. A good indicator of the power you are generating is the cold section fan on the front. If you can hear the fan moving air, you're close to voltages that will break the duet regulator \(more than 28V\). As long as you can see the fan is not gaining speed you are fine. Move components at about 30 mm/s. It is best to always move components while the system is powered.

4. DISABLING MOTORS

   When you disable motors the bed will drop to the limit switch. Giving you print access.

5. ESD SAFETY:

   The Duet contains an ARM class 2 processor, we recommend you use a wrist straps when touching any wires that could send shocks to the main processor and fry it.

6. DON'T USE AN ESD WRIST STRAPS TIED TO A SURGE STRIP

   The printer is grounded. If you wire the strap wrong it can cause a short circuit through your body whenever you touch the printer.

7. USE UNDER SUPERVISION

   Place the printer in a place where nothing can catch on fire should the worst occur. The Crane is constructed out of metal and fireproof materials. Still, PLA and other filaments can burn and cause a fire if the printer is used improperly.

8. MAXIMUM EXTRUDER SPEED

   Don't extrude faster than 5.6 mm^3/s with any filament in compound extruder to start. Get success first with no skipping then try to push the limits. Do the math: 45mm/s movement, 0.3 mm layers and 0.5 mm wide would be 6.75mm^3/s , a bit to fast for your first print, especially with pla. So adjust layer heights accordingly, for example to 0.25mm high for your first prints. Over time you should be able to print faster. Remember that speed depends on material, number of print moves per second, nozzle type and temperature.

9. Z SPEED

   The bed current, acceleration and speed are configured for heavy prints. You can increase speed when printing lighter items. Currently, the acceleration of the z-axis is set to 75 mm / s ^2 and a max linear speed of 2300 mm/s but that can be improved depending on your application of the printer.

10. BED TEMPERATURE

    If you are using a glass print bed, give the printer an extra few minutes to reach temperature. Without the side and front covers, the glass will be 5-10 C cooler than the bed temperature readouts from the thermistor.

11. FRAME CAN BE SHARP

    The frame of the printer is metal and could be sharp. Use caution when moving the printer or moving around the printer. Keep your hands out of the machine during operation and be careful when lifting.

12. BURN HAZARD

    BED and NOZZLES may cause burns when hot.

13. USE CAUTION WHEN REMOVING PRINTS

    The best strategy is to let the bed cool, most prints pop off by themselves.

14. WATCH THE FAN

    The cold section fan is spinning very fast when the system is on. Please keep tools and yourself clear of it when it is operational.

## About the Z-assembly

1. 
Continue on to the [Unboxing & Assembly](https://m3d.gitbook.io/promega-docs/getting-started/unboxing-and-assembly), the next chapter in the [Getting Started](https://m3d.gitbook.io/promega-docs/getting-started) guide.

