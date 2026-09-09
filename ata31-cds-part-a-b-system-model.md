# A380 ATA 31 — Control & Display System (CDS)
## Phase 0 System Model — extraction for AeroSim simulator build

**Source note sets**

| Ref | Document | Level | Pages used (document page numbering) | Date on pages |
|---|---|---|---|---|
| **N1** | `ATA_31_Ind._Recording_Syst.pdf` — "CONTROL & DISPLAY SYSTEM PRESENTATION (1)" | LEVEL I, Maintenance Course T1+T2 (RR/Metric) | pp. 4–21 (PDF pp. 8–25) | Apr 19, 2007 |
| **N2** | `ATA_31_Indicating_Recording_Systems.pdf` — "COCKPIT CONTROL PANELS DESCRIPTION (3)" | LVL 2&3, Mechanical & Avionics Course T1+T2 (RR Trent 900) | pp. 2–7 (PDF pp. 4–9) | Nov 21, 2011 |
| **N3** | same file — "CONTROL & DISPLAY SYSTEM DESCRIPTION (2)" | LVL 2&3 | pp. 8–19 (PDF pp. 10–21) | Nov 21, 2011 |
| **N4** | same file — "CONTROL & DISPLAY SYSTEM DESCRIPTION (3)" | LVL 2&3 | pp. 20–43 (PDF pp. 22–45) | Nov 21, 2011 |
| **N5** | same file — "ELECTRICAL CLOCK SYSTEM DESCRIPTION (3)" | LVL 2&3 | pp. 44–45 (PDF pp. 46–47) | Nov 21, 2011 |

Everything below is traceable to those pages. Items the notes do **not** state are collected in **0.8** and tagged **(assumed)**; they must be labelled as such anywhere they appear on screen.

---

## 0.1 COMPONENTS

### A. Display units and cockpit positions

| id | Full name (as the notes expand it) | Acronym | Type | Ratings / specs quoted from the notes | Location per the notes |
|---|---|---|---|---|---|
| `DU` | Display Unit (LCD smart DU / Liquid Crystal Display Unit) | DU, LCDU | display unit | "eight identical and interchangeable Display Units (DUs)"; "enlarged (8 inch by 6 inch) Smart Liquid Crystal Display Units" (N1 p.4); "a 6.17 in x 8.22 in usable display area", "a video capability through optic fibers", "display capabilities through AFDX" (N4 p.24). CRTs "have been replaced by eight identical and interchangeable" LCDUs. All eight are identical in hardware **and** software design and capabilities; function set by **pin programming** according to DU location (N4 p.24) | Main instrument panel and pedestal |
| `L1` | Left outer DU — CAPT PFD in normal configuration | — | display unit | one of the eight identical DUs | Main Instrument Panel (N2 p.3) |
| `L2` | Left inner DU — CAPT ND in normal configuration | — | display unit | idem | Main Instrument Panel |
| `C1` | Centre upper DU — EWD in normal configuration ("upper ECAM DU") | — | display unit | idem | Main Instrument Panel |
| `C2` | Centre lower DU — SD in normal configuration ("lower ECAM DU") | — | display unit | idem | Pedestal (N2 p.3) |
| `L3` | Left lower DU — CAPT MFD in normal configuration | — | display unit | idem | Pedestal |
| `R3` | Right lower DU — F/O MFD in normal configuration | — | display unit | idem | Pedestal |
| `R2` | Right inner DU — F/O ND in normal configuration | — | display unit | idem | Main Instrument Panel |
| `R1` | Right outer DU — F/O PFD in normal configuration | — | display unit | idem | Main Instrument Panel |

Display formats hosted by the eight DUs (N1 p.4, N3 p.8): 2 Primary Flight Displays (PFDs), 2 Navigation Displays (NDs), 1 Engine Warning Display / Engine-Warning Display (EWD — N3 p.8 writes "Engine/Warning Display"), 1 System Display (SD), 2 MultiFunction Displays (MFDs).

### B. Control panels

| id | Full name | Acronym / panel no. | Type | Specs quoted | Location |
|---|---|---|---|---|---|
| `ECP` | ECAM Control Panel — an Integrated Control Panel (ICP) | **ECP**, ICP **1135VM** (N1 p.11 figure, N2 p.4). *N4 p.43 figure labels the same panel* **1135VU** *— see 0.11 conflict* | control panel | "The ECP is an Integrated Control Panel (ICP) and is used to control the EWD and the SD DUs. It is the main interface between the flight crew and the ECAM" (N4 p.38). Connected via CAN bus to **IOMs 7 and 8** (N4 p.38). Two segregated ECP CAN channels: **CAN ECP1 (side 1)**, **CAN ECP2 (side 2)** (N2 p.6) | Pedestal (N2 p.4, p.5 figure) |
| `CDSR-C` | CDS Reconfiguration control panel, Captain | **1313VU** (N1 p.7, N3 p.9, N3 p.11) | control panel | "Each CDS RECONF Control Panel is composed of a: PFD, ND, MFD brightness selector; PFD, ND switching button; reconfiguration button" (N4 p.34) | Captain side, main instrument panel area |
| `CDSR-F` | CDS Reconfiguration control panel, First Officer | **1314VU** (N1 p.7, N3 p.9, N3 p.11, N4 p.33). *N1 p.11 figure labels it* **1314VM** *— see 0.11 conflict* | control panel | idem | F/O side |
| `EFISCP-C` | EFIS Control Panel, Captain | — (no panel number given in the notes) | control panel | "mainly composed of: navigation data display settings buttons; barometer settings which have a barometer reference display window and a barometer reference selector; PFD controls: localizer and glide slope scales and velocity vector; ND controls: ND mode and range selection" (N4 p.34) | Glareshield (N2 p.3 shows glareshield as a VU location; the EFIS CP appears on the glareshield strip in N1 p.7 / N4 p.33 figures) |
| `EFISCP-F` | EFIS Control Panel, First Officer | — | control panel | idem | Glareshield |
| `KCCU-C` | Keyboard and Cursor Control Unit, Captain | **KCCU** (parts: **CCD** Cursor and Control Device / Cursor Control Device, **KBD** KeyBoarD) | interactive device / control panel | "composed of two functionally redundant parts: the CCD, based on trackball technology, and the keyboard. There are two KCCUs, one dedicated to each pilot, installed on the pedestal." Keyboards are **QWERTY** type and multifunction. Although CCD and keyboard are in the same equipment item "they are completely segregated; they have independent CAN bus connections" (N4 pp.20, 30) | Pedestal |
| `KCCU-F` | Keyboard and Cursor Control Unit, First Officer | KCCU | interactive device | idem | Pedestal |
| `ICP-CAN` | Integrated Control Panels with CAN interface ("Digital ICP / ICP CAN") | **1211VM, 1212VM, 1215VM, 1225VM, 1235VM** (five) | control panel | "uses discrete, analog and Controller Area Network (CAN) interfaces"; connected to A/C systems (LRUs and LRMs) through the CAN network and **IOMs 1, 2, 5 and 6**; also connected by discrete and analog signals; data is also exchanged between these ICPs (N2 p.6) | Overhead panel; 1235VM on overhead per N2 p.5 figure |
| `ICP-NOCAN` | Integrated Control Panels without CAN ("ICP no CAN") | **1221VM, 1222VM, 1231VM, 1245VM, 1255VM** (five) | control panel | "only uses discrete and analog interfaces"; connected to A/C systems (LRUs and LRMs) "through analog and discrete signals for the control of critical items like relay, pumps, valves…" (N2 p.6) | Overhead panel (N2 p.4/p.5) |
| `VU` | Conventional control panels | VUs | control panel | "located on the consoles, the main instrument panel, the glareshield and partially on the overhead panel" (N2 p.2) | as stated |
| `CLOCK` | Electrical Clock | — | indicator / data source | Displays CHR (chronometer, MIN/SEC), UTC (HR/MO, MIN/DY, SEC/Y) and ET (elapsed time, HR/MIN); controls RST, CHR, SET/DATE, GPS–INT–SET selector, RUN–STP–RST selector (N5 p.45 figure) | Cockpit (panel number not given) |

### C. Computers, networks and data sources referenced by the CDS

