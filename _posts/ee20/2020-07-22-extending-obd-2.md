---
layout:   page
title:    Extended OBD-II
category: ee20
tags:     cars subaru ee20
---

* TOC
{:toc}

## Introduction

Often called Extended OBD-II or Enhanced OBD-II, this newest diagnostic 
protocol has first been seen on Euro 5 diesel ECUs (MY2010+, SH7059 chip,
1.5 MiB ROM size). Several years later new petrol models (MY2014+ ?, 
SH72531 chip ?) require this exclusively (?). See page Boxer Diesel Models. 
As expected, Euro 6 diesel models (MY2015+) also use this protocol. On older 
diesels (Euro 4) and petrol models, both 1 MiB ROM, Extended OBD-II is
definitely not available – SSM2 only!
See also summary page Protocols.

Like standard OBD-II it works via ISO15765 transport protocol, same setup as
OBD-II and SSM2 via CAN. Apparently, other manufacturers use custom OBD-II 
modes, too. Generally, non-standard modes and their PIDs are manufacturer 
specific!

Mode 0x22 means (read) enhanced data and its Parameter Identification Number 
(PID) is made up of two bytes (uint16). Basic PIDs (high byte = `00`) match 
OBD-II standard PIDs e.g. `mode 0x22 PID 0x0005` yields same data as standard
OBD-II `mode 0x01 PID 0x05`.

As with SSM2 via CAN, Subaru Diesel Crew again was first, 2011-05-02, 
in publishing protocol details – enjoy!

### Software / Interface Hardware

Wikipedia info might help: On-board diagnostics

#### SAE J2534 capable

You can try the free tool described in J2534 device ISO15765 tutorial.

#### Torque (Pro) [Android]

    Homepage: http://torque-bhp.com/
    Wiki: http://torque-bhp.com/wiki/Main_Page

According to reports in forums, this Android app is working well and allows flexible configuration.

#### External links

    Subaru Fan Club (CZ) (seems they were first to use the protocol), 2012-09-04: http://subarufanclub.cz/forum/viewtopic.php?f=8&t=391&start=1815#p79506
    AUSubaru.com, 2014-02-15: http://www.ausubaru.com/forum/showthread.php?p=227342#post227342
    http://www.subaruforester.org/vbulletin/f160/pitrack_1-s-saga-dpf-regens-vs-performance-economy-loss-278465/index4.html#post3529673Torque Pro Test PID DPF_regen_256_zps703fa0a9 (subaruforester.org)
    Anyone tried these bluetooth interfaces e.g. WBH BT5
    https://www.blafusel.de/obd/wbh_bt5.html and software tools like mentioned CAN sniffer CANaBIß ?

Engine Link [iPad, iPhone, iPod]

    Homepage: http://www.outdoor-apps.com/enginelink.html
    Wiki: http://www.ksolution.org/outdoor//help.html

Seems to support custom PIDs, display as ASCII etc.
Authentication

Some PIDs might require seed-key login (algorithm needed, we do not publish crypto). Do these yield negative response message at least or no response at all?

However, generic logging applications usually do not support authentication anyway as it is manufacturer and model specific.
Definition Downloads

As always, do not hesitate to report errors, suggestions etc.
OpenDocument Format Spreadsheet

Format: (LibreOffice) OpenDocument Format Spreadsheet .ods:

Download: Subaru_mode22_def.ods

Rename to .ods after downloading. Use your favorite spreadsheet application in order to export as CSV etc. if needed.

Subaru_mode22_def
CSV

Format: CSV (field delimiter: tab), from project ParsePID (project page – github.com)

View and download (click button “Raw”): https://github.com/SubaruDieselCrew/ParsePID/blob/master/data/Subaru_mode22_def.csv
Overview (Listing)

The focus here is on diesel specific items, we will also add more petrol PIDs over time.
Listing is incomplete, though, many useful items (i.e. DPF related) are known and tested by now:

<table>
  <thead>
    <tr>
      <td>PID</td><td>Name</td><td>[D]iesel, [P]etrol</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th colspan="3">Should be same as OBD-II mode 1</th>
    </tr>
    <tr>
      <td>0005</td><td>Coolant Temperature</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>0023</td><td>Fuel Rail Pressure (diesel, or gasoline direct inject)</td>
    </tr>
    <tr>
      <td>003C</td><td>Exhaust Gas Temperature (EGT) at Catalyst Inlet</td>
    </tr>
    <tr>
      <td>003E</td><td>Exhaust Gas Temperature (EGT) at DPF Inlet</td>
    </tr>
    <tr>
      <th colspan="3">Identification</th>
    </tr>
    <tr>
      <td>F100</td><td>SSMID</td><td></td>
    </tr>
    <tr>
      <td>F182</td><td>ROMID</td><td></td>
    </tr>
    <tr>
      <td>F190</td><td>Vehicle Identification Number (VIN)</td><td></td>
    </tr>
    <tr>
      <td>F197</td><td>System String</td><td></td>
    </tr>
    <tr>
      <th colspan="3">Misc</th>
    </tr>
    <tr>
      <td>10AC</td><td>Primary Boost Control</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>10B2</td><td>Alternator Duty</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>10B4</td><td>Intake VVT Advance Angle Right</td><td>[P]</td>
    </tr>
    <tr>
      <td>10B5</td><td>Intake VVT Advance Angle Left</td><td>[P]</td>
    </tr>
    <tr>
      <td>10E3</td><td>Memorised Cruise Speed</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1116</td><td>Final Injection Amount</td><td>[D]</td>
    </tr>
    <tr>
      <td>111B</td>
      <td>Exhaust Gas Recirculation (EGR) Target Valve Opening Angle</td>
      <td>[D]</td>
    </tr>
    <tr>
      <td>111C</td>
      <td>Exhaust Gas Recirculation (EGR) Valve Opening Angle</td>
      <td>[D]</td>
    </tr>
    <tr>
      <td>111F</td><td>Inlet Air Temperature (after air filter)</td><td>[D]</td>
    </tr>
    <tr>
      <td>1121</td><td>Target Engine Speed</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>112A</td><td>Mileage after Injector Learning</td><td>[D]</td>
    </tr>
    <tr>
      <td>112B</td><td>Mileage after Injector Replacement</td><td>[D]</td>
    </tr>
    <tr>
      <td>112C</td><td>Interior Heater</td><td>[D]</td>
    </tr>
    <tr>
      <td>112D, 112E, 112F, 1130</td>
      <td>Quantity Correction Cylinder #1 .. 4</td>
      <td>[D]</td>
    </tr>
    <tr>
      <td>1135</td><td>Battery Current</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1136</td><td>Battery Temperature</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>Diesel Particulate Filter (DPF) specific</td>
    </tr>
    <tr>
      <td>1149</td><td>Cumulative Ash Ratio</td><td>[D]</td>
    </tr>
    <tr>
      <td>114A</td><td>Pressure Difference between DPF Inlet and Outlet</td><td>[D]</td>
    </tr>
    <tr>
      <td>114B</td><td>Estimated Catalyst Temperature</td><td>[D]</td>
    </tr>
    <tr>
      <td>114C</td><td>Estimated DPF Temperature</td><td>[D]</td>
    </tr>
    <tr>
      <td>114D</td><td>Soot Accumulation Ratio</td><td>[D]</td>
    </tr>
    <tr>
      <td>114E</td><td>Oil Dilution Ratio</td><td>[D]</td>
    </tr>
    <tr>
      <td>1155</td><td>Estimated Distance to Oil Change</td><td>[D]</td>
    </tr>
    <tr>
      <td>1156</td><td>Running Distance since last DPF Regeneration</td><td>[D]</td>
    </tr>
    <tr>
      <td>1157</td><td>DPF Regeneration Count</td><td>[D]</td>
    </tr>
    <tr>
      <td>1158, 1159, 115A, 115B</td>
      <td>Micro-Quantity-Injection Final Learning Values Cylinder #1 .. 4</td>
      <td>[D]</td>
    </tr>
    <tr>
      <td>1161</td>
      <td>Individual Pump Difference Learning Value</td>
      <td>[D]</td>
    </tr>
    <tr>
      <td>1162</td><td>Final Main Injection Period</td><td>[D]</td>
    </tr>
    <tr>
      <th colspan="3">Switches</th>
    </tr>
    <tr>
      <td>122F</td><td>Clutch Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1230</td><td>Stop Light Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1231</td><td>Cruise Control Set/Coast Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1232</td><td>Cruise Control Resume/Accelerate Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1233</td><td>Brake Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>1234</td><td>Cruise Control Main Toggle Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>124A</td><td>Cruise Control Cancel Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>124C</td><td>Oil Level Switch</td><td>[D][P]</td>
    </tr>
    <tr>
      <td>124F</td><td>Glow Relay Switch</td><td>[D]</td>
    </tr>
    <tr>
      <td>1254</td><td>Injector Learning</td><td>[D]</td>
    </tr>
    <tr>
      <td>125B</td><td>DPF Active Regeneration Switch</td><td>[D]</td>
    </tr>
    <tr>
      <th colspan="3">Following probably require authentication</th>
    </tr>
    <tr>
      <td>1189</td><td>Oil Dilution Amount</td><td>[D]</td>
    </tr>
    <tr>
      <td>102A, 102B, 102C, 102D</td>
      <td>Injector Code Cylinder #1 .. 4</td>
      <td>[D]</td>
    </tr>
  </tbody>
