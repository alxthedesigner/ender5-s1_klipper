
# Raspberry Pi + Klipper Setup for Ender 5-S1 (No Sonic Pad)
## Install Klipper & Mainsail interface with raspberry pi imager
1. Select raspberry pi Lite Os and set up password protection on the Raspberry Pi by going to Settings. Change or keep the hostname and username. 
2. Write to SD card. When finished, insert SD into raspberry pi
3. Ping the hostname using your username chosen in the settings from step 1: **ping hostname.local**
4. Copy IP address and ssh into the pi: **ssh username@ip_address**
5. Download Kiauh. Install Klipper, Moonscraper, and Mainsail
6. Access Mailsail from browser - use hostname.local you pinged earlier to access Moonsail web interface: http://klipperpi.local

## Build & flash firmware for the 3D Printer
After installing Klipper, Moonscraper, and Mainsail, the 3D printer needs to run the Klipper firmware. The Ender 5-S1’s original firmware is Marlin, so we need to build and flash the Klipper firmware onto the machine to replace it.

### Build Firmware
7. Download the printer.cfg file from trhis repo. For other printers, look up your 3D printer’s config file here 
8. The commented out section at the top of the config file should show the mainboard details. The Ender 5-S1 runs Creality serial 64-bit motherboard (ARM STM32F401 CPU) and PA10/PA9
9. Run Kiauh. Go to: **Advanced > Build only (under Firmware)**
10. Input the mainboard details from the config file
Ender 5-S1 settings:
- Micro-controller: STM32
- Processor: STM32F401
- Bootloader Offset: 64KiB
- Comm Int: Serial on USART1 PA10/PA9
12. Press enter; this will build the firmware on the Raspberry Pi and create a klipper.bin file. The .bin file is located at out/klipper.bin 

### Flash Firmware
After building Klipper firmware you must copy the klipper.bin from your pi to your computer so you can put the klipper.bin on an SD card, and then SD card will then be placed into the 3D printer to flash it. A printer.cfg file is then needed for Mainsail to talk to your printer. 
The klipper.bin file and the STM32F4_UPDATE folder containing the printer.cfg are available to download from this project, but you can follow these directions to do it yourself with Mainsail

13. Copy Klipper firmware from out/klipper.bin to the klipper config folder accessible by Mainsail: **cp klipper/out/klipper.bin /home/<raspberrypi_username>/printer_data/config**
14. Download the klipper.bin to your computer from the Mainsail interface: **Machine > klipper.bin > download**
15. From your computer, wipe the SD card using Disk Utility on Mac if card is not empty. Change directory into SD card: **cd /Volumes/<sd_card_name>**
16. Create a file named STM32F4_UPDATE on the SD card and place the klipper.bin file inside of it
17. Insert the SD card into 3D printer, power on printer, and flashing will begin automatically. Screen will go black and stay black with Klipper software. After 2 minutes power off 3D printer and back on again
18. Download a printer.cfg file for your specific 3D printer and upload it to Mainsail
19. Run a Firmware Restart and visit the Mainsail Dashboard to see your printer

## Sources
- Video on Klipper flashing with Kiauh and Mainsail: https://www.youtube.com/watch?v=-SYqTW7wJTo
- Gist with Ender 5-S1 settings: https://gist.github.com/chouch0u/dd4f1f739635d9eca3b19ec7f60686a7
- Reddit post from @killinmesmalls with settings and specialized printer.cfg file https://www.reddit.com/r/ender5/comments/118v3eu/klipper_make_config_settings_for_ender_5_s1/

Thank you for everyone who contributed to these sources - quite literally couldn't have put it together without you.