| id | Full name | Acronym | Type | Notes-quoted facts |
|---|---|---|---|---|
| `ADCN` | Avionics Data Communication Network | ADCN | network | Main data path from A/C systems to the DUs. Dialog between DUs is done through **Avionics Full Duplex Switched Ethernet (AFDX)** via the ADCN; "each DU is connected to the ADCN through AFDX cables in order to have the capability to transmit and to share data with all other DUs" (N4 p.20) |
| `CAN` | Controller Area Network buses dedicated to the CDS | CAN | network | "There are two CAN buses by side, and each CAN bus on a dedicated side is redundant for reliability purposes. So each DU has two CAN connections." Buses named **CAN BUS 1.1, CAN BUS 1.2, CAN BUS 2.1, CAN BUS 2.2** (N4 pp.20–21). Used mainly to let the KCCU control the DUs. ICP CAN architecture: two sides × two channels = four segregated channels — **CAN 1.1, CAN 1.2 (side 1); CAN 2.1, CAN 2.2 (side 2)**; each ICP CAN panel potentially connected to all four (N2 p.6). CAN characteristics: "Multi-master priority based"; **125 Kb/s** data transmission rate; norm **CAN 02B**; "The loss of one channel does not cause the complete loss of the CAN bus"; "A failure of the CAN network does not disturb the discrete links functioning" (N2 p.6) |
| `ADIRS` | Air Data Inertial Reference System / Air Data Inertial References | ADIRS, ADIRUs | data source | EFIS **backup** source: "In order to overcome a complete ADCN failure, the LCDUs can also acquire data through a backup connection, directly from the Air Data Inertial References (ADIRS)" (N1 p.6, N3 p.8). Backup connections carry **ADIRS data in ARINC 429** (N4 p.32). Three ADIRUs output GPS time/date continuously and back up the clock (N5 p.44) |
| `FWS` | Flight Warning System | FWS | computer/LRU | Drives the EWD Warning Display zone and the SD Status page; computes the current flight phase used by ECAM Normal mode. ECAM **backup**: "In order to overcome a complete ADCN failure, the LCDUs can also acquire data through a backup connection, directly from FWS" (N1 p.10). FWS data in AFDX with **ARINC 429 backup** (N4 p.36) |
| `CMV` | Concentrator and Multiplexer for Video | CMV | computer/LRU | "The CDS acquires parameters from them through the ADCN, **except for the Concentrator and Multiplexer for Video (CMV), which is directly connected**" (N1 p.16). Video data reaches the DUs "by optic fibers" (N4 p.32) |
| `FMS` | Flight Management System | FMS | remote user application | MFD application; page menu "FMS managed by the FMS" (N4 p.16) |
| `AESS` | Aircraft Environment Surveillance System | AESS | remote user application | MFD application; MFD menu "SURV managed by the Aircraft Environment Surveillance System" (N4 p.16) |
| `ATCS` | Air Traffic Control System / ATC Communication | ATCS, ATC-COM | remote user application | MFD application; MFD menu "ATC COM managed by the ATC system"; also drives the SD **ATC Mail Box** |
| `FCUB` | Flight Control Unit Backup | FCU Backup / FCU BKUP | remote user application | MFD application; menu "FCU BKUP managed by the FCU Backup application" |
| `OANS` | On-board Airport Navigation System (Airport Navigation function) | OANS | remote user application | "the CDS and in particular the KCCUs are linked to the OANS by **RS 422**, in order to manage the display of Airport Navigation screen" (N4 p.22). OANS appears as a selectable format in the DU reconfiguration lists (N3 p.11 figure) |
| `ETACS` | (format appearing in the L1/R1 reconfiguration lists) | ETACS | display format | Listed as a reconfigurable format available on L1 and R1 only (N3 p.11 figure). *The notes do not expand this acronym — see 0.8* |
| `CMS` | Central Maintenance System | CMS | computer/LRU | Receives CDS BITE fault messages "for failure isolation, failure memorization and reports generation"; "The CMS can launch CDS interactive tests from the maintenance terminals" (N4 p.22). DU cross-monitoring sends an alarm to FWS and CMS "that respectively generate a warning and a fault message" (N4 p.28) |
| `DLCS` | Data Loading and Configuration System | DLCS | computer/LRU | Receives CDS configuration "for configuration monitoring and management"; "The DLCS loads the DUs applications, definition files and also DUs pin-programming configuration" (N4 p.22) |
| `OMS` | Onboard Maintenance System | OMS | computer/LRU | Destination of CDS BITE/configuration data (N4 p.22 and p.23 figure, which shows CDAM and SCIs between ADCN and OMS) |
| `IOM` | Input/Output Module (IOM-A) | IOM | computer/LRU | ICPs CAN connect through **IOMs 1, 2, 5 and 6**; ECP connects through **IOMs 7 and 8** (N2 p.6, N4 p.38). Clock connects through **IOM-A 5/6** (N5 p.45 figure) |
| `CPIOM-B3/B4` | Core Processing Input/Output Module B3 and B4, hosting the AVS application | CPIOM-B3, CPIOM-B4; **AVS** = Avionics Ventilation System | computer/LRU | "The avionics air cooling system has two Avionics Ventilation System (AVS) Applications hosted in Core Processing Input/Output Modules (CPIOM) -B3 and B4, which regulate the blowing system." Loss-of-cooling information is provided to the CDS "through AFDX bus by the AVS Application in CPIOM-B3/4" (N4 p.26) |
| `MMR1/MMR2` | Multi-Mode Receiver 1 / 2 (GPS1 / GPS2) — external time reference | MMR (GPS1/GPS2) | data source | "In normal configuration (external mode) the MMR1 (GPS1) sends time reference to the electrical clock then the clock transmits time and date to the clock users through ADCN" (N5 p.44) |
| `CDAM` / `SCIs` | Centralized Data Acquisition Module / System Configuration Items (as drawn) | — | computer/LRU | Shown between ADCN and OMS on the CDS-interfaces figure (N4 p.23); no descriptive text in the notes |

### D. Software / data files inside each DU (N4 p.24)

- system software for system management: configuration management, **BITEs**, resource allocation, crew control input management
- **EFIS/ECAM functions applications** providing all display functions under the CDS responsibility
- **A380 objects library** — "a set of widgets (graphical interactive or not objects)"
- one **CDS Definition File (DF)** for EFIS/ECAM functions display definition (CDS responsibility). "A Definition File is a set of data, which specifies to the CDS the graphics/widgets to be displayed on the DUs"
- all definition files outside CDS responsibility for remote user applications: **FWS DF, FMS DF, FCU BACKUP DF, AESS DF, ATC DF, CMV DF** — "located in the DUs but do not belong to the CDS… part of the remote user applications"
- EFIS/ECAM function blocks named in the DU-software figure (N4 p.25): PFD, Slat/Flap/Trim, ND, Vertical Display, Engine Display, SD, Permanent Data, MFD General Menu

---

## 0.2 TOPOLOGY

Format: **from → via → to**. Backup paths are called out explicitly.

### Normal (ADCN) data paths
| # | Path | Source |
|---|---|---|
| T1 | A/C systems → ADCN (AFDX) → EFIS DUs (PFD/ND) | N1 p.6, N3 p.8 |
| T2 | A/C systems → ADCN (AFDX) → ECAM DUs (EWD/SD) | N1 p.10, N3 p.8 |
| T3 | FWS → ADCN → ECAM DUs (EWD Warning Display zone, SD Status page) | N1 p.10, N4 p.36 |
| T4 | ADIRS → ADCN → EFIS DUs | N4 p.33 figure |
| T5 | ECP (1135VM) → CAN (ECP CAN network) → IOM-A 7/8 → ADCN → ECAM DUs & FWS | N4 p.38, N2 p.7 figure |
| T6 | ICPs CAN (1211/1212/1215/1225/1235VM) → ICP CAN network → IOM-A 1/2/5/6 → ADCN → A/C systems (LRUs, LRMs) | N2 pp.6–7 |
| T7 | ICPs (CAN and no-CAN) → discrete / analog signals → A/C systems (LRUs, LRMs) | N2 p.6 |
| T8 | DU ↔ ADCN (AFDX) ↔ every other DU (DU-to-DU dialog) | N4 p.20 |
| T9 | KCCU → CAN BUS 1.1 / 1.2 (CAPT side) → CAPT DUs; KCCU → CAN BUS 2.1 / 2.2 (F/O side) → F/O DUs | N4 pp.20–21 |
| T10 | All DUs + KCCUs (BITE data) → CAN BUS 1.1 and CAN BUS 2.1 → **EWD** → ADCN → CMS | N4 p.20 |
| T11 | CDS BITE → ADCN → CMS → OMS (fault messages, failure isolation, memorization, reports) | N4 p.22 |
| T12 | CDS configuration → ADCN → DLCS → OMS (configuration monitoring/management); DLCS → DUs (applications, definition files, pin-programming configuration) | N4 p.22 |
| T13 | Remote user applications (FMS, AESS, ATCS/ATC-COM, FCU Backup) → ADCN → MFDs | N1 pp.16–18 |
| T14 | EFIS control panel → onside PFD Main Zone and onside ND Main Zone / Vertical Display | N1 p.20 |
| T15 | CDS RECONF control panel 1313VU / 1314VU → onside DUs (reconfiguration and brightness) | N1 p.7, N4 p.34 |
| T16 | MMR1 (GPS1) → Electrical Clock → IOM-A 5/6 → ADCN → clock users (ATC, FMS, CVR, CDS, HSMU, OMS via SCIs) | N5 pp.44–45 |
| T17 | AVS application in CPIOM-B3/B4 ← cooling effect detectors; AVS → AFDX → CDS (loss-of-air-cooling information) | N4 p.26 |

### Direct / non-ADCN paths
| # | Path | Source |
|---|---|---|
| T18 | **CMV → direct connection (optic fibers) → DUs** — video data. "The CDS acquires parameters from them through the ADCN, except for the CMV, which is directly connected" | N1 p.16, N4 p.32 |
| T19 | KCCU ↔ **RS 422** ↔ OANS (Airport Navigation screen management) | N4 p.22 |
| T20 | A/C systems → **discrete** signal transmission → CDS ("data transmission in discrete for particular signal indication") | N4 p.22 |

