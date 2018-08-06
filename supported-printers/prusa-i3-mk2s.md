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

![Front](../.gitbook/assets/image%20%2864%29.png)

As you can see, the front of the mount has two sets of holes, the bottom set is where you will be screwing in the two 3mm standoffs.

![Back](../.gitbook/assets/image%20%2823%29.png)

The back of the mount shows where it will be mounted to the Prusa. The lower X-belt will lie across the ledge of the mount. While the upper X-belt will be wrapped around the two protruding cylinders. You can tighten the X-belt by wrapping more of the belt around the cylinder, as shown in the picture above.   
Additionally, the mount is attached to the Prusa using six zip-ties. Theses zip-ties can be routed through designated holes that the mount contains. 

**STL File\(s\):**

\*\*\*\*

### **Electrically**

{% hint style="info" %}
You will need a Duet Maestro board if you with to follow along during the electrical part of this guide. Look at the bottom of the page to see where to get one.
{% endhint %}

This is the Duet Maestro:

![https://duet3d.dozuki.com/Wiki/Duet\_2\_Maestro\_Hardware\_Overview](../.gitbook/assets/image%20%2835%29.png)

This will be a walk through on how we hooked up the QuadFusion, as well as part of the i3 MK2S, to the Duet Maestro board.

Before you can begin to wire your QuadFusion to the Duet Maestro board you must attach an extension to the board. With this extension you will be able to connect the the extra motor wires to the board.

The following pictures show where the extension goes, and how it looks once it has been plugged in: 

![](../.gitbook/assets/image%20%2857%29.png)

![](../.gitbook/assets/image%20%282%29.png)

### Base Connections {#base-connections}

![](../.gitbook/assets/image%20%285%29.png)

Without the fans, the QuadFusion has six main wires coming from it. The four wires with yellow dots at the ends are the motor wires. The wire with a green dot is the heater wire, and lastly the wire with the red dot is the PT1000 \(or thermistor\). 

The wires plug in to their corresponding color that is boxed in the following picture:

![](../.gitbook/assets/image%20%2841%29.png)

Notes:

* Keep in mind when you're wiring your QuadFusion's motors to the Duet Maestro board which motor is connected to which port. The first picture in this guide labels each port as E0 Stepper, E1 Stepper, E2 External Driver, and E3 External Driver. When facing the front of your QuadFusion, the front left motor is 0, the front right motor is 2, the back left motor is 1, and the back right motor is 3. 
* If you decide to extend the wires given to you, make sure that you are maintaining the original positive and negative wires. 

The next steps will be to connect your i3 MK2S' stepper motors, power source, limit switches and Z-probe.

{% hint style="info" %}
The bed is not connected to the Duet Maestro board, this will be further explained in this guide.
{% endhint %}

Starting with the stepper motors, each one will plug into one of these highlighted ports:

![](../.gitbook/assets/image%20%2859%29.png)

The color coordination is as follows;  
Yellow = X-Stepper Motor  
Orange = Y-Stepper Motor  
Green = Z-Stepper Motors

{% hint style="warning" %}
The original connectors on the i3 MK2S were not compatible with the Duet Maestro. We ended up cutting off the locking mechanisms on each connector that was interfering with plugging the wires into the board.
{% endhint %}

The next step is to wire the limit switches and Z-probe to these highlighted ports:

![](../.gitbook/assets/image%20%2867%29.png)

The picture above shows where each limit switch and the Z-probe should be connected. Color coordination is as follows;  
Yellow = X-Limit Switch  
Red = Y-Limit Switch  
Aqua = Z-Limit Switch  
Green = Z-Probe

When attaching the Z-probe you will need to use some Dupont connectors in order to properly connect it to the Duet Maestro:

![](../.gitbook/assets/image%20%2843%29.png)

Color coordination is as follows:  
The black wire represents the Z-probe's black wire  
The grey wire represents the Z-probe's blue wire  
The brown wire represents the Z-probe's brown wire

Once you have plugged these in you can move on to connecting the power supply. **You will need a 24V power supply** to power your Duet Maestro board

![](../.gitbook/assets/image%20%2817%29.png)

The three circled wires are what will be connecting your power supply to an outlet. The non circled wires are what will be connected to your Duet Maestro board

{% hint style="info" %}
We recommend having an on/off switch between the power supply and Duet Maestro board, this makes it easier to turn your printer on and off. 
{% endhint %}

![](../.gitbook/assets/image%20%2856%29.png)

The red and black wires will be connected to ports 3 and 4, respectively, as shown in the image above.

**Heating the Bed**

The bed was wired separately from the main collection of wires because of the power supply. The QuadFusion requires a 24V power supply in order to properly power the motors, heater, and thermistor. However, the bed could only be safely powered by 12V, so it was decided to have the bed remain wired to Creality's original board. Because of this, you will be able to heat your bed from the control block that comes with the printer, as opposed to heating with the Duet Web Control.





Don't have something that is listed here? Check out these links if you need something for the QuadFusion!

24V power supply: [https://store.printm3d.com/collections/parts/products/400w-power-supply?variant=12283391148110](https://store.printm3d.com/collections/parts/products/400w-power-supply?variant=12283391148110)  
Duet Maestro Board: [https://fitforlaunch.com/projects/duet-2-maestro](https://fitforlaunch.com/projects/duet-2-maestro)  
Toggle Switch: [https://store.printm3d.com/collections/parts/products/lighted-toggle-switch?variant=12283706245198](https://store.printm3d.com/collections/parts/products/lighted-toggle-switch?variant=12283706245198)  


