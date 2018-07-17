---
description: Update the contents of the Duet Maestro microSD card.
---

# Updating SD Card Structure

While your printer was being shipped, it is possible that a new SD card structure was released. More explanation of the SD Card files can be found in the next guide. To ensure that you have the latest files on your SD card, please follow the guide below. 

## M3D Release SD Card

The latest SD card files released by M3D can be found on the [M3D Github ProMega Repository](https://github.com/PrintM3D/Promega). Follow the steps below in order to download the latest version for your printer. Always be careful when downloading the latest version of the SD card files. New SD card files can cause unintended results such as flipped motor directions or wrongly configured heaters. **Always test all motors and heaters carefully before printing after downloading a new update.**

Read the [Accessing Your SD Card](https://m3d.gitbook.io/promega-docs/getting-started/accessing-your-sd-card) for more help on getting to the SD card files.

Read the [SD Card Structure](https://m3d.gitbook.io/promega-docs/getting-started/sd-card-structure) guide for more explanation on the files and directories on the SD card.

{% tabs %}
{% tab title="Downloading Official Release" %}
## Downloading Official Release

This is the recommended option.

Go to the [M3D GitHub Promega Repository Releases](https://github.com/PrintM3D/Promega/releases) and download the latest release. Download the _.zip_ folder for the extruder head that you currently have mounted. The Promega can come with either the K'tana \(two nozzles\) or the compound \(1 nozzle\).

![Downloading the Latest Release](../.gitbook/assets/wheretoinstallnewsdstuff.png)
{% endtab %}

{% tab title="Downloading Directly from the Repository" %}
## Downloading Directly from Repository

This option is not recommended, but it will allow you to get the latest configuration files, regardless of official release. This is not the recommended option. Once you have found and opened the [M3D Github ProMega Repository](https://github.com/PrintM3D/Promega). Press the _Clone or download_ button circled below and then click _Download ZIP_. This will download a _.zip_ file of the repository.

![Downloading from Github](../.gitbook/assets/s8aq28iyeh4lw9ww-howtodownloadgithub.png)
{% endtab %}
{% endtabs %}

## Extracting the Folder

A _.zip_ file is a compressed folder. You will have to first extract the file before you can get to it's contents. Find the file you just downloaded and extract it into a folder. Right click the file and then select _Extract All_. This will move all the files in the compressed file into a folder. You can now access the new SD card files.

![RZHiyY0qCUmtoUtP-ExtractingTheZip.png](../.gitbook/assets/rzhiyy0qcumtoutp-extractingthezip.png)

## Moving the Files onto the SD Card

**Back-up your SD card files before updating so you can always revert to your original settings**. Now that you have access to the files, locate the _SD Card Structure_ folder in the folder you just extracted. This folder will have two folders _Compound_ and _K'Tana_, select the folder based on what nozzle you currently have mounted on your printer. In both of these folders are the files you want to copy to your microSD card. This should be four folders: _sys, gcodes, macros_ and _www_. Plug in the microSD card into your computer with the microSD card reader and copy the files onto it. Your SD card should look like this. Using WinDiff or a similar program to distinguish differences between the latest SD card release and your files might be a good idea.

![Fv3qaHUEgAGLL4np-SDCard.png](../.gitbook/assets/fv3qahuegagll4np-sdcard.png)

## Testing and Tuning

Once you have updated the SD Card files on the microSD card. Test all your motors and heaters one by one to ensure the new settings are compatible with your wiring and board. If you changed any settings in your previous configuration, you will have to add these settings and commands in your new updated version. If any of the motors or heaters are flipped, [this guide](../firmware-guides/help-my-extruders-are-backwards.md) will help.

