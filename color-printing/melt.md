# MELT

This guide will go through step-by-step on how to print a simple gradient design using MELT. This guide will assume you have already downloaded MELT, and have picked your own print file.

To start, open you file up in Cura and selct Extensions --&gt; Post Processing --&gt; Modify G-Code

![](../.gitbook/assets/image%20%2837%29.png)

Next you will want to select the drop down tab "Add a Script" 

![](../.gitbook/assets/image%20%2828%29.png)

Select "Multi-Extruder Layering Tool 3.4.0 \(MELT\)"

![](../.gitbook/assets/image%20%2815%29.png)

Based upon your file you will want to edit your basic settings to fit your print. Below is how the settings were altered for this example print:

![](../.gitbook/assets/image%20%2832%29.png)

**Settings Explained:**  
_Number of Extruders:_  
This setting declares how many filaments you wish to use. With the QuadFusion, you can select up to all four filaments.  
_Shifting Clamp Type:_  
You can decided whether you want to print in gradient based on the layer number of your file, or the percentage of your file.  
_Extrusion \# Start:_  
This instruct the printer to begin the gradient at a certain layer number or a certain percentage of your file.  
_Extrusion \# End:_  
This instruct the printer to end the gradient at a certain layer number or a certain percentage of your file.  
_Shift Frequency:_  
This instructs your printer how fast or slow you want it to take to transition to the next gradient ratio. 

Next, you will want to select "Expert Controls" and "Enable Initial Setup".

![](../.gitbook/assets/image%20%2823%29.png)

**Settings Explained:**  
_Define Tool:_  
This section is a M563 command designed so the user can specifically select which drive they wish to have used when printing gradient. \(e.g. In the example above, by using Drives 0,1,2, and 3, all four filaments will be extruded in gradient\).  
_Initial Main Flow:_  
This instructs the printer what ratio it should begin the print \(e.g. In the example above, the printer will begin with printing 100% of Drive 0\)  
_Final Main Flow:_  
This instructs the printer what ratio it should end the print \(e.g. In the example above, the printer will end with printing 100% of Drive 3\)

From this point on you can edit your slicer settings however you see fit. 