### BACKUP paths (used to overcome a complete ADCN failure)
| # | Backup path | Source |
|---|---|---|
| B1 | **ADIRS → direct backup connection (ARINC 429) → EFIS LCDUs (PFD/ND)** | N1 p.6, N3 p.8, N4 p.32 |
| B2 | **FWS → direct backup connection (ARINC 429) → ECAM LCDUs (EWD/SD)** | N1 p.10, N3 p.8, N4 p.36 |
| B3 | **Critical systems → ARINC 429 backup → DUs** (for SD system pages) — "some systems also send data to CDS in ARINC 429 in order to overcome a complete loss of ADCN network"; the ECAM figure shows "CRITICAL SYSTEMS → BACKUP → PFD A/C Config zone" | N4 pp.22, 36, 37 |
| B4 | **ECP → direct discrete connection → FWS** for the keys "CLR", "RCL", "STS", "EMER CANC", "VALID" and the SCROLL UP/DOWN device, "to fulfill the main ECP function" in case of ECP failure | N4 p.36, p.38, p.39 figure |
| B5 | **ECP "ALL" key → direct discrete connection → CDS** in case of ECP failure | N4 p.36 |
| B6 | **MMR-GPS lost → ADIRUs internally provide the time reference**; if clock data fails or clock is in "SET" mode, time back-up is provided by the three ADIRUs via ADCN | N5 p.44 |

### Power supply topology (N3 p.9 figure — DU/KCCU power table)
| Equipment | Normal supply | Backup supply |
|---|---|---|
| CAPT PFD | DC ESS BUS | — |
| CAPT ND | DC ESS BUS | DC BUS 1 (BACKUP) |
| CAPT MFD | DC ESS BUS | DC BUS 1 (BACKUP) |
| CAPT KCCU CCD | DC ESS BUS | — |
| CAPT KCCU KBD | DC ESS BUS | DC BUS 1 (BACKUP) |
| EWD | DC ESS BUS | — |
| F/O PFD | DC BUS 2 | — |
| F/O ND | DC BUS 1 | DC BUS 2 (BACKUP) |
| F/O MFD | DC BUS 1 | DC BUS 2 (BACKUP) |
| F/O KCCU CCD | DC BUS 2 | — |
| F/O KCCU KBD | DC BUS 1 | DC BUS 2 (BACKUP) |
| SD | DC BUS 2 | — |

**Note quoted verbatim from that figure:** "ON GND IN BAT CONFIGURATION ONLY EWD AND CAPT MFD ARE SUPPLIED. IN THIS CONFIGURATION, RECONF PUSH BUTTON BECOMES ACTIVE, ALLOWING TO RECOVER SD ON CAPTAIN MFD."

### Cooling topology (N4 pp.26–27)
- Each DU → two rear connections: **one blowing air, one extraction air** → avionics air cooling system (Ventilation System side 1 / side 2).
- **KCCUs are NOT connected to the air cooling system.**
- Cooling effect detectors → AVS in CPIOM-B3/B4 → AFDX → CDS.
- DU nominal temperature shown on the figure: **T DU nominal ≈ 40 °C**.

---

## 0.3 CONTROLS

### EFIS Control Panel (one per pilot) — N4 pp.34–35
| Control | Positions / legends | Commands |
|---|---|---|
| Navigation data display settings buttons | Row of pushbuttons legended **CSTR, WPT, VORD, NDB, ARPT** (upper row) and **WX, TERR, TRAF** with left/right arrow keys (lower row); plus **TAXI** button at left | Selection of navigation data overlaid on the ND |
| **LS** button | LS | PFD control — localizer and glide slope scales |
| **V V** button | V V | PFD control — velocity vector |
| Barometer reference display window | Shows e.g. **QNH 1013**, digital readout **1013** | Displays the barometer reference |
| Barometer reference selector (knob) | **in Hg ↔ hPa** | Barometer setting |
| **ND mode selection** knob | **LS, VOR, NAV, ARC, PLAN** | Selects ND display mode |
| **ND range selection** knob | **ZOOM, 10, 20, 40, 80, 160, 320, 640** | Selects ND display range |

Function per N1 p.20: "Each EFIS control panel controls: the onside PFD Main Zone for short-term guidance; the onside ND Main Zone and Vertical Display for Medium/Long term navigation pages selection and display range."

### CDS Reconfiguration Control Panel — 1313VU (CAPT) / 1314VU (F/O) — N3 p.11, N4 pp.34–35
| Control | Positions / legends | Commands |
|---|---|---|
| **PFD DU** brightness knob | **OFF … BRT** | PFD brightness selection; OFF removes the DU |
| **ND DU** brightness knob | **OFF … BRT** | ND brightness selection |
| **MFD DU** brightness knob | **OFF … BRT** | MFD brightness selection |
| **OIT** brightness knob | **OFF … BRT** | (present on the panel; the notes do not describe its function — see 0.8) |
| **PFD/ND** pushbutton | momentary P/B | Manual PFD/ND transfer: CAPT transfers L1 ↔ L2; F/O transfers R1 ↔ R2 |
| **DU RECONF** pushbutton | momentary P/B | Manual reconfiguration: "At each P/B action the next format in the list is displayed (scrolling list type) with a priority order (internal to the list)". "In case of no DU failure, there is no effect if the RECONF P/B is pressed." |

### ECAM Control Panel (ECP, 1135VM) — N4 pp.38–39 figure
| Group | Keys / legends | Commands |
|---|---|---|
| System page selection (left block) | **ENG, BLEED, PRESS, EL/AC, APU, COND, DOOR, EL/DC** | Manual selection of the corresponding A/C system synoptic page on the SD |
| System page selection (right block) | **FUEL, HYD, WHEEL, F/CTL, C/B, ALL** | idem; **ALL** is additionally hard-wired in discrete to the CDS |
| Checklist / procedures | **T.O CONFIG, C/L, ABN PROC, RCL LAST, MORE, RCL, STS** | Manual checklists and abnormal/supplementary procedures; manual call of the STATUS page; recall |
| Alert message management | **CLEAR** (two CLEAR keys, one per side), **EMER CANC**, **✓ ✓** (two tick keys), **↑ ↓** scroll arrows | "manage alert messages ('CLR', 'RCL', 'EMER CANC', 'RCL LAST', UP/DWN arrows and 'MORE')" |
| Video | **VIDEO** key and **VIDEO** rotary selector | Select video source to display |
| **EWD DU** brightness knob | **OFF … BRT** | Switch ON/OFF the EWD and control its brightness |
| **SD DU** brightness knob | **OFF … BRT** | Switch ON/OFF the SD and control its brightness |
| Discrete-connected keys (highlighted magenta on N4 p.39) | **C/L, ✓, ✓, ↑, ↓, ABN PROC, EMER CANC, STS, RCL, ALL, CLEAR (both)** | Directly connected to FWS (or CDS for "ALL") in discrete to survive an ECP failure |

Function per N1 p.20: "The ECP controls the WD part of the EWD for the management and the display of Warning and Cautions, Normal Checklist, and abnormal procedures. It controls also the SD Main Zone for the selection of A/C systems synoptics and Status pages."

### KCCU — N4 pp.30–31
| Part | Control | Positions / legends | Commands |
|---|---|---|---|
| **KBD (KeyBoarD)** | Function keys | **DIR, PERF, INIT, NAV AID, MAIL BOX, F-PLN, DEST, SEC INDEX, SURV, ATC COM, ND** | "operational shortcuts to increase effectiveness of crew control" |
| KBD | Alphanumeric keypad | QWERTY letters, digits 0–9, `.`, `+/-`, `SP`, `ENT`, backspace | Data insertion |
| KBD | Arrow keys + **ESC**, **CLR INFO** | ▲ ▼ ◀ ▶ | Navigation / escape / clear |
| KBD | **KBD ON/OFF** switch | **ON / OFF** | Powers the keyboard part |
| **CCD (Cursor Control Device)** | Trackball | — | Cursor navigation on display unit screens |
| CCD | Validation knob | — | Select objects |
| CCD | Scrolling wheel | — | Scrolling |
| CCD | Right/left navigation keys | **◀◀ / ▶▶** | Particular actions |
| CCD | **ESC** and **KBD** keys | — | "KBD key used to display the soft keyboard on the MFD" |
| CCD | **CCD ON/OFF** switch | **ON / OFF** | Powers the CCD part |

Function per N1 p.20: "Each KCCU controls: the onside ND, for medium/long term lateral navigation; the onside MFD, for Flight Management System (FMS), ATC-COM system, Aircraft Environment Surveillance System (AESS) and Flight Control Unit (FCU) backup functions; the SD lower part, which displays the ATC Mail Box."

### Electrical Clock — N5 p.45 figure
| Control | Positions | Commands |
|---|---|---|
| **GPS / INT / SET** selector | GPS (external), INT (internal), SET | Selects time-reference mode; "SET" allows manual UTC setting |
| **RUN / STP / RST** selector | RUN, STP, RST | Elapsed-time control |
| **CHR** pushbutton and **RST** pushbutton | — | Chronometer start/stop and reset |
| **SET / DATE** pushbutton | — | Set / display date |

---

## 0.4 LOGIC (IF / THEN, with priority)

