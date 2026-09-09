# PART A — SYSTEM MODEL (Phase 0 Extraction)
## A380 ATA 34 — Air Data / Inertial Reference System (ADIRS) & Standby Navigation System (ISIS)

**Source note sets**

| Tag | Document | Sections used | Doc pages | Date |
|---|---|---|---|---|
| **L1** | A380 TTM — MAINTENANCE COURSE T1+T2 (RR/Metric), LEVEL I – ATA 34 Navigation | Navigation Systems Introduction (1); Air Data & Inertial Reference System Pres. (1); Standby Navigation System Presentation (1) | 2–11 | Apr 19, 2007 |
| **L2/3** | A380 TTM — MECHANICAL & AVIONICS COURSE T1+T2 (LVL 2&3) (RR Trent 900), 34 – Navigation | Navigation Systems Description (2); ADIRS Description (3); Navigation Systems OPS/CTL & IND (2); Standby Navigation System Description (3); Navigation Systems Maintenance (3) | 2–19, 20–39 | Nov 21, 2011 (rev 01 AUG 2013) |

**Scope:** ADIRS (ADR + IR) and SNS/ISIS only. VOR/DME/ADF/MMR/RA/AESS/OANS are out of scope except where they interface with ADIRS or ISIS.

---

## 0.1 COMPONENTS

| id | Full name | Acronym | Type | Quantity / identifiers (quoted from notes) | Key ratings quoted | Location as the notes give it |
|---|---|---|---|---|---|---|
| ADIRU1 | Air Data / Inertial Reference Unit 1 | ADIRU | computer/unit | "3 Air Data/Inertial Reference Units (ADIRUs)"; "each ADIRU has 2 parts: the Air Data Reference (ADR) part and the Inertial Reference (IR) part" | 115 VAC = AC EMER BUS; 28 VDC PRIMARY = DC ESS BUS; 28 VDC BACK-UP (10 sec) = HOT BUS 1 | "installed in the main avionics bay" (L2/3 p2); diagram L2/3 p3 shows ADIRU 1 and ADIRU 3 forward, ADIRU 2 aft in the avionics bay |
| ADIRU2 | Air Data / Inertial Reference Unit 2 | ADIRU | computer/unit | as above | 115 VAC = AC BUS 4; 28 VDC PRIMARY = DC BUS 2; 28 VDC BACK-UP = **NOT POWERED** | main avionics bay |
| ADIRU3 | Air Data / Inertial Reference Unit 3 | ADIRU | computer/unit | as above; "ADIRU 3 is mainly in standby" (L1 p4) | 115 VAC = AC BUS 1 / AC EMER BUS; 28 VDC PRIMARY = DC ESS BUS; 28 VDC BACK-UP (10 sec) = HOT BUS ESS | main avionics bay |
| ADR | Air Data Reference part | ADR | computer sub-function | 1 per ADIRU (3 total) | — | inside ADIRU |
| IR | Inertial Reference part | IR | computer sub-function | 1 per ADIRU (3 total); "Three accelerometers, one for each axis"; "Three gyros, one for each rotation axis" | — | inside ADIRU |
| BITE-ADR / BITE-IR | Built-In Test Equipment module | BITE | controller/monitor | "A BITE module is hosted in ADR part"; "A BITE module is hosted in IR part" — for OMS communication | — | inside each ADR / IR part |
| MFP1/2/3 | MultiFunction Probe | MFP | probe/sensor | "There are three MFPs. Each ADIRU is connected to one MFP. One MFP is installed on the left hand side of the A/C and the two others are installed on the right hand side." | 115 VAC (digital converter + anti-icing). Gives AOA, TAT, Pt | "installed on the FWD fuselage" (L2/3 p2); L1 p6: "located on the right or left hand side of the FWD fuselage" |
| ISP 1-1…3-2 | Integrated Static Probe | ISP | probe/sensor | "There are six ISPs. Each ADIRU is connected to two ISPs. Three ISPs are installed on the right hand side of the A/C, and three others are installed on the left hand side." Diagram labels: ISP 1-1, ISP 2-1, ISP 3-1 (LH) and ISP 1-2, ISP 2-2, ISP 3-2 (RH) | "28VDC power supply for digital converter and 115VAC for anti-icing function". Gives local Static Pressure (Ps) | "installed on the FWD fuselage" |
| SSA1/2/3 | Side Slip Angle probe | SSA | probe/sensor | "There are three SSA probes. Each ADIRU is connected to one SSA probe." Diagram: SSA 1, SSA 2, SSA 3 | 115 VAC. "The probe has a wind vane to measure the local SSA" | "installed on the upper part of the nose side of the A/C, just below the windshields" |
| OAT1/OAT2 | Outside Air Temperature probe | OAT | probe/sensor | "There are two OAT probes, installed on the Nose Landing Gear (NLG)". "The OAT probe located on the left hand of the NLG is connected to ADIRU 1"; "the right hand … is connected to ADIRUs 2 and 3" | "directly energized by the ADIRUs"; "heat resisting probes"; "transmits an analog signal" | Nose Landing Gear (NLG) |
| ICP02A | ADIRS Integrated Control Panel | ICP / ICP-ADIRS | control panel | "1 ADIRS control Panel (1221VM) which is common to the 3 ADIRUs"; "ADIRS ICP02A (part of panel 1221VM)"; "made of three independent channels, one for each ADIRU" | — | "installed on the overhead panel" |
| SWTCH | ADIRS SWITCHING panel | — | control panel | "1 SWITCHING panel (1311VU) for the selection of the ADR 3 or IR 3"; "Two rotary selectors are installed on panel 1311VU" | — | "installed on the front panel" / "main instrument panel" |
| ISIS1 | Integrated Standby Instrument System 1 | ISIS | display + computer | "2 independent Integrated Standby Instruments System (ISIS) units"; identified (1311VU) on L1 p11 / L2/3 p29 captions. "The ISIS units are interchangeable." | Normal supply: 28 VDC BUS 1 / ESS BUS (diagram L2/3 p32). Normal mode: standby **flight** display | "installed at the center of the main instrument panel" |
| ISIS2 | Integrated Standby Instrument System 2 | ISIS | display + computer | as above | 28 VDC BUS 2 / ESS BUS. Normal mode: standby **navigation** display | centre of main instrument panel |
| STBY-PITOT | Standby pitot probe | — | probe/sensor | "1 standby pitot probe" | "supplied with 115VAC by the AC ESS BUS bar". Gives Total Pressure (Pt) | "installed on the left FWD fuselage" (L2/3 p28); L1 p10: "located on the left FWD fuselage" |
| STBY-STAT-L / -R | Standby static probes | — | probe/sensor | "2 standby static probes" | "supplied with 115VAC by normal AC bus bars"; diagram L2/3 p32: 115 VAC BUS 2 each. Give Static Pressure (Ps) | "installed on the left and right FWD fuselage on the nose front fairing" |
| STBY-COMPASS | Standby magnetic compass | — | sensor / indicator | "1 standby magnetic compass" | Gives A/C magnetic heading | "installed on the top of the windshield center post"; a COMPENSATION CARD is shown adjacent (L2/3 p29) |
| ADCN | Avionics Data Communication Network (AFDX) | ADCN / AFDX | network | 1 network | Carries ADR and IR data to A/C systems and CDS | Avionics world |
| A429 | ARINC 429 buses | ARINC 429 | network | Probe→ADIRU; ADIRU→ISIS; ISIS→MMR1/OMS/FCU/PRIMs/IOM/CDAM; ADR→LGERS; back-up path for ADR/IR data | — | — |
| CDS | Control and Display System (CAPT PFD/ND, F/O PFD/ND, MFDs) | CDS | display | 2 PFDs, 2 NDs, MFDs (per diagrams) | — | glareshield / main instrument panel |
| EFIS CP | EFIS Control Panels | EFIS CP | control panel | "2 EFIS Control Panels, installed on the glareshield, allowing the baro-reference setting" | — | glareshield |
| KCCU | Keyboard Cursor and Control Unit | KCCU | control panel | "2 Keyboard Cursor and Control Units (KCCUs), located on the pedestal" | — | pedestal |
| VMO/MMO SW | Maximum Operating Speed / Mach switch | VMO/MMO | switch | 1 switch, discrete to ADR | "used for ferry flights with landing gear down" | "lower part of the main avionics bay, between the ADIRUs 1 and 3" |
| MMR1/MMR2 | Multi Mode Receiver | MMR | data source | MMR 1 and MMR 2 shown; "Each ISIS is interfaced with the Multi Mode Receiver (MMR) 1" | Supplies GPS data to IR; receives GPIRS data | — |
| FCU / FCU back-up | Flight Control Unit / FCU back-up in CPIOMs-C | FCU | data source | 1 FCU + FCU back-up application hosted in CPIOMs-C | Supplies baro-setting and TRUE/MAG selection | glareshield / CPIOM-C |
| LGERS | Landing Gear Extension and Retraction System | LGERS | data source | — | Receives CAS via ARINC 429; supplies GND/FLT discrete | — |
| OMS / SCI / CDAM | Onboard Maintenance System / Secure Communication Interface / Centralized Data Acquisition Module | OMS, SCI, CDAM | maintenance | — | ADR & IR BITE ↔ OMS; ISIS ↔ OMS via SCI (ARINC 429 + discrete); ISIS air/inertial data → CDAM | — |
| PRIMs / FCGUs | PRIMary computers, Flight Guidance Computer Units | PRIM, FCGU | user system | "two Flight Guidance Computer Units (FCGUs) included in each one of the three PRIMary (PRIM) systems" | ISIS sends air/inertial data "in case of two ADIRS failure" | — |
| FWS / IOM | Flight Warning System via Input/Output Module | FWS, IOM | user system | FWS application "hosted in the CPIOM-C" | ISIS status & warning data via IOM | — |

