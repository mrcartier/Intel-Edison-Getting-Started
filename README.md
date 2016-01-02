# Intel-Edison-Getting-Started
Instructions on how to get the board up and running on OS X Yosemite 10.10.5 with the mini breakout board. There's more than enough tutorials, walkthroughs, etc. for RPi, BBB and the others but had to go to several different sites for the Edison. Also, a good deal of info that's available focuses on the Arduino expansion board.

#INSTRUCTIONS
1. Download PhoneFlashToolLite_5.3.2.0_mac64.pkg (http://downloadmirror.intel.com/25384/eng/edison-iotdk-image-280915.zip)

2. Download edison-iotdk-image-280915.zip which it contains Yocto 2.1 (http://downloadmirror.intel.com/25384/eng/PhoneFlashToolLite_5.3.2.0_mac64.pkg) 

3. Assemble the board. Put the module on the breakout board, lining up the holes on the module with the screws on the breakout board. Press down on the module at the upper left corner and just below the words "What will you make?" until you feel it click into place. Use the 2 hex nuts to secure the module to the expansion board.

4. Get a microUSB to USB cable (these cables are commonly used to charge phones so don't go out & buy them if you have several laying around). Plug in one end of the cable to the bottom USB connector on the expansion board. Plug in the other end of the USB cable to your Mac. A green light should light up on the expansion board. You'll know it's finished when your Mac mounts a new drive named Edison.

5. Get another microUSB to USB cable. Plug in the second cable to the top USB connector on the expansion board. 

6. Remove old images. Open up a new Terminal window. Enter the command:
cd /Volumes
To remove all visible files and folders, enter the command:
rm –rf Edison/*
To remove all hidden files and folders, enter the command:
rm –rf Edison/\.*
Note: If you get a message stating that rm: “.” and “..” may not be removed, this is expected. The “.” and “..” entries are special links to the current directory and parent directory, which may not be removed.
To view files on the mounted Edison drive, enter the command:
ls -lag Edison.
Verify that the files have been removed.

6. Install Phone Flash Tool Lite. Double click the PhoneFlashToolLite_5.3.2.0_mac64.pkg you downloaded earlier. Be sure to click continue/install in the pop up window to finalize installation (you should not have to open FlashToolLite.dmg or drag Flash Tool Lite into the Application folder as suggested in other tutorials). Once it's done you'll see Phone Flash Tool Lite in the Applications folder.

7. Flash firmware with Phone Flash Tool Lite. BE SURE TO POWER OFF THE BOARD FIRST. There aren't specific instructions on how to do so, but you can just unplug the bottom USB cable. Launch Phone Flash Tool Lite. Click Browse, then navigate to and select the edison-iotdk-image-280915.zip file you downloaded earlier. Flash Tool Lite will automatically unzip and locate the correct FlashEdison.json file to use. Once you see the FlashEdison.json file loaded look immediately to the right. In the Configuration drop down menu select CDC (BE SURE TO SELECT IT AS RNDIS IS FOR WINDOWS). Click 'Start to Flash', you should get a message from Flash Tool Lite telling you to plug in the board so do it. Wait for the process to complete, you should set 100% inside a bright green rectangle & beside it how long the flashing took to finish. Most people state it only takes 3 - 4 mins to flash but my board took a little over 6 mins so be patient. You also may get a message stating the board will automatically reboot after the flashing completes. I waited over 10 mins & mine never rebooted on it's own??? Eventually just unplug the bottom USB connector for a few seconds, then power the board again like you did in Step 4 (wait for the Edison to mount again)

8. Setup serial communication. Open a terminal window & type 'ls /dev/cu.usbserial-*'. Find the entry that ends in /dev/cu.usbserial-XXXXXXXX (a sample entry would read /dev/cu.usbserial-A402YSYU). In the terminal window type 'screen /dev/cu.usbserial-XXXXXXXX 115200 –L'. At the blank screen, press Enter (if you have an old version of the firmware, you have have to press Enter twice). A login screen is displayed. At the login prompt, type 'root' and press Enter. Press Enter when prompted for a password. Type 'configure_edison --password' to setup a password & then type 'configure_edison --setup' to change the name of your board & connect to wifi. Additional wifi instructions are in the next steps.

9. Connect to wifi. (If you chose not to do 'configure_edison --setup' in previous step, in terminal window type 'configure_edison --wifi', wait for Edison to scan & display a list of available networks when finished.) Locate the network you would like to connect to in the list and enter the corresponding number in the prompt. Press Enter. To confirm your entry, type “Y” and press Enter. If your network requires a password or other information, enter the appropriate network credentials. The board will attempt to make a connection to the network. When you see a Done message, your board is connected to a Wi-Fi network. You should see the board IP address in the terminal window but you can always type 'ifconfig' or 'ip a' while in the terminal. The IP address will be under the wlan0 entry. Verify connection in a browser by typing 'xxxx.local' where xxxx is the name of your device displayed in the terminal line. A sample is root@yourboardname:~#, so for that device you would enter yourboardname.local in the browser.

I purposefully skipped the installation of an IDE (Arduino, Intel or Eclipse are you choices) because it's possible to use Edison without one. However for those who need an IDE, installation would occur between steps 5 & 6, prior to flashing the firmware but after intial power on & drive mount. Link to the IDEs: https://software.intel.com/en-us/iot/software/ide. Also, Intel provides an integrated installer (https://downloadmirror.intel.com/25384/eng/m_iot_dev_kit_2015.0.026.tar.gz) which is to install and IDE & flash the firmware.