### L-A. Automatic DU reconfiguration (N3 p.10)
Trigger: DU failed **or** switched off (brightness knob to OFF).

| Rule | Condition | Action |
|---|---|---|
| A1 | IF **L1** is failed or off | THEN **PFD CAPT is transferred automatically to L2** |
| A2 | IF **R1** is failed or off | THEN **PFD F/O is transferred automatically to R2** |
| A3 | IF **C1** is failed or off | THEN **EWD is transferred automatically to C2** |
| A4 | (after a manual PFD/ND transfer) IF **L2** is failed or off | THEN **PFD CAPT is transferred automatically to L1** |
| A5 | (after a manual PFD/ND transfer) IF **R2** is failed or off | THEN **PFD F/O is transferred automatically to R1** |

Notes state exactly three types of reconfiguration: **automatic reconfiguration**, **manual PFD/ND transfer**, **reconfiguration on manual pilot action**.

### L-B. Manual PFD/ND transfer (N3 p.10)
| Rule | Condition | Action |
|---|---|---|
| B1 | CAPT presses **PFD/ND** P/B on 1313VU | Transfer L1 ↔ L2 (PFD and ND swap sides on the CAPT pair) |
| B2 | F/O presses **PFD/ND** P/B on 1314VU | Transfer R1 ↔ R2 |

### L-C. Reconfiguration on manual pilot action — the RECONF list (N3 p.10 + p.11 figure)
- The CDS holds **one list for CAPT and one for F/O** containing the format(s) of the associated failed or off DU(s) available for reconfiguration.
- After a DU failure or OFF position, the format(s) of the failed/off display are automatically accessible in the list in this fixed order: **MFD, EWD, SD, PFD, ND**.
- The list is reached with the **RECONF P/B** (one CAPT, one F/O) on the CDS reconfiguration control panel 1313VU / 1314VU.
- Each P/B action displays the next format in the list — a scrolling list with an internal priority order.

**List-location priority (which DU shows the RECONF list):**
| Rule | Condition | List available on |
|---|---|---|
| C1 | Default | **L3 (CAPT) / R3 (F/O)** |
| C2 | IF L3 is out (failed or off) | **L2** |
| C3 | IF L3 **and** L2 are out | **L1** |
| C4 | IF R3 is out (failed or off) | **R2** |
| C5 | IF R3 **and** R2 are out | **R1** |

**Constraints:**
| Rule | Statement |
|---|---|
| C6 | "A CDS mechanism avoids the display of the EWD or SD formats at the same time on both sides (not accessible in the list when one is still displayed)." |
| C7 | "Furthermore EWD and SD must not be displayed on L1 and R1." |
| C8 | "In case of no DU failure, there is no effect if the RECONF P/B is pressed." |

**Reconfiguration matrix — formats each DU position can display (N3 p.11 figure, "MANUAL RECONFIGURATION PRINCIPLE"), in the listed order:**

| DU | Formats available, in list order |
|---|---|
| **L1** | PFD, ND, MFD, ETACS, OANS |
| **L2** | ND, PFD, MFD, EWD, SD, OANS |
| **L3** | MFD, PFD, ND, EWD, SD, OANS, VIDEO SD |
| **C1** | EWD |
| **C2** | SD, EWD, VIDEO SD |
| **R3** | MFD, PFD, ND, EWD, SD, OANS, VIDEO SD |
| **R2** | ND, PFD, MFD, EWD, SD, OANS |
| **R1** | PFD, ND, MFD, ETACS, OANS |

### L-D. ECAM mode selection (two note sets — reconcile as below)

**Definitions of the four modes (N1 p.14):**
| Mode | Trigger / behaviour |
|---|---|
| **Normal mode** | "without any A/C system failure, the SD presents automatically A/C system synoptic pages according to the current flight phase computed by the FWS" |
| **Manual mode** | "without any A/C system failure, the SD presents A/C system synoptic pages selected by the crew via the ECAM Control Panel (ECP). Note that the manual mode can override all other modes." |
| **Advisory mode** | "The ECAM permanently monitors the value of some critical system parameters. When a value drifts from its normal range, the Advisory mode is triggered and the ECAM displays automatically the corresponding SD page, with the affected parameter pulsing." |
| **Failure related mode** | "When an A/C system failure occurs the ECAM displays on the EWD the warning and caution messages generated by the FWS. In this case the failure related mode displays automatically on the SD the corresponding A/C system synoptic page." |
| — | "An advisory may or may not lead to a failure. Advisory and Failure related modes are totally independent one from the other and when triggered they cancel the other modes." (N1 p.14) |

**Priority order (N4 p.40, LEVEL 2&3 — the authoritative statement):** "The image displayed on the DU, which process SD format is the result of the CDS SD selector logic which manages the priorities between the different ECAM modes. ECAM modes are triggered according to the following higher to lower priority order:
1. **manual mode / failure related mode**
2. **failure related mode / manual mode**
3. **advisory mode**
4. **flight phase related mode** (= Normal mode)"

with the two tie-breakers that resolve the ambiguous top two lines:
| Rule | Condition | Action |
|---|---|---|
| D1 | A manual crew input occurs while the failure related mode was operating | **Manual mode wins** ("a manual crew input automatically triggers the ECAM manual mode, even if the ECAM failure related mode was operating") |
| D2 | An incoming warning occurs while the ECAM is in a manual mode configuration | **Failure related mode wins** ("an incoming warning automatically triggers the failure related mode") |
| D3 | No manual input and no failure/advisory | **Flight phase (Normal) mode** — SD page follows the FWS-computed flight phase |
| D4 | Monitored parameter drifts out of range, no higher mode active | **Advisory mode** — associated SD page displayed automatically, parameter pulsing |

Flight phases shown on the Normal-mode figure (N1 p.15, N4 p.41): **DOOR → WHEEL → ENGINE → CRUISE → WHEEL → DOOR**.

### L-E. Advisory-mode indication logic (N4 p.42)
| Rule | Condition | Indication |
|---|---|---|
| E1 | Monitored parameter deviates from its defined operational range | **"ADV" appears on the bottom line of the EWD** |
| E2 | SD is displaying a flight-phase page when the advisory occurs | SD automatically displays the associated system page **and** the associated ECP pushbutton **white light comes on** |
| E3 | SD already displays a system page following a previous advisory, and another advisory occurs | **No additional indication** until the first advisory is cleared |
| E4 | SD displays a crew-requested system page and an advisory condition exists | The associated ECP pushbutton **flashes**, prompting the crew to press it |
| E5 | SD displays a system page following an ECAM alert | **No further indication on the EWD** |
| E6 | Crew presses the associated ECP pushbutton, **or** the parameter returns to its defined operational range | **ADV disappears from the EWD** |

### L-F. ADCN-failure backup switchover (N1 pp.6, 10; N3 p.8; N4 pp.22, 32, 36)
| Rule | Condition | Action |
|---|---|---|
| F1 | Complete ADCN failure | EFIS DUs acquire data through the **backup connection directly from the ADIRS** (ADIRS data in ARINC 429) |
| F2 | Complete ADCN failure | ECAM DUs acquire data through the **backup connection directly from the FWS** (ARINC 429) |
| F3 | Complete loss of ADCN network | **Critical systems** send data to the CDS in **ARINC 429** for SD system pages / PFD A/C-config zone |
| F4 | ECP failure | **CLR, RCL, STS, EMER CANC, VALID** keys and the **SCROLL UP/DOWN** device act on the FWS through **direct discrete** connections; **ALL** key acts on the CDS in discrete |
| F5 | CAN network failure | "A failure of the CAN network does not disturb the discrete links functioning"; "The loss of one channel does not cause the complete loss of the CAN bus" |

### L-G. DU cross monitoring (N4 p.28)
| Rule | Statement |
|---|---|
| G1 | Each DU monitors its own control/display capability and its I/O status, with CDS-internal and external equipment (**DU self monitoring / normal monitoring**) |
| G2 | "A DU monitors one other DU, which in turn monitors another DU. This makes a feedback monitoring 'loop'. **There are two independent feedback monitoring loops, each loop includes four DUs.**" |
| G3 | Example loop given: **CAPT PFD monitors EWD → EWD monitors CAPT ND → CAPT ND monitors CAPT MFD → CAPT MFD monitors CAPT PFD** |
| G4 | IF **CAPT MFD failure or power supply lost** THEN **CAPT ND monitors CAPT PFD** (loop closes over the failed DU) |
| G5 | IF a monitoring DU detects a difference between the data it receives from a source system and the data shown on the monitored DU THEN it shows a message telling the crew the data shown is incorrect: the monitored DU **and the same related DU on the other side** show the message **"Check <DU>"** (DU = F/O PFD, CAPT PFD, F/O ND …) |
| G6 | In addition an alarm is sent to the **FWS** and to the **CMS**, "that respectively generate a warning and a fault message". The figure shows the EWD warning **"CDS DISPLAY DISAGREE"** |

### L-H. BITE centralisation (N4 p.20)
| Rule | Statement |
|---|---|
| H1 | The **EWD** is connected to the CAN network through **CAN bus 1.1** and **CAN bus 2.1** to centralise the BITE data of all DUs and KCCUs and transmit it to the CMS through the ADCN |
| H2 | IF the **EWD is failed or OFF** THEN **the SD takes over this function** |

