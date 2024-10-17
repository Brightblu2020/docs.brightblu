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

## Current Production release: 3.9.3

# Firmware Version: 3.9.3
Release Date: 18/09/2024

Release Notes:
-            Added GPIO pin 28 for SIM module reset.

# Firmware Version: 3.9.2
Release Date: 07/06/2024

Release Notes:
-            Control pilot voltage range changed due to removal of C27 capacitor.

# Firmware Version: 3.9.1
Release Date: 06/06/2024

Release Notes:
-            Edit to float to string function as negative float values were not getting converted properly.
-            Edit to control pilot range.
-            Initialization message sent to communication controller (CBINIT)
-            Error mask enabled for diode error
-            Change made to FSM state. When charger moves from Diode or Vent error to Suspended EV, it should first go to Finishing state so the session can end.

## Three Phase

## Current Production release: 3.6.3
Release Date: 13/05/2024

# Firmware Version: 3.6.3
Release Date: 13/05/2024

Release Notes:
-            Addition of Version number string.

# Firmware Version: 3.6.2
Release Date: 22/04/2024

Release Notes:
-            Correction to the energy meter hex value conversion.
-            Ability for ESP to request energy meter register value added.
-            Frequency measurement and monitoring added.
-            Mask to enable and disable frequency error added.
