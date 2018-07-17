---
description: How to properly prepare a 3D print.
---

# Preparing a Print

Before uploading a print to the Duet board and printing it with the Promega, you will need to prepare a _.gcode_ file of your model. The first step to preparing a print involves creating a _.STL_ file. This file is a representation of the outer shell of a CAD \(Computer Aided Design\) model. An _.STL_ file can then be sliced by slicer software such as _Cura_ or _Simplify3D_ \(and many others!\) to produce a _.gcode_ file. Slicer software will incorporate numerous print and printer settings into the G-code print file. You can then upload this file to your printer to print it. Properly preparing a print is very important to produce a print with good print quality. Follow this guide to create a _.gcode_ file with the proper print settings. If you are already familiar with creating an _.STL_ file, you can continue to [Preparing a Print](https://m3d.gitbook.io/promega-docs/getting-started/preparing-a-print#cura).

**Note: if you want to quickly get printing for the first time you can find a pre-sliced** G-code file of a [**rook model here**](https://drive.google.com/open?id=1PK1snlv7iPuX1XC8wjrwxUQiDmN8HcHH)**, this is recommended if you are printing for the first time. Once you have downloaded the model you can continue to:** [**Running a Print**](https://m3d.gitbook.io/promega-docs/getting-started/running-a-print)

Below you will have the option of creating a _.STL_ file or finding one from the internet.

## Finding an _.STL_ File

It is possible to create your own _.STL_ file by downloading a CAD \(Computer Assisted Design\) software such as SolidWorks or [TinkerCAD](https://www.tinkercad.com/). An easier initial step is to download a working model from the internet. This is because multiple constraints of the 3D printer have to be taken into account when designing a model for printing with a 3D printer. Downloading a model is much easier. There are many different websites such as [Thingiverse](https://www.thingiverse.com/), [Pinshape,](https://pinshape.com/) [MyMiniFactory](https://www.myminifactory.com/) and many others!

Go to one of the websites listed above and download a _.STL_ model of something you would want to print. For the example below I used the model: [Customizable Yin-Yang Planter / Container](https://www.thingiverse.com/thing:2531208) by [Lucina M](https://www.thingiverse.com/Lucina/about) from Thingiverse. Follow the red markings below. Click Thing Files and then click the models you want to download the ._STL_ files of. These files will then end up in your downloads folder.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHE-lyuMwBirREkEIi_%2F-LHE8o3TpybTjjyGm5mp%2Fhowtothingiverse.png?alt=media&token=4b2cc5dc-6b3f-4940-8499-1fa7b0f614d1)

## Creating an STL File

In most CAD software you can choose to save a model in the _.STL_ file format. When creating this file, it is important to remember that an STL represents the shell of the CAD model. It is possible that minute details are changed when you save in this format. Whenever you create a CAD model ensure that your dimensions are realistic and that the model will fit in the buildspace of the Promega \(388mm x 388mm x 377mm\). Typically, you will also be able to change the scale of your model in the slicer software in the next step. In most CAD software you can click _Save As_ and then save the part in the _.STL_ file format.

### SolidWorks

To save a model as an STL in SolidWorks, click _File &gt; Save As_. Then select _.STL_ as shown in the file below.  

![Saving a File as STL](../.gitbook/assets/xorbieh8qmorw6zm-saveasstl.png)

Then a window will appear, confirming the fact that you are saving the file as an STL. In the background you will see a representation of the model as an _.STL_ file. Press _Yes_ in order to save your model as an _.STL_ file.

 

![](../.gitbook/assets/fev3lghg61ntf514-solidworksstl.png)

## Finding a Slicer

There are many slicers currently available to slice your models. We recommend that you download and install one of the slicers listed below. These are the slicers which are currently supported by M3D. We have created Promega slicer profiles which will allow you to get printing better and faster. This list will keep growing over time as we create more profiles for different slicers. It is possible to use a different slicer, but you will have to spend more time tuning the slicer settings in order to print successfully. We recommend you only do this if you are an experienced Promega user.

Find the slicer profiles on [our GitHub Account.](https://github.com/PrintM3D/Promega) Supported slicers:

* [Cura](https://ultimaker.com/en/products/ultimaker-cura-software)

## Setting up your Slicer

Once you have downloaded your preferred slicer you can follow the steps below to see how to set up the slicer with the correct printer settings.

### Cura

Open Cura's Setting by pressing _Preferences &gt; Configure Cura...._

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHE-lyuMwBirREkEIi_%2F-LHEBiNF86L4EkctPJrQ%2Fconfiguringcura.jpg?alt=media&token=ba80d6e9-5823-471d-bab7-44ca1fee718c)

Once you have opened Cura's settings we will go to add a printer. This is because we need to tell Cura the specifics of our printer, such as the maximum build volume of the printer. Press _Printers_ and then _Add_ in order to add a new printer. This will open a new window.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHE-lyuMwBirREkEIi_%2F-LHECq1Z-9-5KblRRl6J%2Fconfiguringcura2.jpg?alt=media&token=19f66a4c-e797-4897-a1f2-195da83306e6)

 Next, press _Custom._ This indicates we are adding a custom printer to Cura's loadout. You can define the _Printer Name_ however you want. Then press _Add Printer,_ this should open another setting window_._

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHE-lyuMwBirREkEIi_%2F-LHEDLTDhp0R_GeMck_f%2Fconfiguringcura3.jpg?alt=media&token=20142237-8d73-482d-962b-9570a5338af7)

This window allows you to configure the printer settings of the Promega. This informs Cura of the Promega's build space, the firmware flavor and specifies starting and ending G-code. The build volume of the printer represents the maximum value that the printer can travel in each direction. The firmware flavor is the type of firmware that the board is running. The Duet Maestro board runs on RepRap firmware. Your firmware flavor indicates what type of commands the board can understand. The starting and ending G-code is a series of commands that are run at the start and at the end of every print. This is important as it allows you to retract your filament after the print and turn all the heaters off. Configure the settings in this window exactly as shown in the image below.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHE-lyuMwBirREkEIi_%2F-LHEJ_r1qobgdBJv1fgr%2Fcuramachinesettings.jpg?alt=media&token=c600f426-cfb6-468d-be01-075357663331)

`; Starting G-code: G1 Z15.0 F6000 ;Move the platform down 15mm ;Prime the extruder G92 E0 G1 F200 E3 G92 E0`

`; Ending G-code M104 S0 M140 S0 M106 S0 G28 X Y G91 G1 Z10 S1 G90 ;Retract the filament G92 E3 G1 E-3 F300`

**Don't click** _**Close**_ **just yet!** Move on to the _Extruder 1_ tab and fill in the following information. Fill in the nozzle diameter and the material diameter. Your nozzle diameter may vary in the future as you mount different types of nozzles on the Promega. Then you can click _Close._

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHE-lyuMwBirREkEIi_%2F-LHEKZXOSTGmf3CoooVo%2Fcuramachinesettings_extruder.jpg?alt=media&token=cc21a58d-480c-48d7-8ee3-aee8d89f6ec2)

Once you have added the printer make sure to activate it by selecting the name and then clicking the button _Activate._

### Importing the Printer Profile {#importing-the-printer-profile}

The next step is to go to the M3D GitHub Promega repository, in the [Cura Profiles folder](https://github.com/PrintM3D/Promega/tree/devel/Cura%20Profiles) and download the Cura profile for your extruder setup. In order to download the Cura Profile, click on the file in GitHub and then press the Download button as seen in the image below, outline in red. This profile contains all kinds of print settings that help the Promega print well. You can find and tune these settings through experimentation at a later time. For now, this default profile will work well.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJ7ti8RozJmzJ3hXmu%2Fdownloadingcuraprofile.png?alt=media&token=d24bc282-919c-432c-981b-84d86a9a37df)

In Cura, open the Preferences again by clicking _Preferences &gt; Configure Cura._ Click _Profiles &gt; Import_. Then a window will pop up that will allow you to navigate to the profile you just downloaded. It will most likely be in the _Downloads_ folder.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJ8da60a79oyKJM4oF%2FImportingCuraprofile.png?alt=media&token=59e63c98-a1da-45d2-acc6-1981a859d315)

Once you have properly imported the file you will have to _Activate_ it. Select the profile and click the button _Activate._ The print settings you just downloaded have now been applied to Cura. Whenever you slice a model, it will now incorporate these settings.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJ8gPT2VfePjBUUSyM%2Factivatingcuraprofile.png?alt=media&token=1a5e7b18-81c0-4d0f-8f64-c17edc84880d)

## Slicing your Model

Slicing your model is an extremely important step. Most slicer software allow you to control different print settings such as layer height or print speed in order to change how you print. Slicing has great effect on the quality of your print you produce. Follow the steps below for a guide on how to slice properly with different slicer software.

### Cura

#### Opening a Model

Now we will actually slice the model we downloaded earlier. First, click the folder icon _Open File_ in the top left of the window. Then navigate to the _.STL_ file you downloaded earlier and press _Open._ You should then see the model appear on your build plate.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJC5mDVU6QtaG-dSLs%2Fcurahasamodel.png?alt=media&token=022dcb03-8cd9-4f33-88d6-e049225eed0b)

In order to better view your model you can right click and drag in order to change the orientation of your model. Shift + Left Click and dragging will allow you to move the position of the camera. You can always home your view with the buttons in the top-left corner. In the image above I imported three different models.

#### Positioning the Model

Use the b~~u~~ttons on the left of the window in order to orient and position the parts as you want. Make sure to keep appropriate distance between parts. Make sure that the parts also have a sufficient flat surface of their model to adhere to the print bed. Check out the images below for more guidance on part orientation.

![This is a good print layout](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJEIDrwLkBf2BrArtM%2FMovingmodelsaround.png?alt=media&token=4ed6e874-6b06-450a-91bd-ef2604e1a706)

![Make sure models are kept apart](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJEJo1VZcRFg1eEnRh%2Fdontcurathisway1.png?alt=media&token=78578cb9-48b2-410c-8afe-0ed89698688d)

![Make sure parts are oriented correctly, this might not print correctly without support.](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJEPcsaawWWniBiGlq%2Fdontcurathisway2.png?alt=media&token=f00b408f-3fdc-4498-b16a-10d596e2f539)

### Configuring Print Settings {#configuring-print-settings}

Next, we will configure the print settings in Cura. This will all take place on the right side of the Cura window. In a tab called _Custom._

If you can't see any of the option in the steps below. Go to _Preferences &gt; Configure Cura &gt; Settings_ and change the _Setting Visibility_ to _Basic._ This will allow you to see more settings. Eventually, you can change this to _Advanced_ or _Expert_ in order to allow for more print setting options.

![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJFWGQ1yKsr6hOdyxG%2Fsettingvisibility.png?alt=media&token=b292ba4f-4243-416a-bb66-5b1ea6e81369)

The only thing you should have to configure for your first print is the _Material: Temperature Setting._ Configure this based on the material you are printing with. If you are printing with ABS-R, I recommend a temperature of 235°C and if you are printing with PLA a temperature of 205°C is fit. Fill this into the box as shown below. For my print, I am printing with ABS-R, so I filled in 235°C.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJJ3PnUHuU8ESCI6kO%2Fsettingcuratemperature.png?alt=media&token=eacd7da7-bd89-463f-b1c7-7337b017b004)

Now we are ready to slice the model. Just click Prepare in the bottom right corner. It might take a few seconds for Cura to slice the model. Click once and wait for a few seconds.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LH1ZPQUJrjMM5Ql5c--%2F-LHJ14S2auLuan3N_dt1%2F-LHJJOdS-V2O8ZEuIg7O%2Fslicingincura.png?alt=media&token=47e61b68-2641-4f6f-9077-c74634f6cb4c)

Once you have sliced the model press the _Save to File_ button. Then save the file to a location that you will remember. You will notice that the file you are saving is a _.gcode_ file which is ready to print.

You will have to tune your Slicer settings as you continue your printing career with the Promega. The slicer settings that you can find on the M3D GitHub repository are generic and work well for most prints. To have optimal print quality for your print, you will have to tune the slicer settings to your print. 

Continue on to the [Running a Print](https://m3d.gitbook.io/promega-docs/getting-started/running-a-print) guide, the next chapter in the [Getting Started](https://m3d.gitbook.io/promega-docs/getting-started) guide.

