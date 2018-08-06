# Prusa i3 MK2S

This guide will go through the process of hooking up your QuadFusion to Prusa's i3 MK2S printer.

{% hint style="warning" %}
The QuadFusion and the company M3D have no affiliation with the Prusa i3 MK2S or its company.
{% endhint %}

### Mechanically

The Prusa i3 MK2S requires an entirely new extruder mount in order to mount the QuadFusion. The new mount is very similar to the old, a few things were just shifted to accommodate for the new fan mounts.

![](../.gitbook/assets/img_1390.jpg)

You will need...  
- 3mm Hex Standoffs \(20mm long\) \(x2\)  
- 3mm Hex Screw \(33mm long\) \(x2\)  
- 8mm Nut \(3mm thick\) \(x2\)  
- QuadFusion Mount  
- Zip-ties \(x6\)

Tools...  
- 2.5mm Hex Screwdriver

![Front](../.gitbook/assets/image%20%2860%29.png)

As you can see, the front of the mount has two sets of holes, the bottom set is where you will be screwing in the two 3mm standoffs.

![Back](../.gitbook/assets/image%20%2821%29.png)

The back of the mount shows where it will be mounted to the Prusa. The lower X-belt will lie across the ledge of the mount. While the upper X-belt will be wrapped around the two protruding cylinders. You can tighten the X-belt by wrapping more of the belt around the cylinder, as shown in the picture above.   
Additionally, the mount is attached to the Prusa using six zip-ties. Theses zip-ties can be routed through designated holes that the mount contains. 

**STL File\(s\):**

\*\*\*\*

### **Electrically**

{% hint style="info" %}
You will need a Duet Maestro board if you with to follow along during the electrical part of this guide. Look at the bottom of the page to see where to get one.
{% endhint %}

This is the Duet Maestro:

![https://duet3d.dozuki.com/Wiki/Duet\_2\_Maestro\_Hardware\_Overview](../.gitbook/assets/image%20%2833%29.png)

This will be a walk through on how we hooked up the QuadFusion, as well as part of the i3 MK2S, to the Duet Maestro board.

Before you can begin to wire your QuadFusion to the Duet Maestro board you must attach an extension to the board. With this extension you will be able to connect the the extra motor wires to the board.

The following pictures show where the extension goes, and how it looks once it has been plugged in: 

![](../.gitbook/assets/image%20%2853%29.png)

![](../.gitbook/assets/image%20%282%29.png)

### Base Connections {#base-connections}

![](../.gitbook/assets/image%20%285%29.png)

Without the fans, the QuadFusion has six main wires coming from it. The four wires with yellow dots at the ends are the motor wires. The wire with a green dot is the heater wire, and lastly the wire with the red dot is the PT1000 \(or thermistor\). 

The wires plug in to their corresponding color that is boxed in the following picture:

![](../.gitbook/assets/image%20%2839%29.png)

Notes:

* Keep in mind when you're wiring your QuadFusion's motors to the Duet Maestro board which motor is connected to which port. The first picture in this guide labels each port as E0 Stepper, E1 Stepper, E2 External Driver, and E3 External Driver. When facing the front of your QuadFusion, the front left motor is 0, the front right motor is 2, the back left motor is 1, and the back right motor is 3. 
* If you decide to extend the wires given to you, make sure that you are maintaining the original positive and negative wires. 

The next steps will be to connect your i3 MK2S' stepper motors, power source, and Z-probe.

{% hint style="info" %}
The bed is not connected to the Duet Maestro board, this will be further explained in this guide.
{% endhint %}