---

## 0.2 TOPOLOGY

**Probes → ADIRUs** (each probe except OAT has an internal air-data/digital converter; ARINC 429 to the ADIRU)

| From | via | to |
|---|---|---|
| MFP 1 (AOA, TAT, Pt) | integrated digital converter → ARINC 429 | ADIRU 1 (ADR) |
| MFP 2 | digital converter → ARINC 429 | ADIRU 2 (ADR) |
| MFP 3 | digital converter → ARINC 429 | ADIRU 3 (ADR) |
| ISP 1-1 and ISP 1-2 (Ps) | digital converter → ARINC 429 | ADIRU 1 (ADR) |
| ISP 2-1 and ISP 2-2 | digital converter → ARINC 429 | ADIRU 2 (ADR) |
| ISP 3-1 and ISP 3-2 | digital converter → ARINC 429 | ADIRU 3 (ADR) |
| SSA 1 / SSA 2 / SSA 3 | digital converter → ARINC 429 | ADIRU 1 / 2 / 3 (ADR) |
| OAT 1 (LH of NLG) | analog signal (no converter; energised by the ADIRU) | ADIRU 1 (ADR) |
| OAT 2 (RH of NLG) | analog signal | ADIRU 2 **and** ADIRU 3 (ADR) |

**Other inputs to the ADIRU**

| From | via | to |
|---|---|---|
| MMR 1 / MMR 2 (GPS data) | ARINC 429 | IR part of each ADIRU |
| FCU / FCU back-up (CPIOMs-C) — baro-setting | ARINC 429 | ADR part |
| FCU / FCU back-up — "TRUE/MAG" selection | ARINC 429 | IR part |
| LGERS — GND/FLT | discrete | ADR part |
| VMO/MMO switch position | discrete | ADR part |
| ICP02A (selector SW, IR P/BSW, ADR P/BSW) | discrete | ADIRU (IR OFF/ADR OFF, NAV MODE, ATT MODE, IR BUS ON/OFF, ADR BUS OFF/ON) |
| 1311VU switching panel | discrete ("ADIRU 3 RECONFIGURATION" line, via IOM-A) | ADIRU 3 and the CDS display routing |

**ADIRU outputs**

| From | via | to |
|---|---|---|
| ADR part | AFDX interface via ADCN (primary); ARINC 429 (back-up) | A/C systems (AGS, AICUs, APU ECB, ATC, BCS, CPCS, FQMS, SEC…) and CDS |
| IR part | AFDX via ADCN (primary); ARINC 429 (back-up) | A/C systems and CDS |
| ADR part — CAS | ARINC 429 | LGERS |
| IR part — GPIRS data | ARINC 429 | MMRs |
| ADR + IR of **ADIRU 1 and ADIRU 3** | ARINC 429 | ISIS 1 and ISIS 2 |
| ADIRU 1 or ADIRU 3 | discrete | ISIS probes automatic anti-icing activation |
| ADR/IR BITE | — | OMS |
| ADIRU 1 (IR1 + ADR1 data) | ADCN | CAPT PFD and CAPT ND |
| ADIRU 2 (IR2 + ADR2 data) | ADCN | F/O PFD and F/O ND |
| ADIRU 3 (IR3 + ADR3 data) | ADCN, selected by 1311VU | CAPT side (CAPT ON 3) or F/O side (F/O ON 3) |
| ADIRS status | ADCN | CDAM → OMS |

**Switching-panel paths (1311VU)** — see 0.4 for the truth table

- ATT HDG selector NORM → IR1 → CAPT PFD/ND; IR2 → F/O PFD/ND; IR3 standby
- ATT HDG selector CAPT ON 3 → IR3 replaces IR1 on the CAPT side
- ATT HDG selector F/O ON 3 → IR3 replaces IR2 on the F/O side
- AIR DATA selector — same three positions, same philosophy, acting on the ADR part

**ISIS**

| From | via | to |
|---|---|---|
| Standby pitot probe (Pt) | pneumatic link | ISIS 1 and ISIS 2 |
| Standby static probes L and R (Ps) | pneumatic link | ISIS 1 and ISIS 2 |
| ISIS ↔ ISIS | discrete links | automatic reconfiguration between the two ISIS |
| ADIRU 1 and ADIRU 3 (IR data) | ARINC 429 | ISIS 1 and ISIS 2 |
| MMR 1 (LS: LOC & Glide; GPS: ground speed, lat/long) | ARINC 429 | each ISIS |
| ISIS | ARINC 429 + discrete link, via SCI | OMS (maintenance data, test results) |
| ISIS ↔ FCU and FCU back-up (CPIOMs-C) | — | magnetic/true heading selection data |
| ISIS | ARINC 429 | FCGUs of the three PRIM systems |
| ISIS output 1 — status & warning data | ARINC 429 via IOM | FWS application in CPIOM-C |
| ISIS output 2 — air data & inertial data | ARINC 429 | CDAM |
| Standby magnetic compass | direct reading | flight crew (magnetic heading) |

---

## 0.3 CONTROLS

### ADIRS Integrated Control Panel ICP02A — panel **1221VM**, overhead panel
Three independent channels, one per ADIRU.

