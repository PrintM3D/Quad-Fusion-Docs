# Slic3r Multi-Material

{% hint style="info" %}
Support for multi-color printing in common slicers is often limited to specific purposes or capabilities.  In this guide, we use Slic3r Prusa Edition and an M3D-developed script to make the generated G-Code compatible with a QuadFusion-enabled printer.  As slicer capabilities improve, this guide will be updated and the process will be simplified.
{% endhint %}

## You Will Need

Slic3r Prusa Edition \(link\)

NOTE: have been using 1.39.1

M3D Cleanup Script \(link\)

IPython Notebook or equivalent, such as Jupyter Notebook \(link\)



## Find \(or Create\) Multi-Part STL Set

## 

## Slice and Export

#### Load and Adjust Print Settings

#### Assign Tool Numbers

## Manual Cleanup Step

## Automated Cleanup Script

Take the .gcode file from the prior step and move it to your IPython working folder.  For example, on my system, these files are held in ~/Documents/Workspaces/\_python.  For this example, I moved the file "ed\_MAN1\_tower-of-cascades.gcode" to ~/Documents/Workspaces/\_python/Working.  \("Working" has been a convenient folder to hold the .gcode files separate from the actual IPython script file\(s\).\)

Launch IPython Notebook and load the script titled "PostprocSPEForColor4\_auto.ipynb".

Run the first three blocks of code.  \(The first is a short block defining "clamp" and nothing else; the next are much longer.\)

In the fourth code block, there is a note on values you will need to change for your particular job.  Adjust these values to your particular job.  First layer and other layer height are from your slicer setup.  The in file is the file you created in the prior step.  The out file is the .gcode file that will be created by the cleanup script and sent to the printer.

A large number of diagnostics messages will output when this code block is run.



TODO: in main -- find "def main\(\):"

