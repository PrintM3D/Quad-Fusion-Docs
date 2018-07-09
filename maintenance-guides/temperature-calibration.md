# Temperature Calibration

Proper temperature calibration is vital to allow for good print quality. The hot-end\(s\) and the bed are controlled by temperature feedback loops which are supposed to maintain a steady temperature. The type of feedback loop is a first order plus dead time \([FOPDT](https://controlguru.com/process-data-dynamic-modeling-and-a-recipe-for-profitable-control/)\) loop. This loop has three different control variables: 1. Gain: Kp: Allows for manipulation of the strength of the heater response. 2. Time Constant: Tp: Control of the speed of the response of the heater. 3. Dead time: The delay before the system will begin a response.

This control loop and its variables are applied to the different heaters on the Promega. With the command `M303` and `M307` the temperature control loop can be tuned and changed. The default control variables supplied by M3D in the configuration files should allow you to print at a stable temperature. However, significant changes to the printing environment, such as room temperature, air-flow or humidity can impact your control loop effectiveness and stability. An improper control loop can cause problems listed below.

* **Overshoot**: A response to a new set-point will send the temperature of the heater significantly beyond the set-point. An overshoot of about 15°C is reasonable. A greater overshoot can cause your filament to char or present a fire hazard. 
* **Oscillation**: An unstable control loop can result in a temperature oscillation. An oscillation of more than 5 °C degrees can impact printing quality.
* **Steady-state Error**: The stable temperature output of the control loop does not reflect the temperature set-point.
* **Long Response Timer**: The heater will take a long time to achieve the desired set-point. While not dangerous, this can be an annoying and unnecessary delay.

#### Auto-tuning

RepRap firmware has a built in auto-tune heater function. This allows you to tune the control loop of a heater on the Promega. Follow the section below!

**WARNING: The auto-tune function can rapidly heat your hot-end\(s\) to a high temperature. DO NOT leave your printer unattended while running** `M303`

**Overview**

The command `M303` will heat-up your hot-end to a set-point temperature and record data as it does so. Therefore, while your hot-end is undergoing it is important to replicate the conditions that your 3D printer prints in. For example, turning on your nozzle fans. First, the tuning process will heat the hot-end to your set temperature. It will likely overshoot the set-point. The nozzle will then cool-down to room temperature. If you instructed the control board to perform multiple cycles, it will repeat this process multiple times. Once complete, the firmware will return suggested control variable values.

`M303` Parameters:

* `Hnnn`: Heater number \(by default: 0 is bed, 1 & 2 hot-ends\)
* `Pnnn`: PWM percentage from 0 to 1.
* `Snnn`: Set-point temperature in °C

`M307` Parameters:

* `Hnnn`: Heater number \(by default: 0 is bed, 1 & 2 hot-ends\)
* `Annn`: Gain constant
* `Cnnn`: Time constant
* `Dnnn`: Dead time
* `Fnnn`: PWM frequency
* `Bn`: Bang-bang control enable \(1\)
* `Snnn`: Maximum PWM
* `Vnnn`: Vin at the time of calibration. Allows for compensation of power supply voltage variation.
* Unload the filament from your hot-end. Once you are more familiar with the `M303` command, this step is not necessary. We recommend removing filament as it can burn and char inside your hot-end if the tuning process reaches a high temperature.
* Wait for the heater to reach room temperature. **This is important to achieve a good result!**
* Send the `M303` command. Change the `H` parameter to reflect the heater number. The PWM percentage can be changed with `P` if the heater is heating up too fast, and the firmware is unable to present control variables. The `S` parameter should be set to a typical printing temperature, such as 230°C. An example would be `M303 H1 P0.5 S230` in order to run auto-tune on hot-end 1, with 50% PWM and to 230°C.
* Wait for auto-tune to complete. Do not leave the printer unattended.
* The firmware should print out the calculated control variables. Sending `M303` should also display the control variables.
* Use the `M307` command in order to set new control variables. Use the parameter list above to determine the proper syntax. 
* Remember to replace the `M307` command in the configuration file _config.g_ with the command you just entered in order for your changes to take effect upon a system restart.

#### Legacy PID Control

RepRap firmware also allows for control of the heaters with basic PID with three different constants: Kp, Ki, Kd. Use the command `M301` in order to send enable and send these control variables. These control variables also can be found by running the `M303` auto-tune as listed above. The command `M301` will enable the legacy PID control loop.

`M301` Parameters:

* `Hnnn`: Heater number
* `Pnnn`: Proportional constant \(Kp\)
* `Innn`: Integral constant \(Ki\)
* `Dnnn`: Derivative constant \(Kd\)

#### Manually Tuning

Manually tuning your control variables can be done. Read more about the control variables explained in this guide online and their effects on a control loop before changing your control variables. Manually tuning your control variables is often a great option to reduce or obstruct observed errors as the ones listed above. Tuning your control loop from scratch is not recommended! Be careful when changing your control variables as it could easily produce unintended consequences.