| Control | Positions | What each position commands | Indications on it |
|---|---|---|---|
| Selector SW (×3: one per ADIRU) | **OFF / NAV / ATT** | OFF = ADIRU not powered ("IR OFF/ADR OFF"). NAV = "the normal position to energize and use the related ADIRU" → NAV MODE. ATT = "could be selected in case of partial failure (mainly at the accelerometers level) of the related ADIRU" → ATT MODE; "the ADIRU only gives heading and attitude data if the system loses its ability to navigate. The heading has to be entered through the MFD." | Rotary knob position only (no light stated) |
| IR P/BSW (×3: IR1, IR2, IR3) — momentary action | ON (released) / OFF (pushed) | "normally in 'ON' position (no light), to be selected to the 'OFF' position (white light) in case of failure of the IR part of the ADIRU". Commands IR BUS ON/OFF, IR BUS OFF | **FAULT** legend (amber) when the IR part fails; **OFF** legend (white) when the IR output buses are disabled — "the IR sends a discrete IR OFF signal to cause the OFF legend to come on". FAULT **flashing** with OFF extinguished = "ADIRU failure with possibility to keep attitude function" |
| ADR P/BSW (×3: ADR1, ADR2, ADR3) — momentary action | ON / OFF | "same philosophy but relative to the ADR part of the related ADIRU"; controls each ADR data transmission (ON/OFF). Commands ADR BUS OFF/ON | **FAULT** (amber) and **OFF** (white) legends, same logic as IR P/BSW |
| PROBE/WINDOW HEAT P/BSW | **AUTO** (default) / **ON** | AUTO = anti-icing operated automatically by ADIRS. ON = manual activation "when the A/C is on ground with no engine running" | "ON" legend; panel is marked AUTO / O |

### ADIRS SWITCHING panel — panel **1311VU**, main instrument (front) panel
Two rotary selectors, "their standard position is 12 o'clock 'NORM'".

| Control | Positions | What each position commands | Indications |
|---|---|---|---|
| **ATT HDG** (upper rotary) — IR SELECTOR SW | **CAPT ON 3 / NORM / F/O ON 3** | NORM: ADIRU1 → CAPT PFD/ND, ADIRU2 → F/O PFD/ND, ADIRU3 standby. CAPT ON 3: "the IR part of ADIRU3 will replace IR part of ADIRU1". F/O ON 3: "the IR part of ADIRU 3 will replace IR part of ADIRU2" | Knob position; "any switching situation other than normal position will trigger a message on the ECAM (EWD/PFD memo part)" |
| **AIR DATA** (lower rotary) — ADR SELECTOR SW | **CAPT ON 3 / NORM / F/O ON 3** | "The 'AIR DATA' lower rotary selector follows the same philosophy for the AIR DATA part of the ADIRUs" | as above |

Use: "These switches are used in case of failure of the IR or the AIR DATA part of the ADIRU1 or ADIRU2, or in case of discrepancy of parameters shown between CAPT and F/O EFIS Display Units (PFDs/NDs)." "The Switching will also have consequences on ADIRUs power supply."

### ISIS front face — 5 P/BSWs, a rotary knob P/B and a light sensor

| Control | Function |
|---|---|
| **MODE** P/BSW | "used to switch off a display or to perform a manual reconfiguration of the two ISIS" (recovers the standby navigation display after an automatic reconfiguration) |
| **LS/Dir TO** P/BSW | "gives directly access to LS information in standby flight display mode and calls the Dir TO function in standby navigation display mode" |
| **PLUS (+) BRIGHTNESS** P/BSW | increase display brightness |
| **MINUS (−) BRIGHTNESS** P/BSW | decrease display brightness |
| **MENU** P/BSW | "used to display the menu and select options or to reset an instrument" |
| **SET/SEL** rotary knob / pushbutton | "used to set and select data, and to access to the maintenance menu". On standby **flight** display mode: sets barometric pressure reference by pushing (first press: STD; second press: setting of the barometric pressure) and enables setting/selection of items when MENU is used. On standby **navigation** display mode: "only used for the setting/selection of the items, when the MENU P/BSW is used" |
| Light sensor | "automatic setting of the brightness of display according to the cockpit ambient light" |

### Other controls in scope
| Control | Positions / function |
|---|---|
| EFIS control panel — BARO SETTING knob | baro-reference setting sent to the ADR part |
| EFIS CP — TAXI PBSW (green bars) | must be **off** before ADIRS start (powering procedure) |
| KCCU + MFD POSITION/IRS page | manual IR alignment: **ALIGN ON OTHER REF**, enter lat/long, **ALIGN IRS**; also **FREEZE ALL IRS**, **SET HDG**, IRS1/IRS2/IRS3 tabs |
| VMO/MMO switch | defines the new Vmo/Mmo value; ferry flights with landing gear down |

---

## 0.4 LOGIC (IF/THEN, priority ordered)

**L1 — Power-up and power transfer**
1. IF selector SW = NAV or ATT THEN the related ADIRU is energised (the rotary selector powers each ADIRU).
2. IF the ADIRU is powered up THEN "at each power-up, the ADIRU will do an internal test and will verify its power supply. It will verify if it receives the 28 VDC and 115 VAC on its inputs, and will internally switch from the main (115 VAC) to the back-up (28 VDC) power to test the electrical generation."
3. IF the main 115 VAC "exceeds its normal limits" THEN "each ADIRU transfers automatically from primary to back-up generation" (28 VDC).
4. IF loss of main AC electrical generation THEN ADIRU 1 and ADIRU 3 are supplied from the **AC EMER bus**; ADIRU 2 (AC BUS 4) is lost. 28 VDC gives the back-up generation: HOT BUS 1 (ADIRU 1) and HOT BUS ESS (ADIRU 3) for 10 sec; ADIRU 2 back-up = NOT POWERED.

**L2 — IR alignment / mode**
5. IF the IR selector is switched to **NAV** THEN "the Inertial Reference System (IRS) is automatically initialized on the Global Position System (GPS) position at the end of alignment period."
6. Alignment duration: "depends on the aircraft position and may vary from 5 to 17 minutes."
7. Manual alignment (MFD POSITION/IRS): select ALIGN ON OTHER REF → enter lat/long → select ALIGN IRS; THEN "after ten seconds, the ALIGN indications replace the INVALID indications. The AVAIL IN 7 MIN indications come into view"; when aligned, "the NAV indications replace the ALIGN indications."
8. IF alignment is not complete THEN air information is "immediately displayed on the PFDs", but navigation information on the NDs — and IR data on the PFDs — is available only "after the complete alignment."
9. IF selector = **ATT** THEN the ADIRU gives heading and attitude only ("if the system loses its ability to navigate"), and "the heading has to be entered through the MFD" (SET HDG).

**L3 — Normal source allocation (CDS)**
10. NORM: ADIRU 1 → CAPT PFD and CAPT ND; ADIRU 2 → F/O PFD and F/O ND; ADIRU 3 → standby (available for EFIS display function).

**L4 — Switching panel reconfiguration (1311VU) — ADIRUs SWITCHING truth table (L2/3 p17)**

| Selector position | CAPT | F/O | STAND BY |
|---|---|---|---|
| **NORMAL** | ADIRU 1 | ADIRU 2 | ADIRU 3 |
| **CAPT ON 3** | ADIRU 3 | ADIRU 2 | — (no standby) |
| **F/O ON 3** | ADIRU 1 | ADIRU 3 | — (no standby) |

