---
title: LED Status
layout: default
nav_order: 2
parent: ChargeBox Controller
grand_parent: Jolt Business
---

JOLT Business

LED Indicators:

This page provides all the LED indications in BRIGHTBLU JOLT Business chargers and the probable reasoning and solution to the same.

In case of any issues please feel free to contact us at in.support@brightblu.com for any queries or support requirement.

<!-- | Led Color | Reason |
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
| &nbsp;&nbsp;•SDCardFailure | Internal SD Card error(Logging and OTA updates disabled but charger will function normally otherwise) | -->

<!--
<table>
  <thead>
    <tr>
      <th>Led Color</th>
      <th>Reason</th>
    </tr>
  </thead>
  <tbody>
    <tr style="color: Green;">
      <td style="text-shadow: 1px 1px 1px black;">- - -</td>
      <td>If the LED indication is GREEN and Stable, the charger is in Available state</td>
    </tr>
        <tr  >
      <td style="text-shadow: 1px 1px 1px black;color: green;" class="blinking">- - -</td>
      <td >The Charger detects a vehicle has been connected. Its in Preparing State but not authorized to dispense power</td>
    </tr>
    <tr style="background-color: green; ">
      <td style="text-shadow: 1px 1px 1px black;color: cyan;">- - -</td>
      <td >The Charger has been authorized to initiate a charge session, but waiting for the plug to be connected</td>
    </tr>
    <tr style="background-color: blue;">
      <td style="text-shadow: 1px 1px 1px black; color: Yellow;">- - -</td>
      <td >Charger has detected that the current drawn is greater than max allowed (32A)</td>
    </tr>
    <tr style="background-color: yellow; ">
      <td style="text-shadow: 1px 1px 1px black;color: Navy;">- - -</td>
      <td >Charger Temperature sensor detects an internal temperature greater than 80°C and has shut down to prevent further damage.</td>
    </tr>
    <tr style="background-color: orange; color: Red;">
      <td style="text-shadow: 1px 1px 1px black;">- - -</td>
      <td style="text-shadow: 1px 1px 1px black;">Check the number of Blinks to Identify the error</td>
    </tr>
    <tr style="background-color: purple; color: red;">
      <td style="text-shadow: 1px 1px 0 black;">&nbsp;&nbsp;2</td>
      <td style="text-shadow: 1px 1px 0 black;">Emergency Button is pressed</td>
    </tr>
        <tr style="background-color: orange; color: Purple;">
      <td style="text-shadow: 1px 1px 0 black;">- - -</td>
      <td style="text-shadow: 1px 1px 0 black;">Check the number of Blinks to Identify the error</td>
    </tr>
    <tr style="background-color: purple; color: red;">
      <td style="text-shadow: 1px 1px 0 black;">&nbsp;&nbsp;2</td>
      <td style="text-shadow: 1px 1px 0 black;">Emergency Button is pressed</td>
    </tr>
  </tbody>
</table>

<style>
  .blinking {
    animation: blinker 2s linear infinite;
  }

  @keyframes blinker {
    50% { opacity: 0; }
  }
