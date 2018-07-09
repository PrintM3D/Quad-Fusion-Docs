# Important G-Code Commands



This guide serves as a brief introduction to G-code commands. It will list the most useful and important commands to allow proper control of the Promega.

### An Introduction to G-Code

G-code is frequently used programming language to control machine tools, such as a 3D printer. G-code is sent to the printer and promptly executed by a control board, in the Promega's case, the Duet Maestro. What each G-code command does depends on the firmware type the board is running. The Promega runs Reprap firmware, you can find an in-depth list of all supported G-code commands on the [RepRap G-code Wiki](https://reprap.org/wiki/G-code).

G-code commands are sent and interpreted one line at a time. G-code commands typically include a letter followed by a number. In RepRap firmware the first letter of a command will usually be a `G`, `M` or `T`. This letter will then be followed by a number. Together, a letter and number specify a command. For example, `G1` is the move command. However, there is little you can do with just the move command `G1`. So the initial command is typically followed by sequences of letters and numbers called parameters. For example `G1 X100 Y200`, which will move the printer to the 100mm X and 200mm Y position. `X100 Y200` are both parameters in this case. Use the guide below to get an introduction to the most important and useful G-code commands to have as a beginner. There are many more G-code commands that RepRap firmware supports. Be sure to use the link above to continue learning new G-code commands.

#### Important G-Code Commands

* `M112`: Emergency stop, will stop all heaters and motors. A reset with `M999` or power cycle will be required.
* `M999`: Reset the board. This has to be done after the board is emergency stopped or an error has halted the boards operation.
* `G0 & G1`: Move motors or axes, these are the primary movement commands of many printers. There is currently no difference between `G1` and `G0` for RepRap firmware. These commands are followed by parameters to identify distance, feedrate and motors to drive. `G1 Xnnn Ynnn Znnn Ennn Fnnn Snnn`
  * `X, Y` and `Z` represent the different axes. `nnn` represents the distance to travel along that axis.
  * `E` represents an extruder motor. The extruder motor distance is specified just like the X, Y and Z parameters. `E50` will move the extruder to the 50mm position.
  * `F` Allows you to specify a feedrate in mm/s. Feedrates vary greatly depending on whether you are printing or travelling.
  * `S` Enables or disables the endstop check. If the endstop is toggled while moving the printer stops, the `S1` flag enables detection, `S0` disables detection.
* `Tnnn`: Tool select G-code. Where `nnn` defines the tool
* `M106 Snnn`: Turn on fans with speed `nnn`. `nnn`    can be a value between 0 and 255. For older versions of _config.g_ `M106 P2 Snnn` will enable fan control.
* `G30`: This command allows a single Z-probe at the current location. The z-probe should be properly configured before sending this command. Follow the [Bed Leveling & Probing](http://promega.printm3d.com/books/user-manual/page/bed-leveling-probing) guide for more explanation on this topic.

