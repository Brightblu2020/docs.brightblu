---
title: Communication Controller
layout: default
nav_order: 1
parent: Jolt Business
grand_parent: Firmware
---

JOLT Business

Communication Controller:

The communication controller(CC) handles all the external requests to and from the device. It handles everything with regards to network , cloud and Application communication. The CC currently supports 3G/4G SIM Connectivity, LAN and WiFi. The CC also runs BRIGHTBLU OCPP 1.6J, handles all the communication with the Charge Controller. In order to configure the charger please use our installer application :

<b>JOLT INSTALL PARTNER</b>

<a href="https://play.google.com/store/apps/details?id=com.brightblu.joltCommission&hl=en">Play Store </a>
<br>
<a href="https://play.google.com/store/apps/details?id=com.brightblu.joltCommission&hl=en">App Store  </a>


Find the release notes for the latest version and all previous versions.

If you wish to update your charger physically, Please see the <b>Firmware Update Instruction</b>: <a href="FirmwareFlashCommunicationController.html"> Here </a>

Note:
* Only v4.0.26 and above support wss. If the device is below this said version, you are requested to update the CC to the latest version to access this support
* Only v3.0.021/B and above support BLE / Installer Application.


Feel free to contact us at in.support@brightblu.com for any queries or support.

## Current Production release: 4.0.037

# Firmware Version: 4.0.037

Release Notes:

- Added Ability to now do OTA if SdCardFaiure is detected by bypassing SD check.
- Fixed Long file names not working in internal memory and SD card for Logs.
- Improved the websocket thread efficiency.


# Firmware Version: 4.0.035

Release Notes:

- Fixed incorrect phase detection
- Changed how StartTransaction is initiated now. The command to initiate charging is now switched to RTU state instead of preparing.
- Updated certain internal libraries to the latest versions
- Updated register values for all measurands

# Firmware Version: 4.0.032

Release Notes:

- Fixed incorrect Energy Meter Register (only in 3 Phase systems).

# Firmware Version: 4.0.030

Release Notes:

- Added Ability to Switch between networks. Set the WiFi User and pass in Get Configuration and enable WiFiConnect to True. This will enable fallback connection incase the main internet is lost/disconnected. By default the first configured mode of connection is always preffered(In case of restart, it will not switch to fallback).
- Improved disconnection check and moved Websocket connection to a separate thread.
- Removed saving all meterValues when offline. Now only Start/Stop Transactions will be stored along with StatusNotifications to ensure optimal use of limited space.
- Changed StopTransaction Reason to Other when stopped due to faults (For available reasons itll show the correct value for eg: EmergencyStop , PowerLoss).
- Fixed OnPowerLossRestart ending a session in BRIGHTBLU POWER BACKUP enabled devices.





# Firmware Version: 4.0.026

Release Notes:

- Upgraded from v3.0 due to addition of wss support. If installing this version, it is preferred to do a physical flash instead of OTA to ensure the DB files do not get corrupt
- wss support enabled. please use the following url format while entering it via the JOLT INSTALLER APPLICATION
        <wss://hostname:PORT/>. Please Ensure PORT is mentioned. The device will fail to connect if the PORT is not mentioned
- Cleaned up DB size and reduced Buffer size to increase available RAM
- Added SIM reset option in Maintainance Page
- Logging on SD card fixed timestamp mixup (GMT +5:30 option removed due to location instability). Current logs will always be UTC
- Changed Websocket disconnection algorithm. Previously the controller forced a restart if network instability was observed. This sometimes caused a bootloop which required the charger to then be physically restarted. This was due to a memory leak which did not allow the soft restart to function correctly
- Added onPowerLossRestart OCPP configuration which allows the unit to restart a charge session in case a power loss occured during a charge session. Will reuse the same idTag and transactionID. By default this option is False.
- Changed StopTransactionReason from always defaulting to Deauthorized to the correct reason. Deauthorized will now only come when the Server invalidates a session.
- Made changes to SPIFFS Sector reading/Writing to ensure minimal wear and tear
- Added BLE Configuration to change Charger parameters such as GND MSK and TEMP MSK
- If the server URL is set to use WSS, the BLE will be disabled after 30 seconds upon successfully connecting with the CMS Server. To reconnect to the BLE, the device must be restarted and the BLE connection established before the system successfully connects to the CMS Server. The average time for the system to connect to the CMS Server is 60 seconds. However, there's an exception to this behavior: if an application connects to the BLE before the system establishes a connection with the CMS Server, the BLE remains connected and will continue to do so until the application disconnects from it. This is done to optimize for available RAM for wss connection requests.


# Firmware Version: 3.0.21/B - 3.0.025

Release Notes:

- Added BLE support for Jolt Installer Application
- Added LAN Support
- Upgraded to LittleFS from SPIFFS.Allows for higher onboard storage of OFFLINE messages (Current Capacity 350 messages)
- In order to optimize for space and efficiency,if the device goes OFFLINE, the MeterValueSampleInterval is shifted to 900s(This is reverted to original server values upon coming ONLINE).
- If the memory capacity exceeds 349 messages, the device is overwrite the oldest messages to store the latest. 350 messages should be good enough for 3 full charge sessions.
- Implemented FIFO queue when system is online to avoid wear and tear on the File System.
- **Implemented OTA update via BLE. This is for emergency only and not really suitable for mass upgrades and it is very slow and time consuming. Future updates will focus on bringing this time down to about ~ 2min from the current 25-30min
- Websocket Ping/Pong (pingInterval,pongTimeout,disconnectTimeoutCount) interval set to (10000, 3000, 10)
    * pingInterval – uint32_t how often ping will be sent
    * pongTimeout – uint32_t millis after which pong should timout if not received
    * disconnectTimeoutCount – uint8_t how many timeouts before disconnect
- Websocket Ping/Pong will be made configurable in the next iteration via GetConfiguration
- SD card detection and Failure update as StatusNotification with the ERROR Code "SDCardFailure". If this is detected, OTA update will be temporarily disabled. If subsequent physical restarts/ Hard Resets do not fix this issue, a physical inspection is necessary and a format of the card might be required.


    ** Alpha Stage. Will contain bugs which are being actively fixed.


Note: Ensure the correct firmware files are downloaded for your version of charger.
<b> Please proceed with Extreme Caution</b>.
If you are confused about your charger version, please contact BRIGHTBLU Support to guide you at in.support@brightblu.com.

## Download the latest firmware files:  <a href="assets/firmware/BBCCfirmwarefiles.zip" class="download-link" download> Here </a>
