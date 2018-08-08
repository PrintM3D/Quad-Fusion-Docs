# Heater Troubleshooting

This guide serves to fix any problems you might have with the heater cartridge or PT1000.

## PT1000 Problems

![](../.gitbook/assets/image%20%2822%29.png)

The PT1000, or thermistor, is what reads the temperature of the heater block and relays the information onto the Duet Web Control. 

### **Possible Problem\(s\):**

**Not Reading Temperature:**  
This is assuming that whenever you attempt to to heat your extruder the thermistor doesn't read any value which results in a heater fault. It is very likely that the issue here lies within your printer's settings. 

**Solution:**

{% hint style="info" %}
This solution is more directed towards Crane users. If you have a different printer, you may need to tweak some things.
{% endhint %}

Go into Settings, System Editor, and under config.g go to the Heater section:

`;Heaters                                                                               M305 P0 T100000 B4138 C0 R2200   ;Set thermistor+ADC parameters for heater 0            M143 H0 S120                     ;Set temperature limit for heater 0 to 120C                            M305 P1 X501 T1050 R2200         ;Set themistor+ADC parameters for heater 1                 M143 H1 S280                     ;Set temperature limit for heater 1 to 280C`

Try changing the values to match what is above, look under [Heating & Temp Sensor]() guide to fully understand what each letter means. 

## Heater Problems

![](../.gitbook/assets/image%20%2841%29.png)

### Possible Problem\(s\):

**Heater Faults:**  
When trying to heat up your nozzle, if you receive a heater fault there can be a few reasons. The first possibility is that your printer's settings have been set up to expect that your heater will heat faster than it is able to. The second possibility is that your heater is not heating. 

**Solution:**  
The first reason for a heater fault can be solved by editing your printer settings. Go into Settings, System Editor, and under config.g go to the Heater section:



**Loose Connection:**  
It is possible when setting up your QuadFusion that the Heater wire was bent. The pins in the connector may have gotten loose, which is causing your heater to heat poorly.  You may be able to identify this issue by trying to heat your nozzle and wiggling the heater wire. If you get a similar result as the picture below, you have a loose connection:

![Image pulled from: https://forum.duet3d.com/topic/4966/highly-erratic-temperature-readings-above-certain-temperature ](../.gitbook/assets/image%20%2856%29.png)

As you can see the red line is no longer steadily rising, but has begun to move exaggeratedly. 

**Solution:**  
There are two solutions, the first being replace your heater wire entirely. Unless you have the means for the second option, this is by far the least tedious. 