### L-I. DU cooling / thermal protection (N4 p.26)
| Rule | Condition | Action |
|---|---|---|
| I1 | Loss of air blowing/extraction to the DUs | DU power consumption is reduced: **brightness reduced more or less to fifty percent**, **only critical parameters are displayed**, **video functions are inhibited** |
| I2 | Loss of air cooling (too high air temperature **or** too low blown massflow) detected by cooling effect detectors | Information provided to the CDS through AFDX by the AVS application in CPIOM-B3/4 |
| I3 | DU internal temperature increases to a high level | "an internal protection manages DU inner temperature… the DU power consumption is reduced, the same way as in case of loss of blowing/extraction" |
| I4 | Total loss of cooling air supply | The DUs withstand it for **thirty minutes (specified)** — matched to the duration of descent and approach flight phases |
| I5 | Emergency electrical configuration | "information for loss of air-cooling is still available for remaining DUs" |

### L-J. Clock mode logic (N5 p.44)
| Rule | Condition | Action |
|---|---|---|
| J1 | Normal configuration ("external mode") | MMR1 (GPS1) sends time reference to the clock; clock transmits time/date to users through ADCN |
| J2 | Crew detects erroneous/inaccurate GPS time → selects **"INT"** | Clock increments time/date on its internal time base (from last valid GPS data or manually set time) and transmits to users |
| J3 | Mode = external ("GPS") **and** external source not available (GPS failed) | **Degraded mode**: clock increments automatically without crew action on its internal time base, based on last valid external data |
| J4 | External source becomes available again | Clock displays and outputs the external-source data (MMR/GPS1) |
| J5 | Degraded mode duration | Time reference considered UTC data **during 24 hours**; after that the accuracy does not guarantee UTC |
| J6 | Clock data failure **or** clock in "SET" mode | Time reference backed up by the **three ADIRUs** via ADCN |
| J7 | MMR-GPS data lost | ADIRUs internally provide the time reference |

---

## 0.5 STATES (named configurations)

| id | Name | Definition / what is displayed | Source |
|---|---|---|---|
| S0 | **Normal 8-DU configuration** | L1 = CAPT PFD, L2 = CAPT ND, C1 = EWD, C2 = SD, L3 = CAPT MFD, R3 = F/O MFD, R2 = F/O ND, R1 = F/O PFD. EWD on the **upper ECAM DU**, SD main zone on the **lower ECAM DU**, both PFD lower zones on the **outer DUs** | N1 pp.4, 10; N3 pp.8, 18 |
| S1 | **L1 failed / OFF** | PFD CAPT transferred automatically to **L2** (L2 then shows PFD instead of ND). ND format becomes available in the CAPT RECONF list on L3 | N3 p.10 |
| S2 | **R1 failed / OFF** | PFD F/O transferred automatically to **R2** | N3 p.10 |
| S3 | **C1 (EWD) failed / OFF** | EWD transferred automatically to **C2**. SD format becomes available in the RECONF list. In addition, SD takes over the BITE-centralisation function from the EWD | N3 p.10; N4 p.20 |
| S4 | **L2 failed / OFF after a PFD/ND transfer** | PFD CAPT transferred automatically back to **L1** | N3 p.10 |
| S5 | **R2 failed / OFF after a PFD/ND transfer** | PFD F/O transferred automatically back to **R1** | N3 p.10 |
| S6 | **L3 (CAPT MFD) failed / OFF** | No automatic transfer; the CAPT RECONF list moves to **L2**. MFD format is first in the recovery list. (Also: with CAPT MFD lost, CAPT ND monitors CAPT PFD) | N3 p.10; N4 p.28 |
| S7 | **L3 and L2 out** | CAPT RECONF list available on **L1** | N3 p.10 |
| S8 | **R3 (F/O MFD) failed / OFF** | F/O RECONF list moves to **R2** | N3 p.10 |
| S9 | **R3 and R2 out** | F/O RECONF list available on **R1** | N3 p.10 |
| S10 | **C2 (SD) failed / OFF** | SD format recoverable via the RECONF list on L2/L3/R2/R3 (not on L1/R1) | N3 pp.10–11 |
| S11 | **Manual PFD/ND transferred (CAPT)** | L1 ↔ L2 swapped: PFD on the inner DU, ND on the outer DU | N3 p.10 |
| S12 | **Manual PFD/ND transferred (F/O)** | R1 ↔ R2 swapped | N3 p.10 |
| S13 | **ADCN complete failure** | DUs run on backup connections: EFIS from ADIRS (ARINC 429), ECAM from FWS (ARINC 429), critical systems in ARINC 429 for SD pages. Video via CMV is direct and unaffected | N1 pp.6,10; N4 pp.22,32,36 |
| S14 | **ECP failure** | CLR / RCL / STS / EMER CANC / VALID and SCROLL UP-DOWN work through discrete to FWS; ALL works through discrete to CDS; other ECP functions lost | N4 pp.36, 38 |
| S15 | **On ground, BAT configuration** | "ONLY EWD AND CAPT MFD ARE SUPPLIED. IN THIS CONFIGURATION, RECONF PUSH BUTTON BECOMES ACTIVE, ALLOWING TO RECOVER SD ON CAPTAIN MFD" | N3 p.9 figure |
| S16 | **Loss of DU air blowing/extraction (or DU over-temperature)** | Brightness reduced ~50 %, only critical parameters displayed, video functions inhibited; DUs withstand total loss of cooling air for 30 min | N4 p.26 |
| S17 | **DU disagree (cross-monitoring trip)** | Monitored DU and the same related DU on the other side show **"Check <DU>"**; EWD shows **CDS DISPLAY DISAGREE**; FWS warning + CMS fault message | N4 pp.28–29 |
| S18 | **ECAM Normal (flight-phase) mode** | SD shows the synoptic page for the FWS-computed flight phase (DOOR / WHEEL / ENGINE / CRUISE / WHEEL / DOOR) | N1 p.14 |
| S19 | **ECAM Manual mode** | SD shows the page selected on the ECP; overrides all other modes | N1 p.14; N4 p.40 |
| S20 | **ECAM Advisory mode** | SD auto-displays the affected system page with the parameter pulsing; **ADV** on the bottom line of the EWD; associated ECP P/B white light on (or flashing) | N1 p.14; N4 p.42 |
| S21 | **ECAM Failure-related mode** | EWD shows FWS warning/caution messages; SD auto-displays the corresponding system synoptic page | N1 p.14 |
| S22 | **Clock external / internal / degraded mode** | See L-J | N5 p.44 |

---

## 0.6 INDICATIONS — what each display zone shows

| Display | Zone | Contents (as listed in the notes) | Driven by |
|---|---|---|---|
| **PFD** | **PFD Main Zone** (the "two upper thirds") | aircraft attitudes; air speed; altitude and vertical speed; heading; information on flight modes; radio altitude; landing system data | EFIS (from ADIRS + A/C systems) |
| **PFD** | **A/C Configuration and Flight Limitation Zone** (lower zone) — "not part of the EFIS, related to the ECAM system" | slats, flaps and trim position; memos and limitations. "all memos and limitations generated by the FWS are displayed on the WD while PFDs display only Memos and Limitations related to short-term flight" | ECAM / FWS |
| **ND** | **ND Main Zone** (the "two upper thirds") | aircraft location with respect to the flight plan and/or NAVAIDS (Navigation Aid); weather radar information; surveillance information | EFIS |
| **ND** | **Vertical Display (VD) Zone** (lower third) | aircraft altitude; safe altitude; trajectory; terrain and weather. "takes into account the vertical selected or managed profile, and improves crew awareness on A/C vertical situation by providing a synthetic view of vertical parameters". "Note that the VD also displays a ND FM Dialog Window" | EFIS |
| **EWD** | **Engine Display (ED) Zone** | all engine primary parameters | "driven by the ECAM itself" |
| **EWD** | **Warning Display (WD) Zone** | Warning/Caution messages and corresponding procedures; Memos; general Limitations; normal checklists; abnormal procedures. Also carries the **ADV** indication on its bottom line | "driven by the FWS" |
| **SD** | **SD Main Zone** (upper zone) | A/C systems synoptic pages, **or** the Status page | synoptics driven by the ECAM itself; Status page driven by the FWS |
| **SD** | **Permanent Data Zone** (middle zone) | permanent data related to temperature, time, weight and fuel (figure shows TAT, SAT, UTC clock, GW, GWCG, FOB) | "driven by the ECAM as well" |
| **SD** | **Air Traffic Control (ATC) Mail Box** (lower zone) | ATC mail box | **"not driven by the ECAM"**; controlled by the onside KCCU |
| **MFD** | **Upper MFD zone** | "specific to each system, is used for the pages selection" — MFD menu + system sub-menu | remote user applications |
| **MFD** | **MFD Main Display** | "dedicated to the display of remote user application functions" — the page content of the system sub-menu | FMS / AESS / ATC-COM / FCU Backup |
| **MFD** | **Bottom message area** | "one small area at the bottom, to show messages. This area is referred to as the 'bottom message area'" | remote user applications |
| **MFD** | Four available menus | **FMS** (managed by the FMS), **ATC COM** (managed by the ATC system), **SURV** (managed by the AESS), **FCU BKUP** (managed by the FCU Backup application) | — |

