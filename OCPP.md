---
title: OCPP
layout: home
nav_order: 5
---
# OCPP 1.6J Integration Guide

## Overview
This document provides integration specifications for the BrightBlu Charging Communication Controller. Our implementation follows the OCPP 1.6J protocol with specific enhancements and behaviors detailed below.

## Transaction Flow Architecture

Our controller implements a state machine for transactions with the following key states:

1. **Available**: Ready to accept a new transaction
2. **Preparing**: Authorization in progress
3. **Charging**: Active charging session
4. **Suspended EV**: Vehicle has paused charging
5. **Finishing**: Transaction ending sequence
6. **Reserved**: Connector is reserved for a specific user
7. **DiodeError**: Vehicle has detected water/contaminents in the connector. Will not charge
8. **VentError**: Vehicle has detected Ventillation issues with its cooling system and will need to cool down before charging
9. **Faulted**: Faults detected by the charger or vehicle. Detailed list provided below

### Authorization Flow

The authorization sequence follows specific pathways based on configuration parameters:

```
┌─────────────────┐    ┌───────────────────┐    ┌───────────────────┐
│ RFID Presented  │───►│ LocalPreAuthorize │───►│ Local DB Check    │
└─────────────────┘    └───────────────────┘    └─────────┬─────────┘
                                                           │
                                                           ▼
┌────────────────────┐    ┌───────────────┐    ┌───────────────────┐
│ Remote Authorization◄───┤ Not Found     │◄───┤ RFID Found?      │
└──────────┬─────────┘    └───────────────┘    └───────────────────┘
           │                                            │
           ▼                                            ▼
┌─────────────────────┐                       ┌──────────────────┐
│ Central System Auth  │                      │ Begin Transaction │
└──────────┬──────────┘                       └──────────────────┘
           │
           ▼
┌─────────────────────┐
│ Transaction Decision │
└─────────────────────┘
```

## Parameter Interactions & Dependencies

### Authorization Parameter Relationships

The following parameters work together to control authorization behavior:

| Primary Parameter | Related Parameters | Interaction Behavior |
|-------------------|-------------------|----------------------|
| LocalPreAuthorize | AuthorizationCacheEnabled | When LocalPreAuthorize=true and AuthorizationCacheEnabled=true, the system checks the local cache before making a server request |
| LocalAuthorizeOffline | AllowOfflineTxForUnknownId | When offline, LocalAuthorizeOffline controls whether local authorization is attempted. If true but RFID is unknown, AllowOfflineTxForUnknownId determines if charging proceeds |
| AuthorizeRemoteTxRequests | - | Controls whether RemoteStartTransaction commands require separate authorization via Authorize request |

**Example**: If server connectivity is lost during charging (connectionServer=false):
- If LocalAuthorizeOffline=true: New RFID requests will be validated against local whitelist
- If AllowOfflineTxForUnknownId=true: Unknown RFIDs will be accepted
- If both are false: No new charging sessions will be authorized during offline periods

### Transaction Control Parameters

These parameters determine behavior during active charging sessions:

| Parameter | Related Parameters | Effect |
|-----------|-------------------|--------|
| StopTransactionOnEVSideDisconnect | UnlockConnectorOnEVSideDisconnect | When vehicle disconnects while StopTransactionOnEVSideDisconnect=true, transaction ends and connector unlocks if UnlockConnectorOnEVSideDisconnect=true |
| StopTransactionOnInvalidId | - | When a different RFID is presented during charging, transaction ends if this is true |
| suspendedEVTimeout | - | Maximum time (seconds) to wait in "SuspendedEV" state before ending transaction |

**Implementation Detail**: Our controller sends StatusNotification with status="SuspendedEV" when charging pauses, then monitors for timeout specified in suspendedEVTimeout. Once exceeded, a StopTransaction with reason="EVDisconnected" is automatically triggered.

### Meter Value Configuration

The meter value parameters form a complex interaction that controls data sampling and reporting:

| Parameter | Related Parameters | Effect |
|-----------|-------------------|--------|
| MeterValueSampleInterval | MeterValuesSampledData | Controls how frequently (seconds) the meter values in MeterValuesSampledData are sampled and sent |


**Implementation Note**: Our system attempts to optimize network traffic by:
1. Not sending unchanged meter values when variations are below thresholds
2. Bundling multiple measurements when possible
3. Prioritizing critical measurements (Energy.Active.Import.Register) during network constraints


## Phase Configuration & Power Management

The "Phase" parameter is critical for charger operation:

* **Single.Phase**: Operates on L1-N, limits to 7kW
* **Three.Phase**: Operates on L1-L2-L3-N, supports up to 22kW

The system automatically applies appropriate limits to DPM (Dynamic Power Management) based on phase configuration.

## Meter Value Measurement Specifics

Our implementation supports these specific measurements:

