---
title: Charge Controller
layout: default
nav_order: 2
parent: Jolt Business
grand_parent: Firmware

---


JOLT Business

Charge Controller:

The charge controller(CC) controls all the hardware systems in the charger. These systems are –

1. Control Pilot signal generation and detection of vehicle states.
2. Leakage current detection
3. Input voltage range detection
4. Continuous earth monitoring
5. Temperature monitoring
6. User authentication
7. LED control
8. Charger state monitoring
9. Energy measurements

The charge controller communicates the status messages of the charger hardware to the communication controller.
Find the release notes for the latest version and all previous versions.
If you wish to update the charge controller physically, Please see the Firmware Update Instruction
Note:
Feel free to contact us at in.support@brightblu.com for any queries or support requirement.

## Single Phase

## Current Production release: 4.0.1


# Firmware Version: 4.0.1

Release Date: 08/04/2025

Release Notes:
- Changed overcurrent value to 32A
- Added bootloader trigger on pin 24
- Added USBDFU functionality
- Enhanced Energy Meter Features
  * Added ability to read any register via serial monitor
  * Added ability to modify meter configuration via serial
  * Added support for changing serial 1 baud rate
- Added CP PWM reset feature in RTU state
  * Resets communication every 1 minute (3 attempts)
  * Can be enabled/disabled via serial monitor

# Firmware Version: 3.9.4

Release Date: 14/01/2025

Release Notes:
- Changed energy meter baud rate from 9.6k to 19.2k

# Firmware Version: 3.9.3

Release Date: 18/09/2024

Release Notes:
- Added reset control for SIM module

# Firmware Version: 3.9.2

Release Date: 07/06/2024

Release Notes:
- Reverted control pilot analog voltage range to previous values

# Firmware Version: 3.9.1

Release Date: 06/06/2024

Release Notes:
- Fixed float to string conversion for negative values
- Modified control pilot range for cap C27 expansion
- Added CBINIT message to communication controller
- Enhanced Error Handling
  * Added mask for diode error
  * Updated FSM to transition through Finishing state when moving from Diode/Vent error to Suspended EV

# Firmware Version: 3.8.4

Release Date: 19/04/2024

Release Notes:
- Fixed energy meter register reading
- Added ability for CMS to access any energy meter register

# Firmware Version: 3.8.3

Release Date: 12/03/2024

Release Notes:
- Added frequency parameter measurement and error with Mask
- Increased setup delay for voltage protection relay bootup
- Enhanced FSM Behavior
  * Modified config state to allow direct error transitions
  * Updated duty cycle values for control pilot PWM
  * Changed error to unavailable state transition to go through configuring
- Added global version string constant

# Firmware Version: 3.8.2

Release Date: 11/12/2023

Release Notes:
- Added power failure error for capacitor power backup chargers
- Added ability to modify control pilot PWM duty cycle directly from CMS

# Firmware Version: 3.8.1

Release Date: 17/05/2023

Release Notes:
- Added support for Emergency Button interface with NO contact
- Changed energy readings to be cumulative

# Firmware Version: 3.8

Release Date: 11/04/2023

Release Notes:
- Added masks for Leakage sensor and VPR

# Firmware Version: 3.7

Release Date: 16/02/2023

Release Notes:
- Fixed bug with 7-byte and 4-byte RFID tags

# Firmware Version: 3.6

Release Date: 24/01/2023

Release Notes:
- Added color codes for ESP and WiFi connection issues

# Firmware Version: 3.3.2

Release Date: 14/12/2022

Release Notes:
- Fixed duplicate error message in input check function

# Firmware Version: 3.2.1

Release Date: 10/05/2022

Release Notes:
- Added debug checks for energy and power measurement

# Firmware Version: 3.2

Release Date: 09/03/2022

Release Notes:
- Updated RFID read function to support both 4-byte and 7-byte cards

# Firmware Version: 3.1.2

Release Date: 27/02/2022

Release Notes:
- Updated DPM profile functionality

# Firmware Version: 3.1

Release Date: 15/02/2022

Release Notes:
- Added new DPM profile function

# Firmware Version: 3.0

Release Date: 05/01/2022

Release Notes:
- Updated firmware for new PCB board (C1-JOLT-V2.1)
  * Changed serial port configuration
  * Updated LED UI for config and preparing states
  * Modified temperature sensor behavior
- Added masks for system monitoring
  * Temperature monitoring
  * Ground fault detection
  * -12V supply fault detection

## Three Phase

## Current Production release: 4.0.1

# Firmware Version: 4.0.1
Release Date: 11/04/2025
Release Notes:
- Changed overcurrent value to 32A
- Added bootloader trigger on pin 24
- Added USBDFU functionality
- Added CP PWM reset feature in RTU state
  * Resets communication every 1 minute (3 attempts)
  * Feature can be enabled/disabled via serial monitor

# Firmware Version: 3.7.2
Release Date: 12/03/2025
Release Notes:
- Fixed baud rate auto update bug (9.6k to 19.2k)
- Enhanced serial energy meter configuration:
  * Added ability to set register address and data via serial
  * Added ability to set Serial 1 baud rate via serial

# Firmware Version: 3.7.1
Release Date: 20/02/2025
Release Notes:
- Fixed float to string conversion for negative values
- Added CBINIT message to communication controller
- Enhanced error handling:
  * Updated FSM for diode and vent errors
  * Added mask for diode error
- Added energy meter features:
  * Added ability to read any register via serial monitor
  * Added ability to change baud rate via serial

# Firmware Version: 3.7.0
Release Date: 13/01/2025
Release Notes:
- Changed energy meter communication baud rate from 9.6k to 19.2k

# Firmware Version: 3.6.3
Release Date: 13/05/2024
Release Notes:
- Added version number check through serial monitor

# Firmware Version: 3.6.2
Release Date: 22/04/2024
Release Notes:
- Fixed energy meter register reading
- Added ability for CMS to access any energy meter register
- Added frequency parameter measurement and error mask

# Firmware Version: 3.6.1
Release Date: 18/04/2024
Release Notes:
- Increased setup delay for voltage protection relay bootup
- Updated control pilot PWM duty cycle values
- Updated FSM state transitions (error to unavailable now goes through configuring)
- Added version string storage

# Firmware Version: 3.6
Release Date: 15/01/2024
Release Notes:
- Enhanced FSM with error state priority
- Added power failure error detection for chargers with capacitor power backup

# Firmware Version: 3.5
Release Date: 04/07/2023
Release Notes:
- Fixed duplicate error messages in input check function
- Added safety features:
  * Added masks for VPR and leakage sensor
  * Added support for Emergency Button interface with NO contact
- Changed energy readings to be cumulative

# Firmware Version: 3.4
Release Date: 01/03/2023
Release Notes:
- Fixed bug with 7-byte and 4-byte RFID tags

# Firmware Version: 3.3.1
Release Date: 06/02/2023
Release Notes:
- Updated energy meter configuration (MSB and LSB bytes interchange)

# Firmware Version: 3.3
Release Date: 26/12/2022
Release Notes:
- Added WiFi error codes to LED UI

# Firmware Version: 3.1
Release Date: 09/03/2022
Release Notes:
- Updated RFID read function for 4-byte and 7-byte card operation

# Firmware Version: 3.0
Release Date: 18/01/2022
Release Notes:
- Updated firmware for new PCB board (C1-JOLT-V2.1):
  * Changed serial port configuration
  * Updated LED UI for config and preparing states
  * Modified temperature sensor behavior
- Added system monitoring:
  * Temperature monitoring
  * Ground fault detection
  * -12V supply fault detection