</style> -->
<!--
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LED Status Table</title>
    <style>
        table {
            border-collapse: collapse;
            width: 100%;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        .led {
            width: 30px;
            height: 15px;
            border-radius: 5px;
            display: inline-block;
            margin-right: 10px;
        }
        .blinking {
            animation: blinker 2s ease-in-out infinite;
        }
        .blink-2 {
            animation: blinker-2 15s infinite;
        }
        .blink-3 {
            animation: blinker-3 15s ease-in-out infinite;
        }
        .blink-4 {
            animation: blinker-4 15s ease-in-out infinite;
        }
        .blink-5 {
            animation: blinker-5 15s ease-in-out infinite;
        }
        @keyframes blinker {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }
        @keyframes blinker-2 {
            100% { opacity: 1; }
            0 { opacity: 0.3; }
        }
        @keyframes blinker-3 {
            0%, 9%, 11%, 19%, 21%, 29%, 31%, 100% { opacity: 1; }
            10%, 20%, 30% { opacity: 0.3; }
        }
        @keyframes blinker-4 {
            0%, 7%, 9%, 15%, 17%, 23%, 25%, 31%, 33%, 100% { opacity: 1; }
            8%, 16%, 24%, 32% { opacity: 0.3; }
        }
        @keyframes blinker-5 {
            0%, 6%, 8%, 13%, 15%, 20%, 22%, 27%, 29%, 34%, 36%, 100% { opacity: 1; }
            7%, 14%, 21%, 28%, 35% { opacity: 0.3; }
        }
    </style>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>Led Color</th>
                <th>Reason</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><div class="led" style="background-color: green;"></div></td>
                <td>Charger is in Available state</td>
            </tr>
            <tr>
                <td><div class="led blinking" style="background-color: green;"></div></td>
                <td>Charger detects a vehicle has been connected. Its in Preparing State but not authorized to dispense power</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: cyan;"></div></td>
                <td>Charger has been authorized to initiate a charge session, but waiting for the plug to be connected</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: yellow;"></div></td>
                <td>Charger has detected that the current drawn is greater than max allowed (32A)</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: navy;"></div></td>
                <td>Charger is in Charging state and dispensing power to the vehicle</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: red;"></div></td>
                <td>Check the number of Blinks to Identify the error</td>
            </tr>
            <tr>
                <td><div class="led blink-2" style="background-color: red;"></div></td>
                <td>Emergency Button is pressed</td>
            </tr>
            <tr>
                <td><div class="led blink-3" style="background-color: red;"></div></td>
                <td>Red Error Code 3</td>
            </tr>
            <tr>
                <td><div class="led blink-4" style="background-color: red;"></div></td>
                <td>Red Error Code 4</td>
            </tr>
            <tr>
                <td><div class="led blink-5" style="background-color: red;"></div></td>
                <td>Red Error Code 5</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: purple;"></div></td>
                <td>Check the number of Blinks to Identify the error</td>
            </tr>
            <tr>
                <td><div class="led blink-2" style="background-color: purple;"></div></td>
                <td>Purple Error Code 2</td>
            </tr>
            <tr>
                <td><div class="led blink-3" style="background-color: purple;"></div></td>
                <td>Purple Error Code 3</td>
            </tr>
            <tr>
                <td><div class="led blink-4" style="background-color: purple;"></div></td>
                <td>Purple Error Code 4</td>
            </tr>
            <tr>
                <td><div class="led blink-5" style="background-color: purple;"></div></td>
                <td>Purple Error Code 5</td>
            </tr>
        </tbody>
    </table>
</body>
</html> -->


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LED Status Table</title>
    <style>
        table {
            border-collapse: collapse;
            width: 100%;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        .led {
            width: 30px;
            height: 15px;
            border-radius: 5px;
            display: inline-block;
            margin-right: 10px;
            opacity: 1;
            transition: opacity 0.1s;
        }
        /* Blinking animations for Red and Purple LEDs on a 15s cycle */
        .blink-2 {
            animation: blinkAnimation2 10s infinite;
        }
        @keyframes blinkAnimation2 {
            0%, 100% { opacity: 1; }
            10%, 20%{ opacity: 0; }
            12%, 22%, 32% { opacity: 1; }
        }
        .blink-3 {
            animation: blinkAnimation3 10s infinite;
        }
        @keyframes blinkAnimation3 {
            0%, 100% { opacity: 1; }
            10%, 20%, 30% { opacity: 0; }
            12%, 22%, 32% { opacity: 1; }
        }
        .blink-4 {
            animation: blinkAnimation4 10s infinite;
        }
        @keyframes blinkAnimation4 {
            0%, 100% { opacity: 1; }
            10%, 20%, 30%, 40% { opacity: 0; }
            12%, 22%, 32%, 42% { opacity: 1; }
        }
        .blink-4purple {
            animation: blinkAnimation4purple 8s infinite;
        }
        @keyframes blinkAnimation4purple {
            0%, 100% { opacity: 1; }
            10%, 20%, 30%, 40% { opacity: 0; }
            12%, 22%, 32%, 42% { opacity: 1; }
        }
        .blink-5 {
            animation: blinkAnimation5 10s infinite;
        }
        @keyframes blinkAnimation5 {
            0%, 100% { opacity: 1; }
            10%, 20%, 30%, 40%, 50% { opacity: 0; }
            12%, 22%, 32%, 42%, 52% { opacity: 1; }
        }
        .blink-6 {
            animation: blinkAnimation6 10s infinite;
        }
        @keyframes blinkAnimation6 {
            0%, 100% { opacity: 1; }
            10%, 20%, 30%, 40%, 50%, 60% { opacity: 0; }
            12%, 22%, 32%, 42%, 52%, 62% { opacity: 1; }
        }
        .blink-7 {
            animation: blinkAnimation7 10s infinite;
        }
        @keyframes blinkAnimation7 {
            0%, 100% { opacity: 1; }
            10%, 20%, 30%, 40%, 50%, 60%,70% { opacity: 0; }
            12%, 22%, 32%, 42%, 52%, 62%,72% { opacity: 1; }
        }
        .blink-8 {
            animation: blinkAnimation8 10s infinite;
        }
        @keyframes blinkAnimation8 {
            0%, 100% { opacity: 1; }
            10%, 20%, 30%, 40%, 50%, 60%,70%,80% { opacity: 0; }
            12%, 22%, 32%, 42%, 52%, 62%,72%,82% { opacity: 1; }
        }
        /* Green LED is always visible */
        .green-blink {
            animation: greenBlink 2.5s ease-in-out infinite;
        }
        @keyframes greenBlink {
            25%, 100% { opacity: 1; }
            50% { opacity: 0.1; }
        }
        .purple-blink {
            animation: purpleBlink 1s ease-in-out infinite;
        }
        @keyframes purpleBlink {
            25%, 100% { opacity: 1; }
            50% { opacity: 0.1; }
        }
    </style>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>Led Color</th>
                <th>Reason</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><div class="led" style="background-color: green;"></div></td>
                <td>Charger is in Available state</td>
            </tr>
            <tr>
                <td><div class="led green-blink" style="background-color: green;"></div></td>
                <td>Charger detects a vehicle has been connected. Its in Preparing State but not authorized to dispense power</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: cyan;"></div></td>
                <td>Charger has been authorized to initiate a charge session, but waiting for the plug to be connected</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: yellow;"></div></td>
                <td>Charger has detected that the current drawn is greater than max allowed (32A)</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: navy;"></div></td>
                <td>Charger is in Charging state and dispensing power to the vehicle</td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: red;"></div></td>
                <td>Observe the blinks and match it with the error list below. The blink pattern repeats every 15s</td>
            </tr>
            <tr>
                <td><div class="led green-blink" style="background-color: red;"></div></td>
                <td>  Reason: <b>Charger is in Configuring state. Check Communication controller if this error persists for more than 5min</b></td>
            </tr>
            <tr>
                <td><div class="led blink-2" style="background-color: red;"></div></td>
                <td>LED Blink: <b>2</b> Error Reason: <b>Ground Fault</b></td>
            </tr>
            <tr>
                <td><div class="led blink-3" style="background-color: red;"></div></td>
                <td>LED Blink: <b>3</b> Error Reason: <b>Emergency Button</b></td>
            </tr>
            <tr>
                <td><div class="led blink-4" style="background-color: red;"></div></td>
               <td>LED Blink: <b>4</b> Error Reason: <b>Earth Leakage Error</b></td>
            </tr>
            <tr>
                <td><div class="led blink-5" style="background-color: red;"></div></td>
                <td>LED Blink: <b>5</b> Error Reason: <b>Voltage Error (Over/Under Voltage)</b></td>
            </tr>
            <tr>
                <td><div class="led blink-6" style="background-color: red;"></div></td>
                <td>LED Blink: <b>6</b> Error Reason: <b>Temperature</b></td>
            </tr>
            <tr>
                <td><div class="led blink-7" style="background-color: red;"></div></td>
                <td>LED Blink: <b>7</b> Error Reason: <b>Over Current</b></td>
            </tr>
            <tr>
                <td><div class="led blink-8" style="background-color: red;"></div></td>
                <td>LED Blink: <b>8</b> Error Reason: <b>Frequency Error</b></td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: red;"></div></td>
                <td>LED Blink: <b>0</b> Error Reason: <b>Power Supply Error/Power Loss (BRIGHTBLU Battery Backup)</b></td>
            </tr>
            <tr>
                <td><div class="led" style="background-color: Fuchsia;"></div></td>
                <td>Observe the blinks and match it with the error list below</td>
            </tr>
            <tr>
                <td><div class="led purple-blink" style="background-color: Fuchsia;"></div></td>
                <td>Reason: <b>BLE Connection detected.</b>The Device is now in configuration mode</td>
            </tr>
            <tr>
                <td><div class="led blink-4purple" style="background-color: Fuchsia;"></div></td>
                <td>LED Blink: <b>4</b> Error Reason: <b>Disconnected From Server.Attempting to reconnect</b></td>
            </tr>
        </tbody>
    </table>
</body>
</html>
