# Heating the Bed and Nozzles

Both the bed and the hot end\(s\) of the Promega can be activated through the Duet Web Console. You can either utilize the web interface to set a temperature for these components or send G-code commands such as `M109`, `M104`, `M140` or `M190`. Read the sections below to learn more.

> Prior to every heating of the nozzles or the bed, check the temperature readouts in the _Current_ column. These values should be in the 20°C - 250°C. A value of 2000°C a problem in the wiring of the thermistor. Fix the issue prior to activating the heaters.

## Heating Up the Bed

1. Connect to your Duet via your network. Utilize [the network setup guide](https://m3d.gitbook.io/promega-docs/getting-started/network-setup) to help with network setup, and [web interface guide](https://m3d.gitbook.io/promega-docs/getting-started/accessing-web-interface) to provide a better understanding of the Duet Web Console. Once you are connected, proceed to the next step. Decide whether you want to heat up the bed with G-code commands or via the Duet Web Console.

**Heating the Bed with Duet Web Console**

1. In the Duet Web Console find the table _Tools/Heaters/Extra_, pictured below. In the row _Bed_ change the active temperature from 0C to your desired temperature and press Enter.

   ![ZzzciCea9XJ9Ev9A-heatingbed.PNG](../.gitbook/assets/zzzcicea9xj9ev9a-heatingbed%20%281%29.PNG)

2. In order to turn the heated bed off, set the temperature back to 0 in the _Active_ column and press Enter.

> It can take a few minutes for the bed to reach the desired temperature.

**Heating the Bed with G-Code Commands**

1. Utilizing G-code commands can be fast and easy, but be careful with the commands you enter, the control board will execute everything you send.
2. To heat up the bed, commands `M140` and `M190` are utlized. `M140` sets a temperature for the bed and immediately allows the board to execute other commands. `M190` will set a temperature for the heated bed, and temporarily halt the processing and execution of commands until the bed has reached its set temperature.
3. The `M140` and `M190` commands have an S parameter to specify temperature. For example, sending the command `M140 S60` will heat up the bed to 60°C without waiting. Observe the temperature change in the graph and table of the Duet Web Console.
4. In order to turn off the bed send the `M140` command with a temperature of 0. Like so: `M140 S0`.

> It can take a few minutes for the bed to reach the desired temperature.

## Heating Up the Nozzles

1. Just like heating up the heated bed, connect to your Duet via your network. Utilize [the network setup guide](https://m3d.gitbook.io/promega-docs/getting-started/network-setup) to help with network setup, and [web interface guide](https://m3d.gitbook.io/promega-docs/getting-started/accessing-web-interface) to provide a better understanding of the Duet Web Console. Once you are connected, proceed to the next step. Decide whether you want to heat up the nozzle via G-code commands or the Duet Web Console.

**Heating the Nozzles with Duet Web Console**

1. In the Duet Web Console find the table _Tools/Heaters/Extra_, pictured below. In your desired tool row change the active temperature from 0C to your desired temperature and press Enter.

   ![ZzzciCea9XJ9Ev9A-heatingbed.PNG](../.gitbook/assets/zzzcicea9xj9ev9a-heatingbed.PNG)

2. Remember that the tool will only heat up to your set active temperature when the tool is selected. Select a different tool with the command `Tn` where `n` is your tool number.
3. In order to turn off the heater. Set the tools active temperature to 0 and press Enter. Remember that a tool will heat up to the standby temperature when the tool is not selected.

**Heating the Nozzles with G-code Commands**

1. Utilizing G-code commands can be fast and easy, but be careful with the commands you enter, the control board will execute everything you send.
2. To heat up the nozzles, use commands `M104` and `M109`. Just like with the heated bed, the distinction between these two commands is that one command, `M109`, waits for the extruder to reach temperature, while the other, `M104`, does not wait for the extruder to reach temperature. The `M104` and `M109` commands require an `S` parameter which allows you to define the temperature. For example, if you wanted to set the extruder to 230°C, and wait until the extruder reaches the set temperature, you would enter the command `M109 S230`.
3. Remember that this command will heat up the heaters of the tool currently selected.
4. In order to turn off the nozzle send the set temperature command `M104` with a temperature of 0.

Continue on to the [Loading and Unloading Filament](https://m3d.gitbook.io/promega-docs/getting-started/loading-and-unloading-filament) guide, the next chapter in the [Getting Started](https://m3d.gitbook.io/promega-docs/getting-started) guide.