11. ATT HDG selector acts on the **IR** part only; AIR DATA selector acts on the **ADR** part only — they are independent, so e.g. AIR DATA CAPT ON 3 with ATT HDG NORM is a valid configuration (ADR3 to CAPT, IR1 to CAPT).
12. IF either selector ≠ NORM THEN an ECAM message is triggered on the EWD/PFD memo part.
13. IF electrical emergency configuration (loss of normal busses) **AND** "CAPT ON 3" selected on the ADIRS switching panel THEN "system 1 will no longer be supplied and system 3 will take system 1" (probe systems).

**L5 — ADIRU 1 failure handling (Level 2/3 procedure)**
14. IF ADR 1 fails (selector in NAV) THEN ADR 1 PBSW **FAULT** legend comes on; ADR 1 warning flags shown on ND, PFD and ISIS (SPD, ALT, V/S); ECAM message + check list on EWD. THEN crew selects AIR DATA = CAPT ON 3 (ADR of ADIRU 3), THEN depresses ADR 1 PBSW → output buses disabled → ADR sends a discrete ADR OFF signal → **OFF** legend on.
15. IF IR 1 fails (selector in NAV) THEN IR 1 PBSW FAULT legend lights; IR 1 warning flags on ND, PFD and ISIS (ATT, HDG); ECAM message + check list. THEN crew selects ATT HDG = CAPT ON 3, THEN depresses IR 1 PBSW → IR sends discrete IR OFF → OFF legend on.
16. IF ADIRU 1 failure **with possibility to keep attitude function** THEN ECAM message + check list; on the IR PBSW "the FAULT legend is flashing and the OFF legend is extinguished". THEN "to extinguish the FAULT legend, turn the selector ADIRU 1 to the ATT position."

**L6 — Probe anti-icing activation (L2/3 p9, p10)**
17. AUTOMATIC MODE: IF (at least one engine is running) OR (IR Ground Speed > 30 kts) THEN probe anti-icing activated.
18. MANUAL MODE: IF A/C on ground with no engine running AND PROBE/WINDOW HEAT P/BSW pressed THEN probe anti-icing activated.
19. Logic gate form (diagram): (ENGINE RUNNING **OR** GS > 30 kts) **OR** (PROBE/WINDOW HEAT PB, on ground) → PROBE ANTI-ICING ACTIVATION.

**L7 — ISIS logic**
20. Normal configuration: ISIS 1 = standby **flight** display; ISIS 2 = standby **navigation** display. "Each ISIS is capable of doing all the functions of either standby flight display or standby navigation display."
21. IF ISIS 1 fails THEN "ISIS 2 is automatically reconfigured in standby flight display mode" (via the discrete links between the two ISIS).
22. IF ISIS 2 has been auto-reconfigured to flight display THEN "it is possible to recover the standby navigation display again by an action on the MODE P/BSW."
23. ISIS source selection: "Basically, the ISIS displays the data coming from ADIRU 3. In case of failure of the ADIRU 3, ISIS will switch to ADIRU 1."
24. ISIS probes anti-icing discrete comes from ADIRU 1 or 3 with the conditions: one engine running, or GS > 30 kts; and from the ISIS itself with: CAS > 50 kts. Manual activation via the ICP ADIRS.
25. IF two ADIRS fail THEN ISIS sends air data and inertial data to the FCGUs of the PRIM systems via ARINC 429.
26. ISIS supply: normal DC buses; "In case of emergency electrical configuration, their supply changes to DC essential bus."

**L8 — Data-path priority**
27. Primary transmission of ADR and IR parameters is AFDX via ADCN; "or in back-up using ARINC 429".

**L9 — Powering procedure (ADIRS 1; "use the same procedure to start ADIRS 2 and 3")**
28. EFIS CP TAXI PBSW green bars off → 1311VU AIR DATA = NORM and ATT HDG = NORM → on 1221VM check the FAULT and OFF legends of the three IR and three ADR PBSWs are off and set the three OFF/NAV/ATT selectors to NAV → on PFDs, SPD/ALT/V/S (ADR) warning flags not shown after **ten seconds**; HDG warning flag **is** shown and the ATT warning flag not shown after **thirty seconds** → on the NDs, HDG warning flags are shown → check the same parameters on ISIS.

---

## 0.5 STATES

| State | Configuration | Buses / sources live | Display consequence |
|---|---|---|---|
| **S0 — OFF** | All three selectors OFF | ADIRUs not energised | All ADIRS flags on PFD/ND; ISIS still available (own sensors) |
| **S1 — Powering / self-test** | Selectors moved to NAV; each ADIRU runs internal test and verifies 115 VAC and 28 VDC inputs, momentarily switching to back-up power | 115 VAC primary + 28 VDC | SPD/ALT/V/S flags clear after 10 s; ATT flag clears after 30 s; HDG flag remains |
| **S2 — Alignment in progress** | IR selectors NAV; automatic alignment on GPS position; 5–17 min | Normal | POSITION/IRS shows ALIGN (then AVAIL IN 7 MIN on manual align); air data on PFDs immediately; ND navigation data and PFD IR data only after complete alignment; HDG warning flags shown on NDs |
| **S3 — Normal three-channel** | 1311VU both selectors NORM; all three ADIRUs in NAV, POSITION/IRS shows IRS1/2/3 = NAV | ADIRU1: AC EMER BUS + DC ESS BUS; ADIRU2: AC BUS 4 + DC BUS 2; ADIRU3: AC BUS 1/AC EMER BUS + DC ESS BUS | CAPT PFD/ND from ADIRU1, F/O PFD/ND from ADIRU2, ADIRU3 standby; ISIS1 flight display, ISIS2 nav display |
| **S4 — ADIRU 1 (or ADR1/IR1) failed, CAPT ON 3** | ATT HDG and/or AIR DATA = CAPT ON 3; ADR1/IR1 PBSW pushed OFF | ADIRU 3 feeds CAPT side; no standby channel remains | CAPT PFD/ND fed by ADIRU 3; FAULT then OFF legends on ADR1/IR1 PBSW; ECAM memo for abnormal switching |
| **S5 — ADIRU 2 failed, F/O ON 3** | ATT HDG and/or AIR DATA = F/O ON 3 | ADIRU 3 feeds F/O side; no standby channel | F/O PFD/ND fed by ADIRU 3; ECAM memo |
| **S6 — Partial ADIRU failure, ATT mode** | Selector of the affected ADIRU turned to ATT | ADIRU powered | Heading and attitude only; heading must be entered via the MFD (SET HDG); FAULT legend extinguishes when ATT selected |
| **S7 — Loss of main AC generation (electrical emergency)** | ADIRU 1 and ADIRU 3 supplied from the **AC EMER BUS**; ADIRU 2 lost (AC BUS 4 gone) | 28 VDC back-up: HOT BUS 1 (ADIRU1) and HOT BUS ESS (ADIRU3) for 10 sec; ADIRU 2 has no 28 VDC back-up. ISIS supply changes to the DC essential bus | CAPT and standby channels retained; F/O side needs F/O ON 3. Probe systems: if also "CAPT ON 3", system 1 is no longer supplied and system 3 takes system 1 |
| **S8 — 28 VDC back-up** | Automatic transfer whenever 115 VAC exceeds its normal limits | ADIRU1 → HOT BUS 1; ADIRU3 → HOT BUS ESS; both quoted "(10 sec)" | Continuity of ADIRU 1 and 3 only |
| **S9 — ADIRS lost, ISIS as back-up** | SNS is "the back-up system in case of ADIRS failure or CDS failure" | ISIS on normal DC buses (or DC ESS bus in emergency); standby pitot 115 VAC AC ESS BUS; standby statics 115 VAC BUS 2 | ISIS 1 standby flight display + ISIS 2 standby navigation display; standby magnetic compass for magnetic heading; on two-ADIRS failure ISIS also feeds the PRIM FCGUs |
| **S10 — ISIS 1 failed** | Automatic reconfiguration through the ISIS-to-ISIS discrete links | — | ISIS 2 becomes standby flight display; navigation display recoverable by MODE P/BSW |
| **S11 — ADIRU 3 failed (ISIS source)** | ISIS switches its ADIRU source | — | ISIS takes ADIRU 1 instead of ADIRU 3 |

