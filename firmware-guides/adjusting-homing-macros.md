# Adjusting Homing Macros

Whenever you press the homing buttons located on the _Machine Control_ tab of the Duet Web Interface macros are called. This guide will cover the possible changes you can make to your homing G-code files. For assistance in homing your printer checkout the [Homing the Printer](http://promega.printm3d.com/books/user-manual/page/homing-the-printer) guide.

#### Homing Macros

If you looked inside the _sys/_ directory of the microSD card you will have noticed five homing files. These homing files control the homing of different components of the printer.

* **homeall.g**: This file contains G-code to home all three axes of the printer. This file is executed whenever the command `G28` is entered or whenever the _Home All_ button on the Duet Web Interface is pressed.
* **homex.g & homey.g**: This file contains G-code to home the coreXY system of this printer. Because this printer is a coreXY system, the X and Y axes are linked. We recommend that whenever you home your X axis, you also home your Y axis. This is visible in these G-code files as they are both the same. Each g-code file homes both the X and Y axes. If you prefer, it is possible to separate the homing of the two axes. These files are executed whenever the _Home X_ or _Home Y_ buttons are pressed or when `G28 X` or `G28 Y` is sent.
* **homez.g**: This file contains G-code to home the Z-axis of this printer. It is called whenever you press the _Home Z_ button on the Duet Web Interface or `G28 Z` is sent.
* **homedelta.g**: This file is for homing a delta printer, so obviously not very necessary.

**Changing the Macros**

You are free to change the G-code in the homing macros. But be careful as you could easily crash your printer. When your printer is not homed but moves to a physical limit it will skip motors or belts. Please be sure of the direction you are sending your assemblies and ensure that they will hit the limit switch. Each homing macro contains a few critical commands, in the section below we will go over those commands.

* `M564 H0 S0`: Ignore Machine Boundaries, when you home the printer it is likely because you want to define the printers location and limits. To do this the printer might have to pass through boundaries set in the config.g file. The printer also has to be allowed to move while the axes are not homed. This exception to allow movement while not homed and through axes limits is performed with this command. Put this command at the start of every homing macro. At the end of the homing macro you can engage the axes limitation and homing requirement again with the command `M564 H1 S1`.
* `M561` & `G29 S2`: These two command disable bed leveling compenation during this process. It is best not to compensate for bed leveling while homing. Therefore you can disable bed leveling compensation at the beginning of the macro and enable it with the command `G29 S1` at the end of the macro.
* `G91`: Change to relative positioning. Because the printer does not know where it is, this command will base its movement based on the current position. In order to change back to absolute positioning enter the command `G90` at the end of the macro.
* `G1 S1`: The move command is important to allow the carriage to move to the desired location. It is vital to include the `S` parameter in this command with a value of 1 in order to enable endstop detection. Endstop detection means the printer will check if an endstop was hit. Failure to provide this parameter will crash the printer!
* `G92`: This command allows you to set the value of a particular axis. This is the core command of the homing process, whenever you hit a limit switch, you can use `G92` to define the printers position.
* `M208`: This command allows you to define axes limits which can then be enabled and enforced with `M564`.

**Homing Procedure**

When the Promega certain physical constraints have to be taken into consideration.