</table>


Details

Showing payload bytes only for brevity. Setup depends on software used. For example, to request SSMID, full write message bytes using J2534 interface using own application code or generic tool would be “00 00 07 E0 22 F1 00" as first four bytes make up tester/flow-control CAN-ID.

Example responses are provided for comprehension, however, these bytes are often artificially made up due to lack of an actual Euro 5+ car to play with. No guarantees of correctness as always.
SSMID

W: 22 F1 00
R: 62 F1 00 A2 10 14
→ 2.0L DOHC Turbo Diesel
From lookup table: System Names by SSMID
ROMID

W: 22 F1 82
R: 62 F1 82 70 44 D8 70 07
Vehicle Identification Number (VIN)

Returns 17 ASCII characters, similar to OBD-II Mode 0x09 PID 0x02.
W: 22 F1 90
R: 62 F1 90 4A 46 31 ** ** ** ** ** ** ** ** 31 32 33 34 35 36
(redacted)

→ "JF1********123456"

System String

N/A in other protocols. Returns 32 ASCII characters, bytes valued 0x20 are spaces.
W: 22 F1 97
R: 62 F1 97 32 2E 30 20 44 49 45 53 45 4C 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20

→ "2.0 DIESEL                      "

Coolant Temperature

formula: x-40 [°C], like SSM2 0x000008 and OBD-II Mode 0x01 PID 0x05
W: 22 00 05
R: 62 00 05 40
→ 0x40 = decimal 64; → result = 64 – 40 = 24 °C
Fuel Rail Pressure (diesel, or gasoline direct inject)

x*10 [kPa] = x/10 [bar] = ((A*256)+B)*10 [kPa], unlike SSM2 0x0001EC [MPa]
x: response payload data as 16 bit unsigned integer (uint16), big endian; alternative view: A = high (first) byte, B = low (second) byte
W: 22 00 23
R: 62 00 23 0B EA
→ 0x0BEA = decimal 3050; → result = 3050 * 10 = 30500 kPa = 305 bar
Exhaust Gas Temperature (EGT) at Catalyst Inlet

OBD-II name: “Catalyst Temperature
Bank 1, Sensor 1”
x/10-40 [°C] = ((A*256)+B)/10-40 like OBD-II Mode 0x01 PID 0x3C, but unlike SSM2 0x000277
x: response payload data as 16 bit unsigned integer (uint16), big endian; alternative view: A = high (first) byte, B = low (second) byte
W: 22 00 3C
R: 62 00 3C 0E D8
→ x = 0x0ED8 = decimal 3800; → result = 3800/10 – 40 = 340 °C
Exhaust Gas Temperature (EGT) at DPF Inlet

