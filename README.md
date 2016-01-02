# Intel-Edison-Getting-Started
Instructions on how to get the board up and running on OS X Yosemite 10.10.5 with the mini breakout board. There's more than enough tutorials, walkthroughs, etc. for RPi, BBB and the others but had to go to several different sites for the Edison. Also, a good deal of info that's available focuses on the Arduino expansion board.

#INSTRUCTIONS
1. Download PhoneFlashToolLite_5.3.2.0_mac64.pkg (http://downloadmirror.intel.com/25384/eng/edison-iotdk-image-280915.zip)

2. Download edison-iotdk-image-280915.zip which it contains Yocto 2.1 (http://downloadmirror.intel.com/25384/eng/PhoneFlashToolLite_5.3.2.0_mac64.pkg) 

3. Assemble the board. Put the module on the breakout board, lining up the holes on the module with the screws on the breakout board. Press down on the module at the upper left corner and just below the words "What will you make?" until you feel it click into place. Use the 2 hex nuts to secure the module to the expansion board.

4. Get a microUSB to USB cable (these cables are commonly used to charge phones so don't go out & buy them if you have several laying around). Plug in one end of the cable to the bottom USB connector on the expansion board. Plug in the other end of the USB cable to your Mac. A green light should light up on the expansion board. You'll know it's finished when your Mac mounts a new drive (you should see 'Edison' pop up on the screen)

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

7. Flash firmware with Phone Flash Tool Lite. BE SURE TO POWER OFF THE BOARD FIRST. The aren't specific instructions on how to do so, but you can just unplug the bottom USB cable. Launch Phone Flash Tool Lite. Click Browse, then navigate to and select the edison-iotdk-image-280915.zip file you downloaded earlier. Flash Tool Lite will automatically unzip and locate the correct FlashEdison.json file to use. Once you see the FlashEdison.json file loaded look immediately to the right & at the word Configuration & select CDC from the drop down menu. 

7. Setup serial communication. Open a terminal window & enter ls /dev/cu.usbserial-* OR ls /dev/tty.*

8. Find the entry that ends in /dev/cu.usbserial-XXXXXXXX OR /dev/tty.usbserial-XXXXXXXX