**Interactivity / pilot-area allocation (N1 p.21 figure "CDS FUNCTIONS ALLOCATION REVIEW AND INTERACTIVITY"):**
- **KCCU interactive areas (CAPT):** CAPT ND (part), CAPT MFD (FMS / ATC COM / AESS / FCU Back-up), SD ATC Mail Box
- **KCCU interactive areas (F/O):** F/O ND (part), F/O MFD, SD ATC Mail Box
- **ECP piloted area:** EWD Warning Display, SD Main Zone (+ Permanent Data Zone shown within the SD block)
- **EFIS control panel piloted area:** PFD Main Zone, A/C Configuration & Flight Limitation zone, ND (part)
- The A380 CDS allocation philosophy "is based on the Airbus family T: **PFD-ND Capt, EWD-SD, ND-PFD F/O**"

**Maintenance / failure indications:** "Check <DU>" message on the monitored DU and its cross-side twin; **CDS DISPLAY DISAGREE** on the EWD; FWS warning; CMS fault message; CDS BITE fault messages to CMS/OMS.

---

## 0.7 NUMBERS — the whitelist

Only these values may be shown as "specified". Anything else must be tagged **(assumed)**.

| Value | Meaning | Source |
|---|---|---|
| **8** | identical and interchangeable Display Units | N1 p.4; N3 p.8; N4 p.24 |
| **2** | PFDs | N1 p.4; N3 p.8 |
| **2** | NDs | N1 p.4; N3 p.8 |
| **1** | EWD | N1 p.4; N3 p.8 |
| **1** | SD | N1 p.4; N3 p.8 |
| **2** | MFDs | N1 p.4; N3 p.8 |
| **2** | KCCUs (one per pilot) | N1 p.4; N4 p.30 |
| **8 inch by 6 inch** | enlarged smart LCDU size (LEVEL I wording) | N1 p.4 |
| **6.17 in x 8.22 in** | usable display area of each DU (LEVEL 2&3 wording) | N4 p.24 |
| **1313VU** | CDS Reconfiguration control panel, Captain | N1 p.7; N3 pp.9, 11 |
| **1314VU** | CDS Reconfiguration control panel, F/O | N1 p.7; N3 pp.9, 11; N4 p.33 |
| **1314VM** | same F/O panel as labelled on one LEVEL I figure (conflict) | N1 p.11 |
| **1135VM** | ECP (ICP on the pedestal) | N1 p.11; N2 p.4 |
| **1135VU** | same ECP as labelled on one LEVEL 2&3 figure (conflict) | N4 p.43 |
| **1211VM, 1212VM, 1215VM, 1221VM, 1222VM, 1225VM, 1231VM, 1245VM, 1255VM** | ICPs installed on the overhead panel | N2 p.4 |
| **1235VM** | further ICP CAN panel (overhead, shown in N2 p.5 figure and listed among the five ICPs CAN) | N2 pp.5, 6 |
| **5** | number of ICPs CAN (1211VM, 1212VM, 1215VM, 1225VM, 1235VM) | N2 p.6 |
| **5** | number of ICPs no CAN (1221VM, 1222VM, 1231VM, 1245VM, 1255VM) | N2 p.6 |
| **IOMs 1, 2, 5, 6** | IOMs the ICPs CAN connect through | N2 p.6 |
| **IOMs 7, 8** | IOMs the ECP connects through | N2 p.6 (figure IOM-A 7/8); N4 p.38 |
| **IOM-A 5, 6** | IOM the electrical clock connects through | N5 p.45 figure |
| **4** | segregated ICP CAN channels | N2 p.6 |
| **CAN 1.1, CAN 1.2 (side 1); CAN 2.1, CAN 2.2 (side 2)** | ICP CAN channel names | N2 p.6 |
| **CAN ECP1 (side 1), CAN ECP2 (side 2)** | ECP CAN channels (two segregated) | N2 p.6 |
| **125 Kb/s** | CAN data transmission rate | N2 p.6 |
| **CAN 02B** | CAN norm used | N2 p.6 |
| **CAN BUS 1.1, 1.2, 2.1, 2.2** | CDS-dedicated CAN buses (two per side, each redundant) | N4 pp.20–21 |
| **2** | CAN connections per DU | N4 p.20 |
| **CAN bus 1.1 and CAN bus 2.1** | the two buses through which the EWD centralises BITE data | N4 p.20 |
| **2** | independent DU feedback monitoring loops | N4 p.28 |
| **4** | DUs per feedback monitoring loop | N4 p.28 |
| **≈ 40 °C** | T DU nominal | N4 p.27 figure |
| **~50 %** | brightness reduction on loss of blowing/extraction ("reduced more or less to fifty percent") | N4 p.26 |
| **30 minutes** | duration DUs withstand total loss of cooling air supply (explicitly "specified") | N4 p.26 |
| **CPIOM-B3, CPIOM-B4** | modules hosting the two AVS applications | N4 p.26 |
| **2** | Avionics Ventilation System (AVS) applications | N4 p.26 |
| **3** | ADIRUs providing clock back-up | N5 p.44 |
| **24 hours** | period during which degraded-mode clock time is considered UTC data | N5 p.44 |
| **MMR 1 (GPS1), MMR 2 (GPS2)** | external time reference receivers | N5 pp.44–45 |
| **ARINC 429** | backup data format (ADIRS, FWS, critical systems) | N4 pp.22, 32, 36 |
| **RS 422** | KCCU ↔ OANS link | N4 p.22 |
| **AFDX** | DU ↔ ADCN transmission standard (Avionics Full Duplex Switched Ethernet) | N4 pp.20, 22 |
| **DC ESS BUS / DC BUS 1 / DC BUS 2 / DC BUS 1 (BACKUP) / DC BUS 2 (BACKUP)** | DU and KCCU supply buses per the 0.2 power table | N3 p.9 figure |
| ND ranges **ZOOM, 10, 20, 40, 80, 160, 320, 640** | EFIS control panel ND range selector positions | N4 p.35 figure |
| **1013** (QNH), **in Hg / hPa** | baro reference window value and unit selector positions on the EFIS CP figure | N4 p.35 figure |
| **Apr 19, 2007** / **Nov 21, 2011** / **01 AUG 2013** | note-set issue dates carried in the page footers | all |

Illustrative screen values appearing in the sample screenshots (FLEX 83.9 % 59 °C, N1 84.7, EGT 751, FF 4100 KG/H, FU TOTAL 20050/20000, 80100 KG, LDG ELEVN 300 FT, AUTO CAB ALT 500 FT, TAT +10 °C, SAT +10 °C, 13:28:00 GPS, GW 500000 KG, GWCG 40.0 %, FOB 240900 KG, GS 380, TAS 480, 068°, 59 NM, 19:14, TBN 109.30, 4.0 NM, MAX SPD VLE = 200 KTS, GREEN/YELLOW 5000 PSI, 93.6 / 92.6 / 9120 / 118 / 220 on the ENGINE page) are **sample display data only**, expressly annotated in the notes as "RR PARAMETERS AND METRIC UNITS ARE USED ON EWD AND SD AS AN EXAMPLE" — do not present them as system specifications.

---

## 0.8 GAPS (things the simulation needs that the notes do not state)

| # | Gap | Conservative assumption to use, labelled "(assumed)" |
|---|---|---|
| G1 | **ETACS is never expanded or described.** It appears only as a reconfigurable format on L1/R1. | Treat as an opaque selectable format label; display the text "ETACS — format available on L1/R1 only; not defined in these notes **(assumed)**". Do not invent an expansion. |
| G2 | **OANS is used but not expanded in these pages** (only "Airport Navigation screen" and the RS 422 link). | Show as "OANS — Airport Navigation function **(assumed expansion: On-board Airport Navigation System)**". |
| G3 | **VIDEO SD** appears in the L3/C2/R3 reconfiguration lists but is not described. | Model as "SD format with video source selected via the ECP VIDEO selector **(assumed)**". |
| G4 | **No EFIS control panel VU/VM number is given.** | Leave the identifier blank; label the panel "EFIS Control Panel (panel number not stated in the notes)". Do not invent a number. |
| G5 | **The OIT brightness knob on 1313VU/1314VU is shown but not described.** | Label "OIT brightness — control present on the panel; function not covered in these notes **(assumed inactive in this simulation)**". |
| G6 | **No reconfiguration timings** (transfer delay, RECONF debounce, message-latch times). | Use instantaneous transfer on the model tick, and label any displayed timing "(assumed)". |
| G7 | **No DU electrical ratings** (voltage, current, power draw). | Do not display any. Show only the bus names from the 0.2 power table. |
| G8 | **The DU failure detection threshold / self-test criteria are not given.** | Model a DU as either healthy, failed, or OFF (brightness knob at OFF). No intermediate states. |
| G9 | **The second feedback monitoring loop is not enumerated** — only the CAPT-side example is given. | Model the F/O-side loop by symmetry (F/O PFD → SD → F/O ND → F/O MFD → F/O PFD) and tag the whole second loop "(assumed by symmetry — not stated in the notes)". |
| G10 | **Which parameters are "critical parameters" retained under reduced cooling is not defined.** | Display the wording "only critical parameters are displayed" without enumerating them. |
| G11 | **The full ECAM system-page catalogue is not given** — only the ECP key legends (ENG, BLEED, PRESS, EL/AC, APU, COND, DOOR, EL/DC, FUEL, HYD, WHEEL, F/CTL, C/B, ALL) and the sample WHEEL, ENGINE, HYD, CRUISE pages. | Build only those pages named on ECP keys; render each as a labelled placeholder synoptic except the four sampled ones, and tag placeholder content "(assumed illustrative)". |
| G12 | **The mapping of ECAM flight phases to specific SD pages is not tabulated** — only the phase strip DOOR/WHEEL/ENGINE/CRUISE/WHEEL/DOOR. | Map phase → same-named page (DOOR, WHEEL, ENGINE, CRUISE) and tag "(assumed)". |
| G13 | **The list of "critical systems" that send ARINC 429 backup data is not enumerated.** | Show the block as "CRITICAL SYSTEMS" exactly as the figure does; do not name members. |
| G14 | **The RECONF list priority "internal to the list"** is stated but the tie-break between CAPT list and F/O list for a shared format (EWD/SD) is only given as an exclusion rule. | Implement first-come exclusion: whichever side already displays EWD or SD blocks the other side's access (directly from rule C6); tag the arbitration order "(assumed)". |
| G15 | **CDAM / SCIs** appear only in a figure with no text. | Render as figure blocks with no behaviour, tagged "(shown in the notes' figure only — no description)". |
| G16 | **Panel VU numbers for the KCCU and the electrical clock** are not given. | Leave blank. |

