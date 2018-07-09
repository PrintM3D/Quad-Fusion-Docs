# Firmware vs. SD Card Files

This guide is intended to explain the difference between the firmware on the board and the SD card files.

### Firmware

The firmware on the board is a version of RepRap released by DC42. The firmware is released on his [GitHub Releases](https://github.com/dc42/RepRapFirmware/releases). If you want to update your firmware, you can follow the [Updating Firmware](http://promega.printm3d.com/books/user-manual/page/updating-firmware) guide. The RepRap firmware on the board interprets all the G-code commands sent to the board. It is stored on the micro-processor on the Duet Maestro and required for the board to operate. The firmware handles low-level operation such as controlling the stepper motor drivers or processing G-code commands. Changing the firmware directly is not possible, you will have to update the firmware using the guide above.

### SD Card

The SD card stores files that allow for the operation of the Duet Web Server and configure the board. The microSD card has four different folders that each handle a certain part of the Duet board operation \([SD Card Structure](http://promega.printm3d.com/books/user-manual/page/sd-card-structure-05f)\). The SD card files operate on a higher level. The files located in the _sys_ folder, configure the board. They can be changed by the user at any time, either through the Duet Web Console or by changing the files from your computer. The configuration files often simply represent a grouping of G-code commands that are run upon the boot of the Duet board. When you download the SD card file from the M3D Github Repository, you are just taking the M3D preferred settings for the Promega. Finding these settings on your own is possible.

