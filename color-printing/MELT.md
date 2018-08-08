# MELT

MELT is a plugin on Cura that stands for Multi-Extruder Layering Tool. MELT’s main purpose is to take 2 - 4 extruders and manipulate their extrusion ratios in order to print a gradient design. This guide will be a step-by-step explanation on how to create a simple design with gradient using MELT. 

**Step one:**  
Once you have chosen the file you wish to have a gradient design, Click the Extensions tab --&gt; Post Processing --&gt; Modify G-Code

![https://www.thingiverse.com/thing:651015/files](../.gitbook/assets/image%20%2889%29.png)

**Step Two:**  
Once in the Post Processing Plugin, select the "Add a script" drop down menu

![](../.gitbook/assets/image%20%2814%29.png)

Select the "Multi-Extruder Layering Tool 3.4.0 \(MELT\)"

![](../.gitbook/assets/image%20%2862%29.png)

**Step Three:**  
Starting with the basic settings, you will want to edit yours to be similar with the one below. 

![](../.gitbook/assets/image%20%2847%29.png)

**Settings Explained:**  
_Number of Extruders:_   
This will be for how many tools you plan on using. So, four extruders means you will be using all four filaments.  
_Shifting Clamp Type:_   
This can be changed based on layer no. or percentage. Thus, if you wish to change the color ratio based on layer no. or percentage you would select which you'd prefer.  
_Extrusion \# Start:_   
This is which layer you would like to start changing the the color ratio.  
_Extrusion \# End:_   
This is which layer you would like to stop changing the color ratio \(e.g. The last color ratio you have before this, will be what you extruder will continue to print\).  
_Shift Frequency:_  
This means how long it will take to change the color ratio. 

{% hint style="info" %}
You will want to edit these as you continue printing in color depending on what your print will be, how many layers it has, and how many filaments you want to use.
{% endhint %}

**Step Four:**  
Next, you will want to select "Expert Controls" and "Enable Initial Setup"

![](../.gitbook/assets/image%20%283%29.png)

Once you have selected these you will have an ability to edit more settings that will help you specifically choose which drives you want.

**Settings Explained:**  
_Define Tool:_  
This is a `M563` command that will tell your printer which tools will be used for this print.  
_Initial Main Flow:_  
This tells your printer how you want your gradient to begin printing \(e.g. In the example above the plugin has the extruding starting with 100% of tool 0\)  
_Final Main Flow:_  
This tells your printer how you want your gradient to end printing \(e.g. In the example above the plugin has the extruding ending with 100% of tool 3\)

**Step Five:**  
Now that you have completed these steps, go ahead and edit the remaining slicer settings to your preference.   
  
You can now print the file with your QuadFusion!

{% hint style="warning" %}
You can only change color by layer, go to the guide [Slic3r Multi Material](slic3r-multi-material.md) to find out how to change color in the same layer.
{% endhint %}