---

## 0.9 LEARNING OUTCOMES (CAAS SAR-66 Cat B2, Level 2)

On completion of this simulation the learner can:

1. **Identify** the eight CDS display units by cockpit position (L1, L2, C1, C2, L3, R3, R2, R1) and state the display format each carries in the normal configuration, together with the control panel that drives each format (EFIS control panel, ECP, CDS RECONF panel 1313VU/1314VU, KCCU).
2. **Trace** the data path that supplies any given display format from its source system to the DU, distinguishing the normal ADCN/AFDX route from the ADIRS, FWS and critical-systems ARINC 429 backup routes, the direct CMV optic-fibre video route and the KCCU CAN-bus control route.
3. **Predict** the resulting cockpit display layout after a stated DU failure or OFF selection, applying the automatic reconfiguration rules (L1→L2, R1→R2, C1→C2), the manual PFD/ND transfer, and the RECONF list order MFD-EWD-SD-PFD-ND with its L3/L2/L1 and R3/R2/R1 list-location priority and the EWD/SD exclusion constraints.
4. **Operate** the EFIS control panel, the CDS reconfiguration control panel and the ECP to select ND modes and ranges, recover a lost format on an available DU, and call a chosen A/C system synoptic page or the STATUS page on the SD.
5. **Explain** the four ECAM modes (Normal/flight-phase, Manual, Advisory, Failure related), state their priority order, and justify which mode is displayed for a given combination of crew input, warning and out-of-range parameter, including the ADV indication logic on the EWD.
6. **Isolate** a CDS defect from its indications — distinguishing a DU failure, a DU cross-monitoring disagree ("Check <DU>" / CDS DISPLAY DISAGREE), an ADCN loss, an ECP failure, a DU cooling loss and a BAT-configuration power limitation — and name the correct recovery action and the BITE/CMS data available.

---

## 0.10 MISCONCEPTIONS the simulation must expose

| # | Misconception | How the sim must break it |
|---|---|---|
| M1 | "The DUs are dedicated units — the PFD unit is different hardware from the SD unit." | All eight DUs are identical in hardware **and** software; only **pin programming** by location activates a function. Let the student swap any DU and see the same box behave as a different display. |
| M2 | "Pressing the RECONF pushbutton always changes the display." | "In case of no DU failure, there is no effect if the RECONF P/B is pressed." Make the P/B visibly inert in the healthy configuration. |
| M3 | "Any format can be recovered on any DU." | EWD and SD **must not** be displayed on L1 and R1, and a CDS mechanism blocks EWD or SD appearing on both sides at once. Let the student attempt it and be refused, with the reason shown. |
| M4 | "The RECONF list always lives on the MFD (L3/R3)." | It migrates: L3 → L2 → L1 (and R3 → R2 → R1) as those DUs go out. Force the student through a two-DU-out case. |
| M5 | "Losing the ADCN blanks the displays." | Backup connections keep essential data flowing — EFIS from ADIRS in ARINC 429, ECAM from FWS, SD system pages from critical systems, video directly from the CMV. Show the degraded but live picture, and show which content is lost. |
| M6 | "Manual mode always wins over everything." | LEVEL I says "the manual mode can override all other modes", but LEVEL 2&3 adds that **an incoming warning automatically triggers the failure related mode** even from a manual configuration. Stage that sequence explicitly. |
| M7 | "The ATC Mail Box is part of the ECAM because it is on the SD." | The ATC Mail Box zone is **not driven by the ECAM** — it is a KCCU-controlled ATC-COM area sitting inside the SD image. |

---

## 0.11 DEFINITIONS & PRECEDENCE

### Operative terms, in the notes' sense
| Term | Definition as used in these notes |
|---|---|
| **CDS — Control and Display System** | "an avionics world system connected with most of the other aircraft systems in order to display flight information, to allow systems monitoring and aircraft environment video monitoring, through eight identical and interchangeable Display Units". It **includes** the EFIS and ECAM functions and **supplies** display resources to remote user applications. |
| **Smart DU** | An LCD display unit that "includes all resources to fulfil CDS functions" — the display processing is inside the DU itself, not in a separate symbol generator. All eight are identical; the active function is set by **pin programming** according to cockpit location. |
| **Format** | The display content a DU can render (PFD, ND, MFD, EWD, SD, OANS, ETACS, VIDEO SD). Reconfiguration moves **formats**, not hardware. |
| **Reconfiguration** | Recovering, on an available DU, a display lost after a DU failure or OFF selection: "The aim of the reconfiguration function is to allow pilot to recover the display lost after DU failure on an available DU." Three types: **automatic**, **manual PFD/ND transfer**, and **reconfiguration on manual pilot action** (the RECONF list). |
| **Automatic reconfiguration** | The transfer that happens with no crew action when L1, R1 or C1 fails or is switched off. |
| **Manual PFD/ND transfer** | Crew-commanded swap of the PFD and ND between the outer and inner DU of one side, via the PFD/ND P/B on 1313VU (CAPT) / 1314VU (F/O). |
| **RECONF list** | The per-pilot scrolling list of formats belonging to failed/off DUs, ordered MFD, EWD, SD, PFD, ND, stepped through by the RECONF P/B; it has an internal priority order and a defined host-DU priority (L3→L2→L1, R3→R2→R1). |
| **Failed or off** | The notes treat a failed DU and a DU whose brightness knob is at OFF identically for all reconfiguration logic. |
| **Backup (connection)** | A direct, non-ADCN data path used "in order to overcome a complete ADCN failure": ADIRS→EFIS DUs, FWS→ECAM DUs, critical systems→DUs, all in **ARINC 429**; plus the ECP's **discrete** links to FWS/CDS to overcome an ECP failure. Distinct from **backup power supply** (the DC BUS 1/2 (BACKUP) columns of the power table). |
| **Cursor / focus** | The KCCU interaction means: "These LCDUs are equipped with more interactive capability through the use of cursors or focus, controlled by the Keyboard and Cursor Control Units (KCCUs)." The **cursor** is moved by the CCD trackball; **focus** is the selected interactive element. The notes use them as alternative interaction models on the same DUs. |
| **Interactive area** | A screen region a given control means may act on. Per N1 p.21: KCCU interactive areas (CAPT green / F/O blue) = onside ND, onside MFD, SD ATC Mail Box; ECP piloted area = EWD Warning Display and SD Main Zone; EFIS control panel piloted area = PFD Main Zone, A/C config & flight limitations zone, ND. |
| **CCD — Cursor and Control Device / Cursor Control Device** | Trackball-based half of the KCCU; carries trackball, validation knob, scrolling wheel, right/left navigation keys, ESC and KBD keys, CCD ON/OFF switch. N1 p.5 expands it "Cursor and Control Device"; N4 p.31 expands it "Cursor Control Device". |
| **KBD — KeyBoarD** | QWERTY, multifunction keyboard half of the KCCU: function keys, alphanumeric keypad, arrow keys, KBD ON/OFF switch. Functionally **segregated** from the CCD with independent CAN bus connections despite sharing the equipment item. |
| **Remote user application** | A system that is **not hosted in the CDS** but is given display resources (and usually an MFD HMI) by it: FWS, CMV, FMS, AESS, ATCS, FCU Backup. |
| **HMI** | Human-Machine Interface; "The CDS gives most of these systems a dedicated Human-Machine Interface (HMI) called Multi-Function Display (MFD)". |
| **ICP (VM) vs VU** | **ICP** = Integrated Control Panel, identified by a **VM** number, mainly on the overhead panel and part of the pedestal; **VU** = conventional control panel, on the consoles, main instrument panel, glareshield and partly the overhead. |
| **ICP CAN / ICP no CAN** | ICP CAN uses discrete, analog **and** CAN interfaces (1211/1212/1215/1225/1235VM); ICP no CAN uses only discrete and analog (1221/1222/1231/1245/1255VM). |
| **Definition File (DF)** | "a set of data, which specifies to the CDS the graphics/widgets to be displayed on the DUs". One CDS DF is under CDS responsibility; the FWS, FMS, FCU Backup, AESS, ATC and CMV DFs live in the DUs but belong to the remote user applications. |
| **DU normal monitoring / self monitoring** | Each DU monitors its own control and display capability and its I/O status. |
| **DU feedback monitoring** | The cross-check loop in which each DU monitors one other DU; two independent loops of four DUs; a detected data mismatch produces "Check <DU>" plus a FWS warning (CDS DISPLAY DISAGREE) and a CMS fault message. |
| **Advisory** | A monitored critical parameter drifting from its **defined operational range** — flagged by **ADV** on the EWD bottom line and automatic display of the affected SD page with the parameter pulsing. "An advisory may or may not lead to a failure." |
| **Failure related mode** | The ECAM state entered when an A/C system failure occurs: FWS warning/caution on the EWD + the corresponding system synoptic on the SD. |
| **Flight phase related mode** | The LEVEL 2&3 name for the LEVEL I **Normal mode** — SD page follows the FWS-computed flight phase. Treat the two names as the same mode. |
| **BITE** | Built-In Test Equipment inside each DU; BITE data of all DUs and KCCUs is centralised by the EWD (SD if EWD failed/off) over CAN 1.1/2.1 and sent to the CMS via the ADCN. |