---

## 0.6 INDICATIONS

**Control-panel lights (1221VM)**
- IR1/IR2/IR3 P/BSW: amber **FAULT**, white **OFF**. FAULT flashing + OFF extinguished = ADIRU failure with attitude function still possible.
- ADR1/ADR2/ADR3 P/BSW: amber **FAULT**, white **OFF** (same philosophy).
- PROBE/WINDOW HEAT P/BSW: **ON** legend; AUTO position marked on the panel. A caution graphic in the notes reads "AUTO ACTIVATION OF PROBES HEATING".

**ECAM / EWD**
- ADR 1 part failure: "An ECAM message and a related check list appear on the EWD."
- IR 1 part failure: "An ECAM message and related check list appear on the EWD."
- ADIRU 1 failure with attitude kept: ECAM message and check list on the EWD.
- Any 1311VU selector not in NORM: "will trigger a message on the ECAM (EWD/PFD memo part)."
- ISIS sends status and warning data via IOM to the FWS application hosted in the CPIOM-C.

**PFD (from ADIRS)** — ADR: CAS, mach number, ALTitude, Vertical Speed (V/S shown as a trapezoidal grey background surface, a fixed white scale for the mach number, a needle giving the analog V/S value, and a number in a moving amber window). IR: attitude, pitch angle, roll angle, heading. Warning flags: SPD, ALT, V/S (ADR); ATT, HDG (IR). LS glide-slope and localizer deviation scales when LS PBSW selected ON.

**ND (from ADIRS)** — "Only IR parameters are displayed on the ND. Those parameters are the ground speed and the heading information." (The Indicating diagram additionally labels True Air Speed as ADR part and wind data on the ND.) HDG warning flags shown during alignment.

**MFD POSITION/IRS page** — "IRS ALIGNED ON GPS POS", ALIGN ON OTHER REF, per-IRS status (ALIGN / NAV / ATT), DRIFT AT <airport>, GND SPD, SET HDG, IRS1/IRS2/IRS3 tabs, FREEZE ALL IRS, POSITION, T.TRK, T.HDG, GND SPD, MAG HDG, T.WIND, MAG VAR, GPIRS POSITION, ACCURACY, RETURN, MSG LIST. Example messages seen on the page: "IRS 1 ALIGN / EXCESS MOTION / AVAIL IN 10 MIN", "IRS 2 ALIGN / AVAIL IN 3 MIN", "IRS 3 ATT / ENTER HEADING".

**ISIS display content**
- Standby **navigation** display mode: the rose, the heading indication, the ground speed, the position, the active waypoint and waypoint list.
- Standby **flight** display mode: attitude indications (aircraft symbol, pitch, roll, lateral acceleration), airspeed indication (airspeed, mach number), altitude indication (altitude in feet and meters, barometric pressure), bugs (airspeed, altitude), landing system indication (glide slope, localizer, station source information), heading and track indication, position (latitude and longitude), the fix.
- ISIS also shows ADIRS/MMR-sourced parameters: PPOS, Ground/Speed, heading, track, LS information.
- ISIS carries ADR and IR warning flags (SPD, ALT, V/S; ATT, HDG) as listed in the ADIRU 1 failure procedure.
- ISIS MENU → MAINTENANCE → MAINTENANCE PAGES / AIR DATA TESTING (accessed by the SET/SEL knob).

**Maintenance / BITE**
- ADR BITE and IR BITE modules communicate with the OMS. ISIS gives maintenance data to the OMS through the SCI.
- OMS interactive tests (launched from the OMS HMI using the OMT, OIT or PMAT), selecting ATA 34 – Navigation then the BITE (ADR or IR) then the side (ADR 1/2/3 or IR 1/2/3):
  - **ADR tests:** Output test, System test, Equipment test (test-selection screen also offers Slew test; the ADR menu shows Tests…, Reports…, Ram air turbine tests…).
  - **IR tests:** System test, Interface test (the IR menu shows Tests…, Reports…, Specific data…).
- ISIS air data and inertial data are also sent to the CDAM; ADIRS status goes to the CDAM.
- Standby magnetic compass has a **compensation card**.

---

## 0.7 NUMBERS — the whitelist of "specified" values

**Quantities / architecture**
| Value | Meaning | Source |
|---|---|---|
| 3 | ADIRUs (channels) | L1 p4, L2/3 p2, p6 |
| 2 | main parts per ADIRU (ADR and IR) | L1 p4, L2/3 p6 |
| 3 | MultiFunction Probes (MFPs); 1 on LH side, 2 on RH side; 1 per ADIRU | L2/3 p8 |
| 6 | Integrated Static Probes (ISPs); 3 RH, 3 LH; **2 per ADIRU** | L2/3 p8 (L2/3 p2 states "2 ISPs" per channel) |
| 3 | Side Slip Angle (SSA) probes; 1 per ADIRU | L2/3 p8 |
| 2 | Outside Air Temperature (OAT) probes, on the NLG (LH → ADIRU 1; RH → ADIRUs 2 and 3) | L2/3 p8 |
| 4 | types of sensor connected to the ADR part (MFP, ISP, SSA, OAT) | L2/3 p8 |
| 3 | types of sensor (L1 wording: MFP, 2 ISPs, SSA) | L1 p6 |
| 1 | ADIRS control panel (ICP) common to the 3 ADIRUs | L1 p4, L2/3 p2 |
| 1 | SWITCHING panel | L2/3 p2 |
| 2 | ISIS units | L1 p10, L2/3 p2, p28 |
| 1 | standby pitot probe (LH FWD fuselage) | L1 p10, L2/3 p28 |
| 2 | standby static probes (LH and RH FWD fuselage, nose front fairing) | L1 p10, L2/3 p28 |
| 1 | standby magnetic compass (top of windshield centre post) | L1 p10, L2/3 p28 |
| 2 | EFIS Control Panels | L1 p4, L2/3 p6 |
| 2 | Keyboard Cursor and Control Units (KCCUs) | L1 p4, L2/3 p6 |
| 3 | IR momentary-action PBSWs (IR 1, IR 2, IR 3) | L2/3 p20 |
| 3 | ADR momentary-action PBSWs (ADR 1, ADR 2, ADR 3) | L2/3 p20 |
| 3 | selector switches with three positions (OFF, NAV, ATT) | L2/3 p20 |
| 1 | PROBE/WINDOW/HEAT PBSW | L2/3 p20 |
| 2 | rotary selectors on the switching panel (ATT HDG, AIR DATA) | L2/3 p16, p20 |
| 3 | positions per switching selector (CAPT ON 3, NORM, F/O ON 3) | L2/3 p20 |
| 5 | P/BSWs on the ISIS front face (+ 1 rotary knob P/B + 1 light sensor) | L2/3 p34 |
| 3 | accelerometers (one per axis) | L2/3 p12 |
| 3 | gyros (one per rotation axis) | L2/3 p12 |
| 2 | ARINC 429 outputs from the ISIS | L2/3 p30 |
| 3 | PRIM systems, each containing 2 FCGUs | L2/3 p30 |
| 1 | MMR (MMR 1) interfaced with each ISIS | L2/3 p30 |
| 2 | MMRs shown feeding the IR part (MMR 1, MMR 2) | L2/3 p13 diagram |
| 12 o'clock | standard ("NORM") position of the switching selectors | L2/3 p16 |

