# Network Setup

Connecting to your Promega via your local network is very useful as you get access to the Duet Web Console. You can connect your Promega to your local network via the ethernet port on the Duet Maestro. Once the network settings are properly configured, you should be able to connect to the Duet board and access the Duet Web Console. In order to configure your network settings you will need to edit files on the microSD card. The ProMega microSD card has a configuration file called _config.g_ in the _sys/_ folder. This file contains all the necessary information in order to connect to your network. The pre-configured ProMega network settings, which are loaded onto every SD card when the printer goes out our door, utilize DHCP in order to get an IP address from your router. This should allow your printer to connect automatically to your network. If this is successful, you should be able to enter the machine name into your browser tab followed by a forward slash "/". This could look like this: **my\_promega\_name/**. If you are connecting to your promega for the first time, you should be able to enter **promega/** into a browser URL textfield in order to connect. It is also possible to set a static IP address for your ProMega, this will allow you to connect to that IP address to connect to your printer. For Example, a static IP address could be the following: _192.168.1.144_ or _10.0.0.214_. However, the type of IP address is dependent on your network. Follow the steps below in order to configure your network settings using microSD or USB. We recommend using the SD option as it requires less work and setup. If you are unable to connect your Promega to your internal network, follow the Network Bridging section below.

#### Connecting to the ProMega via SD

1. Before removing your microSD card from your printer we recommend you turn off your printer. This reduces the risk of damaging your Duet Maestro. Once the printer is powered off, press the SD card into the board in order to remove it. For more guidance on the SD card check out [this guide.](http://promega.printm3d.com/books/user-manual/page/sd-card)
2. Insert the microSD card into your computer with the microSD card reader. Open the _config.g_ file. This file will be in the _sys/_ folder. It is best to open the config.g file with a text editor like [Notepad++](https://notepad-plus-plus.org/download/v7.5.6.html) or WordPad \(Default Windows Accessory\). The default Windows Accessory _Notepad_ is not recommended as it does not separate the G-code commands into individual lines.
3. There are two options for configuring your network: DHCP and static IP. If you utilize DHCP, your network will assign the control board an IP address. You will then be able to connect to the printer using the printer name you define in the configuration file. **DHCP is the recommended option if you are unfamiliar with networking.** Using a static IP means that you give the Promega a unique and free IP address on your network. You will then be able to connect to the Promega by entering that IP address into a browser tab.

   **DHCP**

   a. Open the file _machine\_access.g_ and find the `M550` command located in this file. The `M550` command sets the machine name, this command syntax requires a P parameter before the machine name. Therefore, if you wanted to name your printer _unicorn_ you would type `M550 Punicorn`. Change the printer name to something you prefer, remember this name as you will use it to connect to your printer.

   b. Find the `M552` command in the _machine\_access.g_ file. The `M552` command sets your IP address and enables or disables the network. In order to set your network setting to DHCP, the following command should be entered: `M552 P0.0.0.0 S1`. The P parameter allows you to define an IP address, entering `P0.0.0.0` enables DHCP. The S parameter enables \(`S1`\) or disables \(`S0`\) network, because you are setting up your network you should set the parameter to `S1`.

   c. Ensure that the other `M552` command is commented out!

   Your _machine\_access.g_ file network settings could look like this:

   ```text
    ; machine_access.g
    ; June 29, 2018

    ; Set the machine name and IP address in here

    M111 S0                       ; Debugging off
    M550 Punicorn                 ; Set machine name, in this case typing unicorn/ would connect you to the printer

    ; M551, No Machine Password
    ; M540 PBE:EF:DE:AD:FE:ED     ; Set MAC address, this can be used to assign a given IP in the DHCP
    M552 P0.0.0.0 S1             ; Use this to enable DHCP
    ; M552 P192.168.1.112 S1     ; This would set a static IP address but it is commented
   ```

   In the example above your machine name would be _unicorn_.

   **Static IP Address**

   a. Find the network section in the _machine\_access.g_ file. Find the `M552` command. This command sets your IP address and enables or disables the network. In order to set your network setting with a static IP the following command should be entered: `M552 Pn S1`. Where _n_ is your preferred IP address. Your IP address depends on your local network. It could be in the form of \(_192.168.1.216_ or _10.0.0.216_\). The S parameter enables \(`S1`\) or disables \(`S0`\) network, because you are setting up your network you should set the parameter to `S1`.

   ```text
   b. Ensure that the other `M552` command is commented out!

       Your *machine_access.g* file network settings could look like this:
   ```

   ```text
    ; machine_access.g
    ; June 29, 2018

    ; Set the machine name and IP address in here

    M111 S0                       ; Debugging off
    M550 PPromega                 ; Set machine name, type promega/ in your browser!

    ; M551, No Machine Password
    ; M540 PBE:EF:DE:AD:FE:ED     ; Set MAC address, this can be used to assign a given IP in the DHCP
    ; M552 P0.0.0.0 S1             ; Use this to enable DHCP, in this case commented
    M552 P192.168.1.112 S1        ; Set Static IP address and enable networking
   ```

   In the example above you should be able to connect to your printer by entering the IP address 192.168.1.112 in your browser tab.

   > If you want to find out the structure of your internal IP address, open a command prompt on a computer connected to the same network as the promega and enter the command `ipconfig`. \(Open a command prompt by pressing _Windows Key_ + _R_, type _cmd_ and press _Enter_\). This will print your network settings and status, look for the "IPv4 Address" number. That number represents an internal IP address on your network. Of course this IP address is occupied by your computer and therefore not a valid IP address for your Promega! ![kJe3IhIAIOE1puFU-ipv4address.PNG](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/kJe3IhIAIOE1puFU-ipv4address.PNG)

4. When you have made the necessary changes to your network settings, save the _machine\_access.g_ file and safely eject the SD card. Insert the SD card back into the Duet board. Ensure that the Ethernet cable is connected properly to the Duet board and turn the board back on. It will take a while for your printer to boot and connect to the network \(~30 seconds\). When your ethernet cable is properly connected to the board, the green LED should be flashing and the yellow LED should be solid. ![1NXuMREA7qVlTdEd-flashingethernet.gif](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/1NXuMREA7qVlTdEd-flashingethernet.gif)
5. Once your printer has had the time to start up, open a browser tab on a computer **connected to the same network as the printer**. In the browser URL textfield enter:
   * Your printer name followed by a forward slash "/" if you used DHCP. For example, `unicorn/`, if you named your printer "unicorn" \(nothing wrong with that!\).
   * Your printer IP address if you used a static IP address with the M552 command. It could look like this `192.168.1.216`.
6. If the connection is successful the Duet Web Console should be shown. You have completed the network setup.

Continue on to the [Accessing Web Interface](http://promega.printm3d.com/books/user-manual/page/accessing-web-interface), the next chapter in the [Getting Started](http://promega.printm3d.com/books/user-manual/chapter/getting-started) guide.

**Network Bridging**

If you are unable to connect your ProMega to your internal network it is possible to use the ethernet cable to connect the printer directly to your computer. In order to do this, complete the _Connecting to the Promega via SD: Static IP_ section, remember the static IP you give the printer, but instead of connecting the ethernet cable to your network, connect it to your computer and follow the guide below.

**Windows**

1. Open Network Connections, you can do this by opening the _Control Panel &gt; Network and Internet &gt; Network and Sharing Center &gt; Change adapter settings_

    ![ixszFpYVwOAR4Mn3-networkandsharing.PNG](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/ixszFpYVwOAR4Mn3-networkandsharing.PNG)

2. Once you have the _Network Connections_ window open. Here you will see your network adapters. The ethernet adapter represents your connection to the Duet board. Find your current network adapter, presumably a WiFi adapter. Ctrl + click both the Ethernet adapter as well as the current network you are using. Then right click on one of the selected adapters and select _Bridge Connections_.

   ![ztReV3zkFYeyGJ7s-networkbridge.png](http://promega.printm3d.com/uploads/images/gallery/2018-06-Jun/scaled-840-0/ztReV3zkFYeyGJ7s-networkbridge.png)

3. This will create a new Network Adapter called _Network Bridge_. You should now be able to connect to the ProMega with the static IP address you determined earlier. Enter the static IP address into a browser URL textfield.

Continue on to the [Accessing Web Interface](http://promega.printm3d.com/books/user-manual/page/accessing-web-interface), the next chapter in the [Getting Started](http://promega.printm3d.com/books/user-manual/chapter/getting-started) guide.

#### Connecting to the ProMega via USB

We recommend setting up your network settings via microSD card as outlined in the section above. However, if you prefer doing it via USB follow the steps below!

1. The Duet Maestro board on the ProMega has a micro USB port which can be used to connect to your computer's USB port. Connect a micro USB to USB cable to the Duet board and your computer. You do not need to power on your ProMega yet as the USB will provide power to the board.

   ![9T2BKQ7jPKK8CgId-duetMaestro.jpeg](http://promega.printm3d.com/uploads/images/gallery/2018-05-May/scaled-840-0/9T2BKQ7jPKK8CgId-duetMaestro.jpeg)

   **Installing Drivers**

2. Now that the cable between the Duet Maestro and your computer is connected you can continue below. If you are running Mac OSX you can proceed to step 3.a.

   Press the Windows Key + R in order to open the windows run prompt. Type in devmgmt.msc and press Enter. This should take you to Device Manager. The Duet should show up as a device in the device manager under _Ports \(COM & LPT\)_. The Duet can either show up as a Duet device or a USB Serial Device. Continue to 3.b.

   **Launching the Terminal**

3. a. _Mac OSX Only:_ Open application &gt; Utilities &gt; Terminal. Enter "ls /dev/tty.\* " and press Enter. The terminal will print out a result. Copy the USB name. It will most likely be in a format similar to "/dev/tty.usbmodem1410". In the terminal, run " screen /dev/tty.usbmodem1410 115200". Where "usbmodem1410" should be the name you obtained from the terminal previously. If this command runs successfully you are connected to the printer. When this step is completed, continue to Step 5.
4. b. _Windows Only:_ The next step is to download YAT \(Yet Another Terminal\) from here: [https://sourceforge.net/projects/y-a-terminal/](https://sourceforge.net/projects/y-a-terminal/). Complete the installation and proceed to the next step.
5. _Windows Only:_ Next, you have to connect YAT to the ProMega. Open YAT and configure it to the correct COM\# port. Where \# is a number representing the COM port number. The COM port that should be selected depends on which USB port you connected the cable to. You can use the device manager, as shown in step 2, in order to find out which COM port the Duet is connected to. The Duet will be listed under Ports \(COM & LPT\) as USB Serial Device. Under Text Settings, set the end-of-line sequence to LF.

**Configuring the Network Module**

1. To continue, enable the network module. This can be done by sending the command "M552" to the Duet board. This will return the status of the network module. If the module is disabled, send the command "M552 S0" in order to switch it to idle mode. If you have Duet Wifi, continue to Step 6. If you have the Duet Ethernet, continue to Step 7.
2. Wifi Setup: In the terminal \(YAT or the Mac OSX terminal\) enter the command "M587 S"your-network-ssid" P"your-network-password". Where your network name and password are entered in between the quotation marks. The SSID and password are case sensitive so be sure to enter the exact characters of the SSID and the network password. Once this step is completed, send the command "M552 S1", which will activate the network module. Once this command is entered, a confirmation message should appear and the setup is completed. Continue to step 8 in order to see how to connect to your Duet via your web browser.
3. Ethernet Setup: In the terminal \(YAT or the Max OSX terminal\) enter the command "M552 S1" which will activate the network module of the board. A confirmation message should appear, indicating that the procedure was successful. Continue to the next step to see how to connect to the Duet board via a web browser.

**Connecting to the ProMega**

1. Enter the following address into your web address in order to connect to your duet: "[http://your-ip-address-here/](http://your-ip-address-here/)", where your-ip-address-here is your IP address. For example: "[http://192.168.1.216/](http://192.168.1.216/)" could be a working address. Next you will be brought to the Duet homepage. This displays all kinds of different information about the ProMega. Go to **\_\_** page in order to learn more about the web interface. In order to ensure that you are able to connect to the Duet if you reset or power cycle the board, you need to enter "M552 S1", into the config file. To open the config file, go to Settings &gt; System Editor &gt; config.g. This will open up your config.g file. Your config.g file is executed upon startup of the duet board. It contains all kinds of critical printer settings. Scan through the config.g file and ensure that the line "M552 S1" is present. Again, this line will turn on your network module for the Duet board. 

> With the P parameter, you can change your IP address to the Duet board. For example, "M552 S1 P192.168.1.216". But becareful, if you enter an invalid or occupied IP address to your network, your Duet board will not connect to the network. If this happens, you will have to connect to your board via USB in order to change your network settings with the M552 command. Additionally, you can take out your microSD card and change the line in the config.g file manually.-

This completes the network setup. If you ever need to change any network settings you can use commands such as M552 or M553 and so on as listed in the RepRap Firmware G-code wiki.

Continue on to the [Accessing Web Interface](http://promega.printm3d.com/books/user-manual/page/accessing-web-interface), the next chapter in the [Getting Started](http://promega.printm3d.com/books/user-manual/chapter/getting-started) guide.

For additional help connecting to the printer via USB and Network setup, visit the following links: 

1. [Duet3D Network Setup](https://duet3d.dozuki.com/Guide/1.%29+Getting+Connected+to+your+Duet/7) 

2. [RepRap Firmware G-Code Wiki](http://reprap.org/wiki/G-code) 

3. [M3D Support](https://printm3d.com/support) 

4. [Duet Forum](https://forum.duet3d.com/): For Duet and RepRap firmware specific questions