| Measurement | Units | Description |
|-------------|-------|-------------|
| Energy.Active.Import.Register | Wh | Cumulative energy consumed (required in all transaction messages) |
| Voltage | V | RMS voltage per phase |
| Current.Import | A | Current being drawn per phase |
| Power.Active.Import | W | Active power being drawn |
| Temperature | C | Internal temperature of charging unit |
| Frequency | Hz | AC frequency |
| Power.Factor | - | Power factor ratio (0.00-1.00) |
| Current.Offered | A | Maximum current available from EVSE |

**Implementation Detail**: All the data is directly retireved from the Energy Meter. No calculations/edits are done to these values.

## Reservation Implementation

Our reservation system has specific behavior:

1. Reservations timeout after the expiry time in ReserveNow
2. Only the specified idTag can initiate a transaction during reservation
3. Presenting a different RFID during reservation period results in FAUTH1 signal and rejection

## Error Code Details

When sending StatusNotification, our controller uses these specific error codes:

| Error Code | Description | System Response |
|------------|-------------|----------------|
| ConnectorLockFailure | Unable to lock/unlock connector | Retry 3 times, then report failure |
| EVCommunicationError | Cannot establish/maintain EV communication | Wait 30s, attempt reset |
| GroundFailure | Ground fault detected | Immediate shutdown, requires manual reset |
| HighTemperature | System temperature exceeds safe threshold | Reduces max current, may shutdown |
| PowerMeterFailure | Unable to read energy meter | Falls back to calculated energy values |
| PowerSwitchFailure | Cannot control power contactor | Immediate shutdown, reports fatal error |
| ReaderFailure | RFID reader malfunction | System remains operational but requires service |
| ResetFailure | Failed to reset system | Attempts alternative reset method |
| WeakSignal | Cellular/WiFi signal below threshold | Only sent in Available State and is NOT a FAULTED state. Attempts connectivity recovery measures.|
| UnderVoltage | BRIGHTBLU Chargers support an input supply value of +/- 20% of 230V |
| OverVoltage | BRIGHTBLU Chargers support an input supply value of +/- 20% of 230V |
| OverCurrentFailure | Charger has detected that the current drawn is greater than max allowed (32A) |
| HighTemperature | Charger Temperature sensor detects an internal temperature greater than 80°C and has shut down to prevent further damage. |
| GroundFailure | Neutral - Earth Voltage has exceeded permissible values (Maximum allowed 8V) |
| DiodeError | Diode Failure detected at Vehicle end |
| VentError | Ventillation Error Failure detected at Vehicle end |
| OtherError: | Includes the following sub-errors (vendorErrorCode): |
| &nbsp;&nbsp;•EmergencyButton | Emergency Button is pressed |
| &nbsp;&nbsp;•InputFrequencyError | Frequency of Input Supply is not between 50/60 Hz |
| &nbsp;&nbsp;•EarthLeakageError | A current leakage of either 30mA AC or 6mA DC has been detected |
| &nbsp;&nbsp;•PowerFailure | Loss of input supply power(Will only work with BRIGHTBLU POWER BACKUP systems) |
| &nbsp;&nbsp;•ModBusComsFailure | Loss of communication with Energy Meter |
| &nbsp;&nbsp;•VPRError | Input Supply error (Phase Reversal or Asymetrical input supply)(Mostly with 3 Phase) |
| &nbsp;&nbsp;•SDCardFailure | Internal SD Card error(Logging and OTA updates disabled but charger will function normally otherwise) |

## Supported Configuration Parameters

Below is a comprehensive list of all configuration parameters supported by our implementation:

