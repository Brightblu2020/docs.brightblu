---
title: Firmware Update Instruction
layout: default
nav_order: 1
parent: Communication Controller
grand_parent: Jolt Business
---

JOLT Business

# BRIGHTBLU Communication Controller Firmware Update Guide

This guide will walk you through the process of updating the firmware on your BRIGHTBLU Communication controller using the ESP Flash Download Tool.
Only do this if you are sure / have experience of doing this before. If you are not sure how to proceed, please contact BRIGHTBLU support at in.support@brightblu.com

## Prerequisites

Before you begin, ensure you have the following:

- BRIGHTBLU Communciation Controller
- Micro-USB cable
- Computer with Windows operating system
- ESP Flash Download Tool (version 3.8.5 or later)
- Firmware files (Download:  <a href="JoltBusinessCommunicationController.html"> Here </a>)
- PuTTY (for verification)

Note:
* For Communication Controllers which are <b>Wroom-32</b>: the firmware version for this version will always be v4.x.xxx.
* For Communication Controllers which are <b>Wrover-IE</b>, the firmware version for these units will always be v5.x.xxx .



## Steps to Update Firmware

### 1. Download and Set Up the Flash Tool

1. Download the Flash Download Tool from:
   <a href="https://www.espressif.com/en/support/download/other-tools"> Here </a>
   <br>
   Look for "Flash Download Tools(ESP8266 & ESP32 & ESP32-S2)".
2. Extract the downloaded file.
3. Locate and run the file named "flash_download_tool_x.x.x.exe".

### 2. Configure the Flash Tool

1. In the initial window, select "Developer Mode".
2. In the next window, choose "ESP32 DownloadTool".

### 3. Prepare the Firmware Files

1. Download the firmware files attached to the email.
2. Save them to a folder on your computer.

### 4. Configure and Flash the Firmware

1. In the ESP32 DownloadTool interface, add the firmware files in this order:

    - Click "..." button, navigate to the file, enter the address, then check the box next to the file name.

            For Wroom-32
                * boot_app0.bin : 0xe000
                * bootloader_dio_40m.bin : 0x1000
                * firmwarev4.x.xxx.bin : 0x10000
                * partitions.bin : 0x8000

            For Wrover-IE
                * bootloader.bin 0x1000
                * partitions.bin 0x8000
                * ota_data_initial.bin 0x11000
                * firmwarev5.x.xxx.bin 0x20000

2. Set the following configuration:
   - SPI SPEED: 40MHz
   - SPI MODE: DIO
   - FLASH SIZE: 32Mbit
   - Do not select any other options

3. Select the correct COM port for your controller.
4. Set the BAUD rate to 115200.
5. Click the "ERASE" button to erase all contents on the chip. Once Successful you may proceed with flashing the controller
6. Click the "START" button to begin the flashing process.
7. When prompted (Sync), press and hold the 'BOOT' button on your controller, then release it once the tool enters 'Download' mode.
8. Wait for the flashing process to complete. You should see a success message when it's done.

### 5. Verify the Update

1. Open PuTTY.
2. Open the Serial Port connected to your controller.
3. Set the BAUD Rate to 115200.
4. Check the output to confirm the new firmware is running correctly.

## Troubleshooting

If you encounter issues during the update process:

- Ensure you've selected the correct COM port.
- Double-check that you're using the correct firmware files and addresses.
- If the controller isn't detected, try putting it into download mode manually (hold the BOOT button while connecting or resetting).
- Make sure you have the latest version of the ESP Flash Download Tool.

## Conclusion

You have successfully updated the firmware on your BRIGHTBLU Communication controller. If you encounter any issues or have questions, please contact BRIGHTBLU support in.support@brightblu.com.