### Conflicts between the note sets, and the precedence taken

| # | Conflict | Resolution |
|---|---|---|
| C-1 | **F/O CDS reconfiguration panel number:** N1 p.7 and all LEVEL 2&3 pages say **1314VU**; the single N1 p.11 ECAM figure says **1314VM**. | Use **1314VU** — three independent occurrences including both LEVEL 2&3 figures, and it matches the VU/VM convention (a panel on the main instrument panel area is a VU). Treat "1314VM" as a figure typographical error; note it in the glossary. |
| C-2 | **ECP panel number:** N1 p.11 figure and the LEVEL 2&3 ICP location text (N2 p.4) say **1135VM**; the N4 p.43 advisory-mode figure says **1135VU**. | Use **1135VM** — it is the one stated in body text ("The ICP 1135VM, which is called ECAM Control Panel (ECP) is installed on the pedestal"), and the ECP is explicitly an **ICP**, which carries VM numbers. |
| C-3 | **DU size:** N1 p.4 "8 inch by 6 inch"; N4 p.24 "6.17 in x 8.22 in usable display area". | Not a true contradiction — 8×6 in is the LEVEL I round figure for the screen, 6.17×8.22 in is the LEVEL 2&3 **usable display area**. Show both, each with its own label. Prefer the LEVEL 2&3 figure for any dimension quoted as a specification (higher level, more recent). |
| C-4 | **EWD name:** N1 "Engine Warning Display"; N3 p.8 "Engine/Warning Display". | Both are in the notes. Use **"Engine Warning Display (EWD)"** as the primary expansion (used in both note sets' glossary boxes) and show "Engine/Warning Display" as an accepted variant. |
| C-5 | **CCD expansion:** N1 p.5 "Cursor and Control Device"; N4 p.31 "Cursor Control Device". | Show both; prefer **"Cursor Control Device"** for LEVEL 2&3 material (more recent, and used in the KCCU description body text). |
| C-6 | **ECP → ECAM/FWS control path:** N1 p.10 "the ECP controls the ECAM and the FWS via the ADCN or **directly through backup connections**"; N4 p.36 "via the ADCN or directly through **discrete signals**". | Same mechanism, different wording. Use the LEVEL 2&3 wording (**discrete signals**) as the technical statement — it is more specific and lists the exact keys. |
| C-7 | **ECAM mode priority:** N1 p.14 says only "the manual mode can override all other modes" and that advisory and failure-related modes "cancel the other modes"; N4 p.40 gives the explicit four-line priority order plus the two mutual-trigger rules. | Prefer the **LEVEL 2&3 rule set (N4 p.40)** for the simulation logic — the master-prompt precedence rule is "the more detailed set for logic". Keep the LEVEL I sentences as teaching text. |
| C-8 | **N1 p.4 lists "2 Multi-Function Displays (MFDs)" as one of the eight formats, while also saying the MFDs "ensure part of the control and display capabilities carried out on the previous Airbus programs by the Multipurpose Control and Display Units (MCDUs)".** | No conflict; record MCDU as the legacy equipment the MFD replaces. |

**General precedence adopted:** ratings, panel identifiers and hardware specs come from the **LEVEL 2&3 set (N2/N3/N4)** as the higher-level and more recent (Nov 2011 / 01 AUG 2013) material; behavioural logic (reconfiguration rules, ECAM priority, monitoring, backup switchover) also comes from the LEVEL 2&3 set because it is the more detailed one; the **LEVEL I set (N1, Apr 2007)** supplies the introductory framing, the zone-by-zone display content lists and the interactivity-allocation picture, and is used where the LEVEL 2&3 set is silent.

---

# PART B — DESIGN BRIEF

**File produced:** `aerosim_ata31_control_display_system.html`

## Archetype: HYBRID

SYSTEM is the right base — the CDS is an architecture of sources, a network and eight display resources, solved as a directed allocation graph with reconfiguration rules, not as a nodal circuit. HYBRID is chosen over pure SYSTEM because the topic has two genuinely different pictures the student must hold at once: the **cockpit** (which format is on which DU right now) and the **data network** (which path is feeding that format), so Explore carries both views and the same click selects the same component in either.

## Page map

| Mode | What this topic gets |
|---|---|
| **Explore** | Two switchable SVG views. *Cockpit* draws the eight DUs at their real panel positions with a live miniature of the format each is rendering, plus the EFIS control panels, 1313VU/1314VU, the ECP and the KCCUs. *Architecture* draws the ADCN, CAN buses, ADIRS, FWS, CMV, critical systems, IOMs, CMS and DLCS with animated flow, colour-coded ADCN / ARINC 429 backup / CAN / CMV-video. Clicking a DU signal-traces its format back to its source and lists the ordered chain. Inspector gives ratings, supply buses, the format matrix, the zone table and "what if it fails". Scenario selector covers all 14 named states; the build-up stepper introduces the system one component at a time in 14 steps. |
| **Build** | Constructor for the CDS data architecture — 12 palette blocks derived from 0.1, orthogonal wiring, drag/nudge/delete, undo/redo, JSON export/import. Instruments are archetype-correct: a **path continuity tester** and a **source readout**, not a voltmeter or scope. Three starter architectures (normal, ADCN-lost, BITE collection) and six *check-my-build* targets. |
| **Fault Lab** | 11 injectable faults, six diagnostic tests, Observe → Hypothesise → Test → Isolate → Rectify → Verify with a step counter, an efficiency score against the one-test minimum, a seeded exam mode and a debrief naming the misconception each fault exposes. |
| **Learn** | 12 lesson steps with predict-observe-explain and auto-detected completion conditions, then a 12-question quiz mapped to LO1–LO6 with a copyable Brightspace results block. |

## Scenarios (0.5)

S0 normal · S1 L1 failed · S2 R1 OFF · S3 C1 failed · S6 L3 failed · S7 L3+L2 out · S10 C2 failed · S11 manual PFD/ND transfer · S13 ADCN complete failure · S14 ECP failure · S15 BAT configuration · S16 cooling loss · S17 cross-monitoring disagree · FREE free play.

## Faults

L1 internal failure · C1 (EWD) failure · complete ADCN failure · ECP failure · cross-monitoring disagree · loss of DU air blowing/extraction · L3 and L2 both out · BAT configuration · R1 brightness knob at OFF · CAN network failure · C2 (SD) failure.

## Check-my-build targets

Normal EFIS supply · EFIS backup on ADCN loss · ECAM backup on ADCN loss · normal ECP control path · KCCU control path · video path.

## Outcome mapping

| Lesson steps | Quiz questions | Outcome |
|---|---|---|
| 1, 2 | 1 | LO1 identify the eight DUs and their driving panels |
| 9 | 8, 9 | LO2 trace a format from source to DU, normal vs backup |
| 3, 4, 5, 6 | 2, 3, 4, 5 | LO3 predict the layout after a DU failure |
| 7 | 6 | LO4 operate the panels |
| 8 | 7 | LO5 explain the four ECAM modes and their priority |
| 10, 11, 12 | 10, 11, 12 | LO6 isolate a CDS defect from its indications |

## Misconceptions the design forces into the open

M1 is broken by the identical-DU model (step 1, Q1); M2 by making the RECONF button visibly inert on a healthy aircraft (step 7, Q6); M3 by refusing EWD/SD on L1/R1 (step 6, Q5); M4 by the list migration in scenario S7 (step 5, Q4); M5 by keeping the displays alive on an ADCN loss (step 9, Q8); M6 by staging the manual→warning→manual sequence (step 8, Q7); M7 by labelling the ATC Mail Box zone as not driven by the ECAM in the SD zone table.