| Parameter | Default | Description |
|-----------|---------|-------------|
| AllowOfflineTxForUnknownId | false | Allow transactions for unknown idTags when offline |
| AuthorizationCacheEnabled | true | Enable authorization cache |
| AuthorizeRemoteTxRequests | false | Require authorization for remote start requests |
| MaxCurrentLimit(A) | 32 | Maximum current limit (will not exceed) |
| ClockAlignedDataInterval | 0 | Interval (sec) for clock-aligned data |
| ConnectionTimeOut | 60 | Timeout (sec) for connection attempts |
| ConnectorPhaseRotation | "NotApplicable" | Phase rotation for the connector |
| ConnectorPhaseRotationMaxLength | 25 | Max length of phase rotation value |
| DefaultIdTag | "" | Default IdTag for free mode |
| FreeMode | false | Allow charging without authorization |
| GetConfigurationMaxKeys | 50 | Max config keys to return |
| HeartbeatInterval | 300 | Interval (sec) between heartbeats |
| LocalAuthListEnabled | true | Enable local authorization list |
| LocalAuthListMaxLength | 1000 | Max size of local auth list |
| LocalAuthorizeOffline | true | Enable local auth while offline |
| LocalPreAuthorize | false | Check auth locally before central system |
| MaxEnergyOnInvalidId | 0 | Max energy (Wh) after invalid IdTag |
| MeterValuesAlignedData | Multiple* | Aligned meter values to collect |
| MeterValuesAlignedDataMaxLength | 500 | Max length of aligned data |
| MeterValueSampleInterval | 60 | Interval (sec) between meter samples |
| MeterValuesSampledData | Multiple** | Values to sample (cannot be edited) |
| MeterValuesSampledDataMaxLength | 500 | Max length of sampled data |
| NumberOfConnectors | 1 | Number of connectors in charge point |
| OcppChargerId | DEVICE_ID | Charge point identifier |
| OcppServerAddress | "" | OCPP server URL |
| OnPowerLossRestart | false | Restart transaction after power loss |
| Phase | "Single.Phase" | Phase configuration |
| ResetRetries | 1 | Number of reset attempts |
| SendLocalListMaxLength | 30 | Max size for SendLocalList |
| StopTransactionOnEVSideDisconnect | true | Stop transaction on EV disconnect |
| StopTransactionOnInvalidId | true | Stop when invalid IdTag presented |
| StopTxnAlignedData | "Energy.Active.Import.Register" | Aligned data in StopTransaction |
| StopTxnAlignedDataMaxLength | 500 | Max length of StopTxn aligned data |
| StopTxnSampledData | "Energy.Active.Import.Register" | Sampled data in StopTransaction |
| StopTxnSampledDataMaxLength | 500 | Max length of StopTxn sampled data |
| SupportedFeatureProfiles | Multiple*** | Supported OCPP features |
| SupportedFeatureProfilesMaxLength | 15 | Max length of feature profiles |
| suspendedEVTimeout | 900 | Max time (sec) in SuspendedEV state |
| TransactionMessageAttempts | 3 | Number of transaction msg attempts |
| TransactionMessageRetryInterval | 30 | Retry interval (sec) between attempts |
| UnlockConnectorOnEVSideDisconnect | true | Unlock on EV disconnect |
| WiFiConnect | false | disable network switching |
| WiFiPass | "N/A" | Fallback WiFi password |
| WiFiSsid | "N/A" | Fallback WiFi SSID |

* MeterValuesAlignedData default for Business: "Energy.Active.Import.Register,Voltage,Current.Import,Power.Active.Import,Energy.Reactive.Import.Register,Temperature,Power.Reactive.Import,Frequency,Power.Factor,Current.Offered,Power.Offered"

* MeterValuesAlignedData default for Home Plus: "Energy.Active.Import.Register,Voltage,Current.Import,Power.Active.Import,Temperature,Current.Offered,Power.Offered"

* SupportedFeatureProfiles default: "Core,FirmwareManagement,LocalAuthListManagement,Reservation,RemoteTrigger"

* **Network Failover System**: The WiFiConnect, WiFiPass, and WiFiSsid parameters work together to provide network redundancy:
  * When WiFiConnect = true: Network failover is enabled
  * When WiFiConnect = false: The device uses only its primary connection method (default)
  * How it works: The device will first try to connect using its primary connection method (Cellular/LAN/WiFi). If that connection fails or becomes unstable, it will automatically switch to the configured WiFi network (using WiFiSsid/WiFiPass) as a backup. The device will continue to monitor both connections and use whichever is more stable.

## Charger Configuration

To set up your charger, please download the BRIGHTBLU Install Partner application:

- [Play Store](https://play.google.com/store/apps/details?id=com.brightblu.joltCommission&hl=en)
- [App Store](https://apps.apple.com/us/app/jolt-install-partner/id6553999518)

Authentication requires a one-time password (OTP) provided by BRIGHTBLU Support. After successful login, you can connect to your BRIGHTBLU JOLT Charger.


### Important Configuration Notes

1. **Device Identification**
   - The Charger ID displayed in the BLE application is fixed and cannot be changed
   - The OCPP Device ID setting affects only OCPP server communications

2. **Server URL Format**
   - Use the following format: `ws://"host":"port"/"path"` or `wss://"host":"port"/"path"`
   - Port specification is mandatory (even for default ports 80/443)
   - Do not include trailing slashes (/) or the charger ID in the URL
   - The device automatically appends the charger ID to complete the connection URL

3. **Energy Metering**
   - JOLT BUSINESS: Stores cumulative energy values between sessions
   - HOME PLUS: Resets energy counter at the start of each session (meterStart = 0)

4. **Network**
   - BRIGHTBLU JOLT HOME PLUS only supports WiFi/ BLE/ SIM
   - BRIGHTBLU JOLT BUSINESS supports WiFi/BLE/SIM/LAN
   - BRIGHTBLU JOLT always uses WiFi. The SIM Module on the JOLT acts as a hotspot for the controller to connect to. If you do not wish to connect it to SIM, you can always configure the charger to access other WiFi Connections and also configure fallback WiFi connections.




## Contact Information

For technical support or further information, please contact:
- in.support@brightblu.com
