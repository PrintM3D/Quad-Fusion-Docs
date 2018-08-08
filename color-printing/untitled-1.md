# MELT

MELT is a plugin on Cura that stands for Multi-Extruder Layering Tool. MELT’s main purpose is to take 2 - 4 extruders and manipulate their extrusion ratios in order to print a gradient design. This guide will be a step-by-step explanation on how to create a simple design with gradient using MELT. 

**Step one:**  
Once you have chosen the file you wish to have a gradient design, Click the Extensions tab --&gt; Post Processing --&gt; Modify G-Code

![](../.gitbook/assets/image%20%2888%29.png)

**Step Two:**  
Once in the Post Processing Plugin, select the "Add a script" drop down menu

![](../.gitbook/assets/image%20%2814%29.png)

Select the "Multi-Extruder Layering Tool 3.4.0 \(MELT\)"

![](../.gitbook/assets/image%20%2862%29.png)

**Step Three:**  
Starting with the basic settings, you will want to edit yours to be similar to the one below. 

![](../.gitbook/assets/image%20%2847%29.png)

**Settings Explained:**  
Number of Extruders:   
This will be for how many tools you plan on using. So, four extruders means you will be using all four filaments.  
Shifting Clamp Type:   
This can be changed based on layer no. or percentage. Thus, if you wish to change the color ratio based on layer no. or percentage you would do so here.  
Extrusion \# Start:   
This is which layer you would like to start changing the the color ratio.  
Extrusion \# End:   
This is which layer you would like to stop changing the color ratio \(e.g. The last color ratio you have before this, will be what you extruder will continue to print\).  
Shift Frequency:  
This means how long it will take to change the color ratio. 

You will want to edit these, as you continue printing in color, depending on what your print will be, how many layers it has, and how many filaments you want to use.

**Step Four:**  
Next, you will want to select "Expert Controls" and "Enable Initial Setup"

![](../.gitbook/assets/image%20%283%29.png)

Once you have selected these you will have an ability to edit more settings that will help you specifically choose which drives you want.

**Settings Explained:**  
Define Tool:  
This is a M563 command that will tell your printer which tools will be used for this print.  
Initial Main Flow:  
This tells your printer how you want your gradient to begin printing \(e.g. In the example above the plugin has the extruding starting with 100% of tool 0\)  
Final Main Flow:  
This tells your printer how you want your gradient to end printing \(e.g. In the example above the plugin has the extruding ending with 100% of tool 3\)

Step Five:  
Now that you have completed these steps, go ahead and edit your settings to your preference.   
  
You can now print the file with your QuadFusion!