OBD-II name: “Catalyst Temperature Bank 1, Sensor 2”
x/10-40 [°C] = ((A*256)+B)/10-40 like OBD-II Mode 0x01 PID 0x3E, but unlike SSM2 0x000278
x: response payload data as 16 bit unsigned integer (uint16), big endian; alternative view: A = high (first) byte, B = low (second) byte
W: 22 00 3E
R: 62 00 3E 0D AC
→ x = 0x0DAC = decimal 3500; → result = 3500/10 – 40 = 310 °C
Primary Boost Control

    Diesel: VGT adjustment of turbocharger nozzle ring (low value → open → low turbo rpm)
    Petrol: Primary wastegate duty cycle.

x*100/255 [%], like SSM2 0x000030
W: 22 10 AC
R: 62 10 AC 64
→ 0x64 = decimal 100; → result = 100*100/255 = 39.2 %
Alternator Duty

x [%], like SSM2 0x00003A
W: 22 10 B2
R: 62 10 B2 00
→ 0x00 = decimal 0; → result = 0*100/255 = 0 %
Intake VVT Advance Angle Right

x-50 [deg], like SSM2 0x00003C
W: 22 10 B4
R: 62 10 B4 40
→ 0x40 = decimal 64; → result = 64 – 50 = 14 deg
Intake VVT Advance Angle Left

x-50 [deg], like SSM2 0x00003D
W: 22 10 B5
See 10B4
Memorised Cruise Speed

x [km/h], like SSM2 0x00010A
W: 22 10 E3
R: 62 10 E3 82
→ 0x82 = decimal 130; → result = 130 km/h
Final Injection Amount

x/256 [mm³/st] = A+B/256, like SSM2 0x0001E2
W: 22 11 16
R: 62 11 16 46 32
→ x = 0x4632 = decimal 17970; → result = 17970 / 256 = 70.195 mm³/st
or: → A = 0x46 = dec 70; B = 0x32 = dec 50; → result = 70 + 50 / 256 = 70.195 mm³/st
Exhaust Gas Recirculation (EGR) Target Valve Opening Angle

x-50 [deg], like SSM2 0x0001E8
W: 22 11 1B
R: 62 11 1B 78
→ 0x78 = decimal 120; → result = 120 – 50 = 70 deg
Exhaust Gas Recirculation (EGR) Valve Opening Angle

x-50 [deg], like SSM2 0x0001E9
W: 22 11 1C
R: 62 11 1C 3C
→ 0x3C = decimal 60; → result = 60 – 50 = 10 deg
Inlet Air Temperature (after air filter)

x-40 [°C], like SSM2 0x0001ED
W: 22 11 1F
R: 62 11 1F 42
→ 0x42 = decimal 66; → result = 66 – 40 = 26 °C
Target Engine Speed

x/4 [rpm] = (A*256+B)/4 like SSM2 0x0001EE
x: response payload data as 16 bit unsigned integer (uint16), big endian; alternative view: A = high (first) byte, B = low (second) byte
W: 22 11 21
R: 62 11 21 0C 90
→ x = 0x0C90 = decimal 3216; → result = 3216 / 4 = 804 rpm
Mileage after Injector Learning

x*5 [km] = (A*256+B)*5, like SSM2 0x0001FA
W: 22 11 2A
R: 62 11 2A 02 58
→ x = 0x0258 = decimal 600; → result = 600 * 5 = 3000 km
Mileage after Injector Replacement

x*5 [km] = (A*256+B)*5, like SSM2 0x000204
W: 22 11 2B
R: 62 11 2B 27 12
→ x = 0x2712 = decimal 10002; → result = 10002 * 5 = 50010 km
Interior Heater

x [steps], like SSM2 0x000270
W: 22 11 2C
R: 62 11 2C 01
→ x = 1 steps
Quantity Correction Cylinder #1