**Panel / equipment identifiers**
| Identifier | Item | Source |
|---|---|---|
| **1221VM** | ADIRS control panel (ICP); ICP02A is part of it | L1 p5, L2/3 p2, p14 |
| **1311VU** | SWITCHING panel; also the identifier used for the ISIS units | L2/3 p2, p16; L1 p11 / L2/3 p29 (ISIS captions) |
| ICP02A | ADIRS Integrated Control Panel designation | L2/3 p14 |
| ARINC 429 | probe→ADIRU, ADIRU→ISIS and back-up data bus standard | L2/3 p8, p12, p30 |

**Electrical**
| Value | Meaning | Source |
|---|---|---|
| 115 VAC | Normal ADIRU supply; probe digital-converter and anti-icing supply | L2/3 p2, p8 |
| 28 VDC | ADIRU back-up generation; ISP digital-converter supply | L2/3 p2, p8 |
| 28 VDC BACK-UP **(10 sec)** | Hot-bus back-up duration quoted in the ADIRUs POWER SUPPLY table | L2/3 p17 |
| ADIRU 1 | 115 VAC = AC EMER BUS; 28 VDC PRIMARY = DC ESS BUS; 28 VDC BACK-UP = HOT BUS 1 | L2/3 p3, p17 |
| ADIRU 2 | 115 VAC = AC BUS 4; 28 VDC PRIMARY = DC BUS 2; 28 VDC BACK-UP = NOT POWERED | L2/3 p3, p17 |
| ADIRU 3 | 115 VAC = AC BUS 1 / AC EMER BUS; 28 VDC PRIMARY = DC ESS BUS; 28 VDC BACK-UP = HOT BUS ESS | L2/3 p3, p17 |
| MFP | AC: system 1 = EMER BUS, system 2 = BUS 4, system 3 = BUS 2 | L2/3 p10 |
| SSA | AC: system 1 = ESS BUS, system 2 = BUS 4, system 3 = BUS 2 | L2/3 p10 |
| ISP | AC: system 1 = ESS BUS, system 2 = BUS 4, system 3 = BUS 2; DC: system 1 = ESS BUS, system 2 = BUS 2, system 3 = BUS 1 | L2/3 p10 |
| ISIS 1 | 28 VDC BUS 1 / ESS BUS | L2/3 p32 |
| ISIS 2 | 28 VDC BUS 2 / ESS BUS | L2/3 p32 |
| Standby pitot | 115 VAC ESS BUS | L2/3 p30, p32 |
| Standby static L and R | 115 VAC BUS 2 | L2/3 p32 |

**Timings and thresholds**
| Value | Meaning | Source |
|---|---|---|
| **5 to 17 minutes** | duration of IR alignment ("depends on the aircraft position") | L2/3 p4 |
| **ten seconds (10 s)** | after ALIGN IRS, ALIGN replaces INVALID; also: SPD/ALT/V/S warning flags not shown after ten seconds in the powering procedure | L2/3 p24, p22 |
| **AVAIL IN 7 MIN** | indication that appears after the manual align command | L2/3 p24 |
| **thirty seconds (30 s)** | ATT warning flag not shown after thirty seconds (powering procedure) | L2/3 p22 |
| **GS > 30 kts** | automatic probe anti-icing activation threshold (IR ground speed) | L2/3 p9, p30 |
| **CAS > 50 kts** | ISIS-generated anti-icing activation condition | L2/3 p30 |
| 10 sec | ADIRU 28 VDC back-up qualifier (see above) | L2/3 p17 |

**Screen example values (MFD POSITION/IRS page) — the notes label these "PARAMETERS SHOWN AS EXAMPLES (NOT CONSISTENT)"; usable only as illustrative screen text, not as system specification**
39°08.2N/076°50.2W (IRS aligned on GPS pos); DRIFT AT LFBO33L 1.0 NM/M for IRS 1/2/3; GND SPD 12 KT; SET HDG 350.0 °T; POSITION 39°08.5N/076°50.9W; T.TRK 359.8 °T; T.HDG 359.8 °T (359.8/351.3 °T on the p13 variant); GND SPD 0 KT; MAG HDG 350.8 °; T.WIND 000°/000 KT; MAG VAR 1.5 °; GPIRS POSITION 39°08.3N/076°50.9W; ACCURACY 110 M. ISIS example readouts: 29.92 (baro), GPIRS N 46 15.5 / E 003 32.3, GS 370, TO WPT 352°/283 NM. PFD/ND examples: QNH 1016, VOR1 116.00 / 117.70, CRS 010°.

---

## 0.8 GAPS — needed by the simulation, not stated in the notes (each with a conservative, labelled assumption)

| # | Gap | Assumption to use, tagged "(assumed)" in the UI |
|---|---|---|
| G1 | No ADIRU voting/comparison-monitoring logic is described. The notes only mention "discrepancy of parameters shown between CAPT and F/O EFIS Display Units" as a **reason for the crew to use the switching panel**. | Model discrepancy detection as **crew-observed only** — no automatic voting. Do not simulate an automatic "best-2-of-3" selection. (assumed) |
| G2 | ADIRU accuracies (position drift rate, attitude/heading accuracy) are not specified; the only figures are screen examples (DRIFT 1.0 NM/M, ACCURACY 110 M). | Show drift/accuracy only as the MFD screen example values, labelled "(screen example)". Never present them as a specification. (assumed) |
| G3 | Alignment progress law between 5 and 17 minutes is not stated. | Use a linear countdown with a default of **10 minutes**, tagged "(assumed)", with the 5–17 min range shown as the specified envelope. (assumed) |
| G4 | The "10 sec" against the 28 VDC BACK-UP column is not explained (duration of hold-up vs transfer time). | Interpret as the **hold-up duration of the hot-bus back-up**, tagged "(assumed — notes give only '10 sec')". (assumed) |
| G5 | ATT mode entry conditions are described qualitatively ("partial failure, mainly at the accelerometers level"). No thresholds. | Make ATT a **manual selection only** in the sim; never auto-enter ATT. (assumed) |
| G6 | Exact ECAM message texts are not quoted anywhere in these notes. | Display generic paraphrases such as "NAV ADR 1 FAULT — see EWD check list" with a "(text paraphrased — not quoted from the manual)" tag. (assumed) |
| G7 | Which specific probe feeds which ADIRU is stated only by count for ISPs (2 each) and by pairing for MFP/SSA. Diagram labels ISP 1-1/1-2 etc. | Adopt the diagram convention: ISP n-1 (LH) and ISP n-2 (RH) → ADIRU n. (assumed from the L2/3 p3 and p10 diagrams) |
| G8 | Behaviour when the ATT HDG and AIR DATA selectors are set to **different** non-normal positions (e.g. ATT HDG CAPT ON 3 while AIR DATA F/O ON 3) is not described, and ADIRU 3 cannot serve both sides. | Allow the selection, show both an ECAM memo and a "(assumed) ADIRU 3 cannot feed both sides — last-selected side served, other side reverts to its own ADIRU" caution. Flag it explicitly as a gap in the debrief. (assumed) |
| G9 | Response time / refresh rate of ADR and IR data on the ADCN is not given. | Animate at a fixed illustrative rate; display no numeric latency. (assumed) |
| G10 | ISIS internal sensor accuracy and the standby-compass compensation values are not given. | Omit; show only the parameter names. (assumed) |
| G11 | The consequence of a **total ADIRU 3 loss** on the switching panel (CAPT ON 3 selected with ADIRU 3 dead) is not stated. | Model as: no data reaches the selected side; the affected PFD/ND shows the ADR/IR warning flags. Tag "(assumed)". |
| G12 | Whether the ADR and IR P/BSW OFF selection also removes power from the ADIRU is not stated (the rotary selector is the power control). | Model P/BSW OFF as **bus/output inhibit only**; power remains from the rotary selector. (assumed, consistent with L2/3 p15 signal names "IR BUS OFF" / "ADR BUS OFF") |
| G13 | ISIS battery/independent supply time is not stated (only "normal DC buses" and "DC essential bus"). | Do not model any ISIS internal battery. (assumed) |

