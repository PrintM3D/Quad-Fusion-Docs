---
description: Getting the heater and Temp sensor calibrated on the QuadFusion 3D Print Head.
---

# \*Heating & Temp Sensor

This guide expects the reader to have completed setting up its QuadFusion, all except the Heater. Your printer should be homed, the fans should be mounted, and the QuadFusion should be correctly assembled. 



1. Connect to the Duet Web Control
2. Go to Settings, and under System Editor you will want to open up your printer's config.g .
3. Scroll until you have reached the Heater section. Which may look like what's below:

`;Heaters                                                                               M305 P0 T100000 B4138 C0 R2200   ;Set thermistor+ADC parameters for heater 0            M143 H0 S120                     ;Set temperature limit for heater 0 to 120C                            M305 P1 X501 T1050 R2200         ;Set themistor+ADC parameters for heater 1                 M143 H1 S280                     ;Set temperature limit for heater 1 to 280C` 

`M305` Explained:

`M305` is the G-code command that sets the heater's parameters by using \(as above\)  
`Pnnn` is used to describe which heater is being edited  
`Xnnn` is the heater ADC channel, or thermocouple or PT100 adapter channel  
`Tnnn` is used to indicate the thermistor's resistance   
`Bnnn` is the beta value if the sensor is a thermistor  
`Cnnn` is the Steinhart - Hart C coefficient \(default 0\)  
`Rnnn` is the series resistor value for the PT1000 and PT100

`M143` Explained:

`M143` is   
`H` is the heater being edited  
`S` is the maximum temperature

{% hint style="info" %}
All this information can be found at: [https://duet3d.dozuki.com/Wiki/Gcode\#Section\_Introduction](https://duet3d.dozuki.com/Wiki/Gcode#Section_Introduction)
{% endhint %}

4. Try heating up your tools to 200C. You should see the red line on the graph begin to increase:

![](../.gitbook/assets/image%20%2826%29.png)

Additionally, you should see that the Current temperature matches the Active temperature. This indicates that you thermistor \(PT1000\) is working as well. 

![](../.gitbook/assets/image%20%285%29.png)

If anything is wrong, or you received a Heater Fault, go to the [Heater Troubleshooting](../troubleshooting-guides/heater-troubleshooting.md) guide for help.