(x-100)/100 [ms] = (A-100)/100, like SSM2 0x00025D
W: 22 11 2D
R: 62 11 2D 71
→ x = 0x71 = decimal 113; → result = (113-100)/100 = 0.130 ms

Cylinders 2, 3, 4 require PIDs 112E, 112F, 1130 respectively.
Battery Current

x-128 [A], like SSM2 0x000271
positive result = charging battery, negative = discharching
W: 22 11 35
R: 62 11 35 8A
→ 0x8A = decimal 138; → result = 138 – 128 = 10 A (charging)
Battery Temperature

x-40 [°C], like SSM2 0x000273
W: 22 11 36
R: 62 11 36 3B
→ 0x3B = decimal 59; → result = 59 – 40 = 19 °C
Cumulative Ash Ratio

x [%], like SSM2 0x000275
W: 22 11 49
R: 62 11 49 20
→ 0x20 = decimal 32; → result = 32 %
Pressure Difference between DPF Inlet and Outlet

x [kPa], like SSM2 0x000276
W: 22 11 4A
R: 62 11 4A 10
→ 0x10 = decimal 16; → result = 16 kPa
Estimated Catalyst Temperature

x*5-40 [°C], like SSM2 0x000279; calculated by ECU algorithm
W: 22 11 4B
R: 62 11 4B 45
→ 0x45 = decimal 69; → result = 69 * 5 – 40 = 305 °C
Estimated DPF Temperature

x*5-40 [°C], like SSM2 0x00027A; calculated by ECU algorithm
W: 22 11 4C
R: 62 11 4C 44
→ 0x44 = decimal 68; → result = 68 * 5 – 40 = 300 °C
Soot Accumulation Ratio

x [%], like SSM2 0x00027B
W: 22 11 4D
R: 62 11 4D 20
→ 0x20 = decimal 32; → result = 32 %
Oil Dilution Ratio

x [%], like SSM2 0x00027C
W: 22 11 4E
R: 62 11 4E 04
→ 0x04 = decimal 4; → result = 4 %
Note

On known Euro 4 and early 5 models the relationship is:
DistanceToOilChange[km] = 15000 - 1500 * OilDilutionRatio[%]
therefore a more precise oil dilution percentage value (roughly one decimal place) can be achieved by querying PID 1155 and calculating:
OilDilutionRatio[%] = 10 - DistanceToOilChange[km] / 1500

    Examples:
    OilDilutionRatio = 10 – 8100 / 1500 = 4.6 %
    OilDilutionRatio = 10 – 8200 / 1500 = 4.5 %

Estimated Distance to Oil Change

x*100 [km], like SSM2 0x00029A
W: 22 11 55
R: 62 11 55 56
→ x = 0x56 = decimal 86; → result = 86 * 100 = 8600 km
Note

On known Euro 4 and early 5 models this parameter derives directly from oil dilution, see post and PID 114E. Please confirm that this calculation is still correct:
DistanceToOilChange[km] = 15000 - 1500 * OilDilutionRatio[%]

If true, you could also calculate Oil Dilution Ratio (normally PID 114E) using this PID 1155 instead, getting better precision:
→ OilDilutionRatio[%] = 10 - DistanceToOilChange[km] / 1500
→ OilDilutionRatio[%] = 10 - (x*100) / 1500 = 10-x/15
→ x = 0x56 = decimal 86; → OilDilutionRatio = 10 – 86/15 = 4.27 %
Running Distance since last DPF Regeneration

x [km] = A*256+B like SSM2 0x00029B
x: response payload data as 16 bit unsigned integer (uint16), big endian; alternative view: A = high (first) byte, B = low (second) byte
W: 22 11 56
R: 62 11 56 02 34
→ x = 0x0234 = decimal 564; → result = 564 km
DPF Regeneration Count

x [-] = A*256+B like SSM2 0x00029D; tracks fully completed regenerations only
x: response payload data as 16 bit unsigned integer (uint16), big endian; alternative view: A = high (first) byte, B = low (second) byte
W: 22 11 57
R: 62 11 57 01 23
→ x = 0x0123 = decimal 291; → result = 291 regenerations
Micro-Quantity-Injection Final Learning Values Cylinder #1

