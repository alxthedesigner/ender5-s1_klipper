
# Raspberry Pi + Klipper Setup for Ender 5-S1
## Set up Klipper & Mainsail interface using raspberry pi imager
1. Select raspberry pi Lite Os and set up password protection on the Raspberry Pi by going to Settings. Change or keep the hostname and username. 
2. Write to SD card. When finished, insert SD into raspberry pi
3. Ping the hostname using your username chosen in the settings from step 1: ping hostname.local
4. Copy IP address and ssh into the pi: ssh username@ip_address
5. Download Kiauh. Install Klipper, Moonscraper, and Mainsail
6. Access Mailsail from browser - use hostname.local you pinged earlier to access Moonsail web interface: http://klipperpi.local


Build & flash firmware for the 3D Printer
After installing Klipper, Moonscraper, and Mainsail, the 3D printer needs to run the Klipper firmware. The Ender 5-S1’s original firmware is Marlin, so we need to build and flash the Klipper firmware onto the machine to replace it.
Video on building and flashing
Instructions on flashing Ender 5-S1

Build Firmware
Look up your 3D printer’s config file here 
The commented out section at the top of the file should show the mainboard details. Ender 5 S1 runs Creality serial 64-bit motherboard (ARM STM32F401 CPU) and PA10/PA9
Run Kiauh. Go to: Advanced > Build only (under Firmware)
Input the mainboard details from the config file
Press enter; this will build the firmware on the Raspberry Pi and create a .bin file. File located at out/klipper.bin 

Flash Firmware
After building Klipper firmware you must get the file firmware file from your pi to your computer so you can put the firmware on an SD card. The SD card will then be placed into the 3D printer and flashed onto it. 
Ender 5-S1 settings:
Micro-controller: STM32
Processor: STM32F401
Bootloader Offset: 64KiB
Comm Int: Serial on USART1 PA10/PA9 
Copy Klipper firmware out/klipper.bin to a klipper config folder accessible by Mainsail web interface: cp klipper/out/klipper.bin /home/<raspberrypi_username>/printer_data/config
Access klipper.bin within Mainsail and download to your computer from Mainsail Interface: Machine > klipper.bin > download
Wipe the SD card using Disk Utility on Mac if card is not empty. Change directory into SD card: cd /Volumes/<sd_card_name>
Create a file named STM32F4_UPDATE and place the klipper.bin file inside: mkdir STM32F4_UPDATE 
Insert the SD card into 3D printer, power on printer, and flashing will begin automatically. Screen will go black and stay black with Klipper software
After 2 minutes power off 3D printer and back on again
Download a printer.cfg file for your specific 3D printer and upload it to Mainsail
Run a Firmware Restart and visit the Mainsail Dashboard to see your printer