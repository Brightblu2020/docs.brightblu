---
title: Error Codes OCPP
layout: default
nav_order: 2
parent: Communication Controller
grand_parent: Jolt Business
---

JOLT Business

Error Codes:

This page provides all the Error Codes present in BRIGHTBLU JOLT Business chargers and the probable reasoning and solution to the same.

In case of any issues please feel free to contact us at in.support@brightblu.com for any queries or support requirement.

ERROR CODE LIST:

| Error Code | Reason |
| :--- | :--- |
| UnderVoltage | BRIGHTBLU Chargers support an input supply value of +/- 20% of 230V |
| OverVoltage | BRIGHTBLU Chargers support an input supply value of +/- 20% of 230V |
| OverCurrentFailure | Charger has detected that the current drawn is greater than max allowed (32A) |
| HighTemperature | Charger Temperature sensor detects an internal temperature greater than 80°C and has shut down to prevent further damage. |
| GroundFailure | Neutral - Earth Voltage has exceeded permissible values (Maximum allowed 8V) |
| OtherError: | Includes the following sub-errors (vendorErrorCode): |
| &nbsp;&nbsp;•EmergencyButton | Emergency Button is pressed |
| &nbsp;&nbsp;•InputFrequencyError | Frequency of Input Supply is not between 50/60 Hz |
| &nbsp;&nbsp;•EarthLeakageError | A current leakage of either 30mA AC or 6mA DC has been detected |
| &nbsp;&nbsp;•PowerFailure | Loss of input supply power(Will only work with BRIGHTBLU POWER BACKUP systems) |
| &nbsp;&nbsp;•ModBusComsFailure | Loss of communication with Energy Meter |
| &nbsp;&nbsp;•VPRError | Input Supply error (Phase Reversal or Asymetrical input supply)(Mostly with 3 Phase) |
| &nbsp;&nbsp;•SDCardFailure | Internal SD Card error(Logging and OTA updates disabled but charger will function normally otherwise) |