These are static learning values, updated after Injector Learning / Calibration procedure had been completed.
Resultant five payload data bytes represent five raw values for Pressure Level #1 .. 5.
(x[i]-128)/200 [ms] like SSM2 0x00023D ...
W: 22 11 58
R: 62 11 58 81 72 93 84 95
Pressure Level #1 → x = x[0] = 0x81 = decimal 129; → result = (129-128)/200 = 0.005 ms
Pressure Level #2 → x = x[1] = 0x72 = decimal 114; → result = (114-128)/200 = -0.070 ms
…

Cylinders 2, 3, 4 require PIDs 1159, 115A, 115B respectively.
Individual Pump Difference Learning Value

This is about SCV (Suction Control Valve).
x-1000 [mA] = ((A*256)+B)-1000 like SSM2 0x000238
W: 22 11 61
R: 62 11 61 03 B1
→ x = 0x03B1 = decimal 945; → result = 945-1000 = -55 mA
Final Main Injection Period

x/1000 [ms] = ((A*256)+B)/1000 like SSM2 0x000257
W: 22 11 62
R: 62 11 62 02 B5
→ x = 0x02B5 = decimal 693; → result = 693/1000 = 0.693 ms
Oil Dilution Amount

Might require authentication!

x/200 [kg] = x*5 [g], like SSM2 0x0002A2 (Euro 4 only)
W: 22 11 89
R: 62 11 89 32
→ x = 0x32 = decimal 50; → result = 50 * 5 = 250 g
Oil Level Switch

like SSM2 0x000196 bit 5
W: 22 12 4C
R: 62 12 4C FF
00 → LOW; FF → HIGH (normal)
Glow Relay Switch

like SSM2 0x000197 bit 5
W: 22 12 4F
R: 62 12 4F FF
00 → OFF; FF → ON
Injector Learning

like SSM2 0x000197 bit 0
W: 22 12 54
R: 62 12 54 00
00 → OFF (not in progress); FF → ON (in progress)
DPF Active Regeneration Switch

like SSM2 0x0001CE bit 3
W: 22 12 5B
R: 62 12 5B 00
00 → OFF (not in progress); FF → ON (in progress)
Injector Codes

Require authentication!

Read cylinder #1 injector code:
W: 22 10 2A
R: 62 10 2A B2 ** ** ** ** ** ** ** ** ** ** ** ** 00 XX

Cylinders 2, 3, 4 require PIDs 102B, 102C, 102D respectively.
Byte index [0..14] 	Content
0 	const: B2 (Euro 5) or B3 (Euro 4)
1..12 	12 payload bytes
13 	const 00
14 	simple XOR checksum

Link to related post: Injector Codes
Updates

    2015-12-10: updated downloads (.ods), added 6 additional diesel PIDs (1158 .. 1162)
    2015-11-15: updated downloads (.ods, added link to .csv), added 9 additional PIDs (cruise control mostly)
    2015-11-12: updated download (.ods), 5 additional PIDs for diesel models: 112C, 112D, …
    2015-10-27: added download (.ods), PIDs: 10AC, 112B
    2015-10-26: corrected some formulas that refer to individual bytes (A, B)
    2015-10-18: added PIDs: Final Injection Amount 1116; EGR Valve Angle: 111B, 111C; added URLs for app Engine Link
    2015-10-09: added PIDs: 10B4, 10B5, 1121, 124C
    2015-10-06: added PIDs for Battery Current/Temp, Inlet Air Temp, Injector Learning …
    2015-10-04: added notes for Distance to Oil Change and Oil Dilution Ratio (better precision)
    2015-10-03: added 3 DPF related PIDs: 114A, 1155, 1156
    2015-09-30: added overview table, external links (Torque etc.)
    2015-09-24: corrected “Exhaust Gas Temperature (EGT) at DPF Inlet”, added “DPF Regeneration Count”, improved formatting
