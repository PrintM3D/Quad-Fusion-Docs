# M3D Crane

This guide will go through the process of hooking up your QuadFusion to M3D's Crane 3D printer.  


### Mechanically

![](../.gitbook/assets/image%20%2874%29.png)

**You will need...**  
**-** 3mm Hex Standoffs \(\_\_\_\_mm long\) \(x2\)

**Tools...**  
**-** 2.0mm Hex Screwdriver  
**-** 3.0mm Hex Screwdriver  
**-** Pliers

If you look behind your Crane, you should see the mount that is already fixated upon it:

![](../.gitbook/assets/image%20%2839%29.png)

Undo the circled wheel using the 3.0mm Hex Screwdriver and the Pliers

![](../.gitbook/assets/image%20%287%29.png)

Once you have removed the bottom wheel, unscrew the two circled screws on the back of the mount. 

Next, attach the two standoffs to the QuadFusion:

![](../.gitbook/assets/image%20%2811%29.png)

Finally, thread the 2.0mm Hex Screws into the standoffs, and mount the QuadFusion head onto the Crane.

### Electrically

**You will need...  
-** 24V Power Supply  
**-** Duet Maestro Board  
**-** Duet Maestro Expansion Board  
**-** Jumper

**Tools  
-** Flat-Head Screwdriver



This is the Duet Maestro:

![https://duet3d.dozuki.com/Wiki/Duet\_2\_Maestro\_Hardware\_Overview](../.gitbook/assets/image%20%2854%29.png)

This will be a walk through on how we hooked up the QuadFusion, as well as part of the Crane, to the Duet Maestro board.

Before you can begin to wire your QuadFusion to the Duet Maestro board you must attach an extension to the board. With this extension you will be able to connect the the extra motor wires to the board.

The following pictures show where the extension goes, and how it looks once it has been plugged in: 

![](../.gitbook/assets/image%20%2879%29.png)

![](../.gitbook/assets/image%20%282%29.png)

#### Base Connections

![](../.gitbook/assets/image%20%288%29.png)

Without the fans, the QuadFusion has six main wires coming from it. The four wires with yellow dots at the ends are the motor wires. The wire with a green dot is the heater wire, and lastly the wire with the red dot is the PT1000 \(or thermistor\). 

The wires plug in to their corresponding color that is boxed in the following picture:

![](../.gitbook/assets/image%20%2860%29.png)

Notes:

* Keep in mind when you're wiring your QuadFusion's motors to the Duet Maestro board which motor is connected to which port. The first picture in this guide labels each port as E0 Stepper, E1 Stepper, E2 External Driver, and E3 External Driver. When facing the front of your QuadFusion, the front left motor is 0, the front right motor is 2, the back left motor is 1, and the back right motor is 3. 
* If you decide to extend the wires given to you, make sure that you are maintaining the original positive and negative wires. 