---

## 0.9 LEARNING OUTCOMES (CAAS SAR-66 Cat B2, Level 2)

On completion of this simulation the student can:

1. **Identify** the three ADIRS channels, each channel's ADR and IR parts, and every ADIRS probe (MFP, ISP, SSA, OAT) and standby sensor (standby pitot, 2 standby statics, standby compass) with its correct quantity, location and channel allocation.
2. **Trace** the supply path of any displayed air-data or inertial parameter from its probe, through the ADR/IR part of the correct ADIRU, over the ADCN (or the ARINC 429 back-up), to the CAPT PFD/ND, F/O PFD/ND or ISIS.
3. **Operate** the ADIRS ICP (1221VM) and the SWITCHING panel (1311VU) — selector OFF/NAV/ATT, IR and ADR P/BSWs, PROBE/WINDOW HEAT, ATT HDG and AIR DATA selectors — and state what each position commands.
4. **Predict** the display, legend and ECAM consequences of an ADR 1, IR 1 or complete ADIRU failure, and of each 1311VU switching selection, before making the selection.
5. **Explain** the ADIRU power architecture — 115 VAC primary per the power-supply table, automatic transfer to 28 VDC when 115 VAC exceeds its normal limits, and which channels survive loss of main AC generation.
6. **Isolate** a failed ADIRS channel using the FAULT/OFF legends, the PFD/ND/ISIS warning flags, the MFD POSITION/IRS page and the OMS interactive ADR and IR tests, then **verify** the reconfiguration and state the ISIS back-up configuration that results.

---

## 0.10 MISCONCEPTIONS the simulation must expose

| # | Misconception | How the sim should make it fail visibly |
|---|---|---|
| M1 | "ADIRU 3 is a spare that automatically takes over when 1 or 2 fails." | It does not. Failing ADIRU 1 leaves the CAPT PFD/ND flagged until the student **manually** moves the 1311VU selector. The notes: "may be **manually** selected". |
| M2 | "The ATT HDG and AIR DATA selectors are one switch." | They are two independent rotaries acting on different parts. Move only ATT HDG after an ADR 1 failure and the SPD/ALT/V/S flags stay on the CAPT PFD. |
| M3 | "Pushing the ADR/IR P/BSW to OFF fixes the failure / removes power from the ADIRU." | The P/BSW only inhibits the output buses and lights the OFF legend; the ADIRU stays powered by the rotary selector. The correct order is: switch first, then push the P/BSW. |
| M4 | "ATT mode is a degraded NAV mode that still gives position." | In ATT the ADIRU "only gives heading and attitude data"; no position, and the heading has to be entered through the MFD. The sim should leave the ND position blank until SET HDG is entered. |
| M5 | "ISIS reads the ADIRS, so if the ADIRS is lost the ISIS is lost." | ISIS computes its own air data (internal pressure sensors) and attitude (internal gyrometers/accelerometers) from the standby pitot/static probes; it only *supplements* with ADIRU 1/3 and MMR 1 data. Kill all three ADIRUs and the ISIS stays alive. |
| M6 | "All three ADIRUs are on the same electrical supply / all survive an electrical emergency." | ADIRU 2 sits on AC BUS 4 with **no 28 VDC back-up**; ADIRU 1 and 3 sit on the AC EMER BUS with HOT BUS 1 / HOT BUS ESS back-up. Loss of main AC generation kills channel 2. |

---

## 0.11 DEFINITIONS & PRECEDENCE

**Operative terms, in the notes' sense**

| Term | Definition as used in these notes |
|---|---|
| **ADIRS** | "The A/C navigation center… an autonomous system, independent of ground navigation aids", giving air data, inertial parameters and time reference to many A/C systems and to the CDS. |
| **Air Data Reference (ADR)** | The ADIRU part that "receives the aerodynamic signals from various sensors and computes air data parameters" (CAS, mach, ALT, V/S, TAS, TAT, AOA, SSA). |
| **Inertial Reference (IR)** | The ADIRU part that "receives the GPS signal from Multi Mode Receivers (MMRs) and computes the inertial parameters and the navigation parameters" from three accelerometers and three gyros (attitude, position, velocities, acceleration, rotation rate). |
| **Channel** | One complete ADIRS lane: one ADIRU (ADR + IR) plus its dedicated MFP, 2 ISPs, SSA and OAT input — "The ADIRS is based on three independent and redundant channels." |
| **Alignment** | The IR initialisation period at the end of which "the Inertial Reference System (IRS) is automatically initialized on the GPS position"; duration 5 to 17 minutes; status shown as ALIGN → NAV on the MFD POSITION/IRS page. |
| **NAV mode** | Selector position that is "the normal position to energize and use the related ADIRU"; full air data + inertial + navigation output. |
| **ATT mode** | Selector position selected "in case of partial failure (mainly at the accelerometers level)"; "the ADIRU only gives heading and attitude data if the system loses its ability to navigate. The heading has to be entered through the MFD." |
| **Standby (of a channel)** | ADIRU 3's normal state: "ADIRU 3 is mainly in standby" / "in standby for EFIS display function" — powered and aligned, but not routed to a PFD/ND until the 1311VU selects it. |
| **Standby (of the SNS/ISIS)** | Different sense: the autonomous instrument system that computes its own air data and attitude from its own probes and internal sensors — "standby flight display" and "standby navigation display" modes. |
| **Back-up** | Two distinct senses: (a) **electrical** — the 28 VDC supply the ADIRU transfers to when 115 VAC exceeds its normal limits; (b) **data path** — "ARINC 429" as the back-up to the AFDX/ADCN primary path; and (c) **system** — the SNS/ISIS as "the back-up system in case of ADIRS failure or CDS failure". Label which sense is meant wherever the word appears in the UI. |
| **Switching** | The manual reconfiguration performed on panel 1311VU, "used in case of failure of the IR or the AIR DATA part of the ADIRU1 or ADIRU2, or in case of discrepancy of parameters shown between CAPT and F/O EFIS Display Units". "The Switching will also have consequences on ADIRUs power supply." |
| **NORM / CAPT ON 3 / F/O ON 3** | The three positions of each 1311VU rotary; NORM is 12 o'clock. Any other position triggers an ECAM memo. |
| **FAULT legend** | Amber legend on an IR or ADR P/BSW indicating failure of that part. Flashing FAULT with OFF extinguished = ADIRU failure with attitude function still possible. |
| **OFF legend** | White legend indicating the output buses of that part are disabled — commanded by a discrete "IR OFF"/"ADR OFF" signal from the part itself after the P/BSW is depressed. |
| **Automatic reconfiguration (ISIS)** | The ISIS-to-ISIS discrete-link function by which ISIS 2 takes the standby flight display if ISIS 1 fails; reversible on the MODE P/BSW. |
| **BITE** | The module hosted in each ADR and IR part for communication with the OMS; also the ISIS maintenance path via the SCI. |
| **Interchangeable (ISIS)** | "The ISIS units are interchangeable" — either unit can perform either display function; the difference in normal configuration is by position/wiring, not by part number. |

### Conflicts between the two note sets and precedence taken

| # | Conflict | Preference and reason |
|---|---|---|
| C1 | **Number of sensor types feeding the ADR.** L1 p6: "The ADR part of each ADIRU receives air data from **3 types** of sensors" (MFP, 2 ISPs, SSA). L2/3 p8: "The ADR part of each ADIRU is connected to **four types** of sensors: 1 MFP, 2 ISPs, 1 SSA probe, 1 OAT probe." | **Take L2/3** (four types, OAT included). L2/3 is the more detailed and more recent set (Nov 2011 vs Apr 2007) and describes the OAT probes, their NLG location and their ADIRU allocation explicitly. Record L1's omission as a Level-I simplification, not a contradiction. |
| C2 | **Number of ISPs.** L1 p6 speaks of "two Integrated Static Probes (ISPs)… (one on each side)" per ADIRU; L2/3 p8 gives the fleet total: "There are six ISPs. Each ADIRU is connected to two ISPs." | No real conflict — L1 gives the per-channel count, L2/3 the total. **Model 6 ISPs total, 2 per ADIRU.** |
| C3 | **Switching-panel identifier.** L2/3 p4 text prints "SWITCHING control panel (1311 VU)" with a space; the diagrams and L2/3 p2 print "1311VU"; the task brief and some captions use "1311VU" for both the switching panel and the two ISIS. | **Use "1311VU"** for the switching panel; note in the UI that the ISIS captions also carry the 1311VU panel reference (both live on the main instrument panel front panel). |
| C4 | **ISIS anti-icing conditions.** L1 p10 says only "Sensors have anti-icing capabilities automatically or manually activated". L2/3 p30 gives the full logic (engine running, GS > 30 kts, CAS > 50 kts, manual via ICP ADIRS). | **Take L2/3** — more detailed logic set. |
| C5 | **ISIS ADIRU source.** L1 does not state which ADIRU feeds the ISIS. L2/3 p12 says ADIRU 1 and 3 give data to ISIS; L2/3 p30 adds "Basically, the ISIS displays the data coming from ADIRU 3. In case of failure of the ADIRU3, ISIS will switch to ADIRU 1." | **Take L2/3 p30** as the operative rule; ADIRU 3 is the preferred source, ADIRU 1 the fallback. |
| C6 | **ICP designation.** L1 calls it the "Integrated Control Panel (ICP) (1221VM)"; L2/3 p14 calls it "ADIRS ICP02A (part of panel 1221VM)". | **Use both**: display "ADIRS ICP02A — panel 1221VM". The L2/3 wording is the more precise (the ICP is a section of the larger overhead panel). |
| C7 | **General rating precedence rule.** Where a rating or bus allocation appears in both sets, **L2/3 wins** (higher level, more recent, and carries the POWER SUPPLIES and ADIRUs POWER SUPPLY tables); where the *logic or procedure* is described in both, **L2/3 wins** as the more detailed set. L1 is retained only for Level-I framing text (system purpose, "ADIRU 3 is mainly in standby", the seven navigation sub-systems list). | — |

---

### Split assessment (Phase 0 threshold)

Counting SOURCES + BUSES + CONVERSION/COMPUTING UNITS in scope: 3 ADIRUs + 2 ISIS + 1 standby compass (source) = 6 computing/display units; probes are sensors, not counted; the ADCN and ARINC 429 are the two networks. This is **well under the ~14 threshold** and covers **two closely-coupled subsystems** (ADIRS and SNS/ISIS, where the SNS is the declared back-up to the ADIRS). **No split is required — build as one page.**

---

# PART B — DESIGN BRIEF

**File produced:** `aerosim_ata34_adirs_standby_nav.html`

## Archetype: SYSTEM

Three redundant channels feeding two cockpit sides through a two-selector switching panel is a source-allocation graph, not a circuit. The engine is a directed solver — power, then per-part health, then allocation through the 1311VU truth table, then the resulting flags. A CIRCUIT zoom would add nothing the notes support, so pure SYSTEM is chosen. A second view carries the power architecture, because the reason ADIRU 2 dies in an electrical emergency and ADIRUs 1 and 3 do not is the single most examinable fact in the topic and it is invisible on a data-flow diagram.

## Page map

| Mode | What this topic gets |
|---|---|
| **Explore** | Two switchable SVG views. *Architecture* draws all three channels with their four probe types, both sub-parts of each ADIRU, the ADCN with its ARINC 429 back-up, the 1311VU routing, the two cockpit sides with live warning flags, and the entirely separate ISIS chain with its own pneumatic probes and the standby compass. *Power supply* lays out the three channels against their 115 VAC, 28 VDC and hot-bus sources. The right rail is a working ICP 1221VM — three OFF/NAV/ATT selectors, three IR and three ADR pushbuttons with real FAULT and OFF legends, and the PROBE/WINDOW HEAT pushbutton — plus the two switching rotaries with the truth table live-highlighted. 12-step build-up stepper. |
| **Build** | Constructor for one ADIRS channel: 14 palette blocks, orthogonal wiring, undo/redo, JSON export/import, a path continuity tester, three starter architectures and **eight** check-my-build targets covering the normal path, the ARINC 429 back-up, the standby chain and the BITE path. |
| **Fault Lab** | 11 cases, deliberately mixing real defects with correct-but-surprising behaviour (an incomplete alignment, an inactive probe heat, a selector combination the notes do not describe). Eight diagnostic tests, the six-step troubleshooting flow, efficiency score, seeded exam mode, debrief naming the misconception. |
| **Learn** | 13 lesson steps with predict-observe-explain, then a 12-question quiz mapped to LO1–LO6. |

## Scenarios

All three selectors OFF · alignment in progress · normal three-channel · ADR 1 failed before the switch · ADR 1 failed with AIR DATA CAPT ON 3 · IR 1 failed with ATT HDG CAPT ON 3 · ADIRU 2 failed with F/O ON 3 · partial failure in ATT mode · loss of main AC generation · all three ADIRUs lost · ISIS 1 failed · ADIRU 3 failed · free play.

## Outcome mapping

| Lesson steps | Quiz questions | Outcome |
|---|---|---|
| 1, 2, 3 | 1, 2, 3 | LO1 identify the channels, parts and probes |
| 10 | 10 | LO2 trace a parameter from probe to display |
| 5, 6, 11 | 5, 11 | LO3 operate the two panels |
| 4, 7, 8 | 4, 6, 7, 8 | LO4 predict the consequences of a failure and a selection |
| 9 | 9 | LO5 explain the power architecture |
| 12, 13 | 12 | LO6 isolate a channel and state the ISIS back-up |

## Misconceptions the design forces into the open

M1 by leaving the Captain's flags on until the crew moves a selector (step 4, Q4); M2 by making the ATT HDG selector visibly fail to clear an air-data flag (step 5, Q5); M3 by lighting the OFF legend while the flags stay on (step 7, Q6, fault f11); M4 by removing the position in ATT mode (step 8, Q8); M5 by keeping the ISIS alive with all three ADIRUs dead (step 12, Q12, fault f7); M6 by killing only channel 2 in the electrical emergency (step 9, Q9, fault f4).
