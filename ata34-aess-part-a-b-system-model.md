# PART A — SYSTEM MODEL
## A380 ATA 34 — Aircraft Environment Surveillance System (AESS)

**Source note sets**
- **LEVEL I** — `23402c6a-ATA_34_Navigation.pdf`, doc pages 32–48: "A/C ENVIRONMENT SURVEILLANCE SYSTEM PRES. (1)" (pp. 32–45) and "NAVIGATION SYSTEMS MAINTENANCE (1)" (pp. 46–47). Ref L4I07141, Apr 19 2007, Maintenance Course T1+T2 (RR/Metric), Level I – ATA 34 Navigation.
- **LEVEL 2&3** — `182f4b62-ATA_34_Navigation.pdf`, doc pages 104–131: "AICRAFT ENVIRONMENT SURVEILLANCE SYSTEM DESCRIPTION (3)" (pp. 104–125) and "SURVEILLANCE SYSTEM MAINTENANCE (3)" (pp. 126–131). Ref LJR11461, Nov 21 2011 / 01 AUG 2013, Mechanical & Avionics Course T1+T2 (LVL 2&3) (RR Trent 900).

Scope: AESS only (WXR/PWS, TAWS, TCAS, ATC XPDR) and its maintenance. ADIRS and radio nav aids excluded.

---

## 0.1 COMPONENTS

| id | Full name | Acronym | Type | Quantity / identifier (quoted from notes) | Ratings / frequencies / location as stated |
|---|---|---|---|---|---|
| AESU1 / AESU2 | Aircraft Environment Surveillance Unit | AESU | computer/unit | "2 identical Aircraft Environment Surveillance Units (AESUs)" (L1 p.34; L2&3 p.104). "The AESS has two AESUs." (p.108) | Located "in the avionics bay" (L1 p.44; L2&3 p.106). Each AESU has **five modules**: WXR/PWS module, TAWS module, TCAS module, XPDR module, and an **Input/Output and alert priority management module** (p.108). "Each AESU has two power supply units, one by group, supplied with 115 VAC" (p.108). Power buses per p.125 diagram: AESU1 [WXR/TAWS] PSU ← 115 VAC ESS BUS; AESU1 [TCAS/XPDR] PSU ← 115 VAC EMER BUS; AESU2 both PSUs ← 115 VAC BUS 4. |
| — (module) | Weather Radar / Predictive Windshear module | WXR/PWS | integrated function (module in AESU) | 1 per AESU | Grouped with TAWS as the **[WXR/TAWS] group** (p.108). Carries "WXR/PWS/TURBULENCE" (p.105 diagram). |
| — (module) | Terrain Awareness and Warning System module | TAWS | integrated function (module in AESU) | 1 per AESU | Grouped with WXR/PWS as **[WXR/TAWS] group** (p.108). Carries "TERRAIN COLLISION" (p.105 diagram). Hosts / extracts from the **TERRAIN DATA BASE** (pp.43, 110 diagrams). |
| — (module) | Traffic alert and Collision Avoidance System module | TCAS | integrated function (module in AESU) | 1 per AESU | Grouped with XPDR as the **[TCAS/XPDR] group** (p.108). Carries "AIRBORNE COLLISION" (p.105 diagram). |
| — (module) | Air Traffic Control transponder module | ATC XPDR | integrated function (module in AESU) | 1 per AESU | Grouped with TCAS as **[TCAS/XPDR] group** (p.108). Carries "SURVEILLANCE" (p.105 diagram). Operates in an "Air Traffic Control Radar Beacon (ATCRB) System environment" (p.112). |
| IOM | Input/Output and alert priority management module | I/O module / IOM | controller (module in AESU) | 1 per AESU | "the primary A/C signal interface of the AESU" (p.108); does the interface with the aircraft systems, the AESS control panel and the other AESU; hosts the **centralized alert management function** on the **master** AESU (p.109); "does the BITE of the whole system" (p.109). |
| ANT1–ANT4 | Combined Mode S transponder and TCAS antennae | Mode S/TCAS antennae | antenna | "4 identical combined Mode S transponder and Traffic alert and Collision Avoidance System (TCAS) antennae" (L1 p.34; L2&3 p.104). "There are four combined Mode S/TCAS antennae" (p.114) | "located at the top and bottom of the fuselage" (L1 p.44; L2&3 p.106). "They operate at a frequency of 1030 MHz for interrogation signals and at a frequency of 1090 MHz for reply signals." "Each AESU is connected to one top antenna and one bottom antenna through a coaxial cable." (p.114). Diagram p.110 shows the four antennae with a FLIGHT/GROUND discrete. |
| WXR-ANT | Weather Radar Antenna (weather flat-plate antenna) | WXR antenna | antenna | "1 Weather Radar Antenna" (L1 p.34; L2&3 p.104) | "installed in the radome. It is composed of 2 Radar Transceiver Units (RTUs), a drive unit and a flat-plate antenna" (L1 p.44; L2&3 p.106). "30 inch flat plate antenna, with ±80° azimuth and ±15° tilt envelope. 45° polarization" (p.118). Accessible through the inside of the Nose Landing Gear (NLG) compartment; assembly weighs **13.64 kg** (L1 p.46). |
| DRIVE | Antenna drive unit (antenna dual drive) | drive unit | unit | "an antenna drive" (L2&3 p.104) | "Dual azimuth & elevation motors: operation & dispatch possible with failed motor. Direct drive motors (no gearing) for reliability." (p.118). Fed **28 VDC** (p.110 diagram). |
| RTU1 / RTU2 | Radar Transceiver Units | RTUs | unit | "2 Radar Transceiver Units (RTUs)" (L2&3 p.104, p.106) | "installed in the drive assembly: a short waveguide (integrated in the drive) requires less power and maintenance" (p.118). Fed **200 VDC** (p.110 diagram). |
| RF-SW | Radar RF switch | RF switch | unit | 1 (p.110 diagram, "RF SWITCH") | "Dual system (including the antenna drive), with the exception of the antenna and RF switch that connects it to either side" (p.118). Its failure is a downgraded-mode cause (p.124). |
| AESS-CP | Aircraft Environment Surveillance System (AESS) Control Panel | AESS CP | control panel | "1 AESS Control Panel" (L1 p.34; L2&3 p.104) | Panel identifier **"(3SE)"** (L1 pp.35–45 diagrams). "located on the pedestal" (L1 p.44; L2&3 p.106). Fed **28 VDC** (p.110 diagram). Carries CAPT WXR block (ELEVN, GAIN, VD AZIM), F/O WXR block (ELEVN, GAIN, VD AZIM), TCAS block (ABV, BLW, TA ONLY), G/S MODE key, and the reconfiguration P/BSWs WXR TAWS SYS1/SYS2 and XPDR TCAS SYS1/SYS2. |
| EFIS-CP | EFIS control panels | EFIS CPs | control panel | 2 implied (CAPT & F/O; "The EFIS control panels select the different modes of view on the NDs", p.104) | Carry the **WX**, **TERR**, **TRAF** P/BSWs (pp.110, 115, 120, 123 diagrams). |
| RMP1 / RMP2 | Radio and Audio Management Panels | RMPs | control panel | "RMP 1 & 2" (L1 p.36); "the RMP1 and the RMP2" (p.112) | "can control some ATC transponder functions" (p.104). Interface to each AESU **through an ARINC 429 bus** (p.112). SQuaWK page with SQWK code field and IDENT (L1 p.37; p.113). |
| KCCU | Keyboard and Cursor Control Units | KCCUs | control panel | "Keyboard and Cursor Control Units (KCCUs)" (p.104) | "interface on the surveillance pages on the MFDs" (p.104). Carry a **SURV** key (pp.113, 115, 120, 123). Used to enter the squawk code in the field below the SQWK indication (p.112). |
| ECAM-CP | ECAM Control Panel | ECAM CP | control panel | 1 (p.109, p.110 diagram) | Carries the **EMERGENCY CANCEL momentary switch**; "In order to cancel an aural alert, on crew request, each AESU is interfaced with the ECAM CP … through an AESU input discrete" (p.109). |
| RESET-1231VM / RESET-1222VM | AESS reset switches | AESS RESET SW | control (maintenance) | 2 panels identified **1231VM** and **1222VM** (p.125 diagram) | "AESS RESET SWITCHES" shown on the two reset panels. |
| PFD | Primary Flight Display | PFD | display | Part of CDS (pp.35, 105 diagrams) | Shows TCAS sector displays on the vertical speed scale; "safe vertical speed" scale (pp.109, 116, 117). |
| ND | Navigation Display | ND | display | Part of CDS; "Independent CAPT & F/O displays" (p.118) | Weather / terrain / traffic background displays; horizontal view; ND Rose Mode (pp.117–120, 123). |
| VD | Vertical Display | VD | display | referenced (L1 p.40; p.118) | "Vertical 'profile' views (on the VD) are a planar 'cut' through the buffer, at an azimuth equal to the aircraft's track angle, or at a manually selected azimuth angle." (p.118) |
| MFD | Multi-Function Display | MFD | display / control | Part of CDS | Hosts the **SURV** pages: "SURVeillance/CONTROL page" (L1 p.36), "SURV/CONTROLS" and "STATUS & SWITCHING" tabs (pp.113, 115, 120, 123, 125 diagrams). |
| CDS | Control and Display System | CDS | display system | 1 | "The warnings and data computed by the AESUs are displayed on the Control and Display System (CDS)" (p.104). Comprises PFD, ND, MFD (p.105 diagram). |
| FWS / FWC | Flight Warning System / Flight Warning Computer | FWS / FWC | user system | FWS hosted in **CPIOMs-C** with the FCU back-up (p.110 diagram) | "The aural warnings generated by the AESS, directly or via Flight Warning System (FWS), are sent to the Radio and Audio Integrating Management System (RAIMS)" (p.104). IOM works "in coordination with the Flight Warning Computer (FWC)" to send authorized audio (p.109). BITE reported to OMS and FWS through the ADCN (p.109). |
| RAIMS / RAMS | Radio and Audio Integrating Management System (L2&3) / Radio and Audio Management System (L1) | RAIMS / RAMS | user system | 1 | Receives the AESS aural warnings (L1 p.34 calls it RAMS; L2&3 p.104 calls it RAIMS). |
| AMU | Audio Management Units | AMUs | unit | plural, "the AMUs" (p.109) | "Each AESU has an interface with the AMUs through an analog audio output. This interface is used to send aural alerts through the loudspeakers." (p.109) |
| LOUDSPEAKERS | Cockpit loudspeakers | — | output | 2 shown either side of the AMUs (p.110 diagram) | Aural alert output path. |
| CPIOM-D1 | Core Processing Input/Output Module D1 hosting the ATC application | CPIOM-D1 / ATC | computer | 1 | "the Air Traffic Control (ATC) application, hosted on the Core Processing Input/Output Module D1 (CPIOM-D1), through the ADCN. The ATC application receives the TCAS status information and the Mode S address through software pin-programming." (p.108) |
| ADCN | Avionics Data Communication Network | ADCN | data network | 1 | The bus carrying nearly every AESS interface (pp.108–110). |
| IOM-A | Input/Output Module A | IOM-A | interface unit | 1 (p.110 diagram) | Carries **RADIO HEIGHT DATA** from the RAs into the ADCN. |
| ADIRU | Air Data and Inertial Reference Units | ADIRUs | source system | plural (p.109, p.110 diagram) | Supplies ADR, IR, GPIRS, GPS data (see 0.2). |
| RA | Radio Altimeter transceivers | RAs | source (sensor) | "each of the **three** Radio Altimeter (RA) transceivers" (p.109) | Radio height above ground for TAWS terrain proximity surveillance. |
| MMR1 / MMR2 | Multi-Mode Receiver | MMRs | source system | "MMR1 and MMR2" (p.109) | LOC / G/S deviation, approach parameters, status. |
| FMS | Flight Management System | FMS | source system | 1 interface per AESU (p.108) | FMS raw data, FMS selection source, vertical display parameters, FMS flight plan. |
| PRIM / FCGU | PRIMary systems / Flight Control and Guidance Units | PRIMs / FCGUs | source & user system | "the two Flight Control and Guidance Units (FCGUs) included in the **three** PRIMary systems (PRIMs)" (p.109) | AFS data in / TCAS escape-manoeuvre orders out. |
| EEC | Engine Electronic Controller | EECs | source system | plural (p.109) | "Engine running" and "Engine at takeoff power" discretes. |
| SFCC | Slat Flap Control Computer | SFCCs | source system | shown on p.110 diagram | Supplies **FLAP POSITION** to the ADCN. |
| LGERS | Landing Gear Extension and Retraction System | LGERS | source system | shown on p.110 diagram | Supplies **LANDING GEAR STATUS**. |
| DME | Distance Measuring Equipment | DMEs | interfacing system | shown on p.110 diagram | Receives the **SUPPRESSOR PULSE** from the AESU. |
| OMS | Onboard Maintenance System | OMS | maintenance system | 1 | Receives BITE from the IOM through the ADCN (p.109). Tests launched "from the OMS HMI (using the OMT, OIT or PMAT)" (p.126). |
| CMS | Central Maintenance System | CMS | maintenance system | 1 | "Only the Master AESU communicates with the CMS." (p.126) |
| CDAM / SCI | Centralized Data Acquisition Module / Secure Communication Interface | CDAM / SCIs | data | shown p.110 diagram (AESS STATUS to CDAM; SCIs on the OPEN WORLD side of the AVIONICS WORLD / OPEN WORLD boundary) | Carries AESS STATUS out of the avionics world. |

---

## 0.2 TOPOLOGY

### Antenna / RF paths
| From | Via | To |
|---|---|---|
| 4 combined Mode S/TCAS antennae (top & bottom of fuselage) | coaxial cable — "Each AESU is connected to one top antenna and one bottom antenna" | AESU1 and AESU2 (TCAS module and XPDR module) |
| Weather flat-plate antenna (radome) | antenna drive unit + RTU1/RTU2 + RF SWITCH ("connects it to either side") | AESU1 or AESU2 WXR/PWS module |
| AESU (WXR/PWS module) | "WEATHER RADAR CONTROL AND MONITORING" line | RTU / drive unit assembly |
| AESU | SUPPRESSOR PULSE | DMEs |
| ATC ground station / TCAS-equipped A/C | 1030 MHz interrogation | Mode S/TCAS antennae → AESU XPDR |
| AESU XPDR | 1090 MHz reply | Mode S/TCAS antennae → ATC ground station / interrogating A/C |
| AESU TCAS | 1030 MHz interrogation via Mode S/TCAS antennae | intruder A/C transponders (Mode C and Mode S) |

### Data inputs to the AESUs (all via ADCN unless noted)
| From | Via | To | Data (as named in the notes) |
|---|---|---|---|
| FMS | ADCN | each AESU | FMS raw data (navigation data, FMS selection source, vertical display parameters); the FMS flight plan for the horizontal- and vertical-display windows of the ND |
| ADIRUs | ADCN | each AESU | Air Data Reference (ADR) — speed, altitude, temperature; Inertial Reference (IR) — heading, attitude, inertial vertical speed; GPIRS; GPS |
| 3 Radio Altimeter transceivers | **IOM-A** → ADCN ("RADIO HEIGHT DATA") | each AESU | radio height above the ground, for TAWS terrain-proximity surveillance |
| MMR1, MMR2 | ADCN ("LOC, G/S DEVIATION") | each AESU | horizontal and vertical deviations (GLIDE/LOC); approach parameters — runway heading, MMR mode; status information |
| PRIMs (2 FCGUs in 3 PRIMs) | ADCN ("AFS DATA / AFS PART / AP/FD") | each AESU | "AP Master Computer" (PRIM source selection), "Altitude selected", "AP engaged" |
| EECs | ADCN ("ENGINE DATA") | each AESU | "Engine running" (auto-start WXR), "Engine at takeoff power" (auto-start PWS) |
| SFCCs | ADCN | AESU | FLAP POSITION |
| LGERS | ADCN | AESU | LANDING GEAR STATUS |
| Mode S/TCAS antennae discrete | direct | AESU | FLIGHT/GROUND |
| AESS control panel | direct, 28 VDC panel ("AESS MODE CONTROL (WXR, TAWS, TCAS)") | AESU | mode & reconfiguration commands |
| RMP1, RMP2 | **ARINC 429 bus** | each AESU | SQWK code entry / change; IDENT activation ("XPDR CODE MFD/RMP SYNCHRONIZATION") |
| KCCUs → MFD SURV page | ADCN | AESU | all SURV/CONTROLS selections, SQWK code entry |
| EFIS control panels | "AESS MODE SYNCHRONIZATION" | AESU | WX / TERR / TRAF selection |
| ECAM CP EMERGENCY CANCEL | AESU input **discrete** | each AESU | aural alert cancel |
| Terrain data base | internal to AESU | TAWS module (and WXR surveillance function, which "also uses this information") | local topographic terrain data |

### Outputs from the AESUs
| From | Via | To | Data |
|---|---|---|---|
| Master AESU I/O & alert priority module | ADCN | PFDs | TCAS vertical-speed sector display / "safe vertical speed" scale; AESS messages linked to detected threats |
| Master AESU I/O & alert priority module | ADCN | NDs | WXR background, TERR background, TCAS intruder symbols and information; horizontal & vertical profile terrain display; pop-up on threat detection |
| Master AESU | ADCN | MFDs (SURV pages) | function status, controls, STATUS & SWITCHING |
| Non-Master AESU | ADCN / inter-AESU link | Master AESU **only** | surveillance data from the function groups it hosts |
| Each AESU | **analog audio output** | AMUs → loudspeakers | aural alerts |
| Master AESU I/O module (with FWC) | — | A/C audio system | "authorized audio" |
| AESU | ADCN | CPIOM-D1 ATC application | "TCAS STATUS, MODES S ADDRESS" |
| AESU TCAS | ADCN | PRIM | request to automatically engage the Flight Directors (manual flight); data to compute and perform an automatic escape manoeuvre (auto flight) |
| AESU I/O module (BITE) | ADCN | OMS and FWS | system failures |
| AESU | — | CDAM → (SCIs, open world) | AESS STATUS |
| AESU | — | RMPs | XPDR code MFD/RMP synchronisation |

### Power
| From | To |
|---|---|
| 115 VAC ESS BUS | AESU1 PSU for the [WXR/TAWS] group |
| 115 VAC EMER BUS | AESU1 PSU for the [TCAS/XPDR] group |
| 115 VAC BUS 4 | AESU2 PSU (both groups) |
| 200 VDC | RTUs |
| 28 VDC | antenna drive unit; AESS control panel |

---

## 0.3 CONTROLS

### AESS Control Panel (3SE), on the pedestal
| Control | Positions / keys | Command | Indication |
|---|---|---|---|
| WXR **ELEVN** selector knob (CAPT, and F/O) | rotary DN↔UP; **pushed in = automatic**, **pulled = manual** | Manual mode: "zero-thickness planar views, selected from zero to 60000 ft absolute altitude (MSL) in 1000 ft. increments. If a pin-programming option is activated, it can be pulled again, for the TILT view: fan shaped, zero thickness at selected angle." | "The mode and value are annotated on the ND." |
| WXR **GAIN** selector knob (CAPT, and F/O) | rotary − ↔ +; pushed in = auto, pulled = manual | "display gain value is adjusted (- /+) for weather analysis" | mode and value annotated on ND |
| WXR **VD AZIM** selector knob (CAPT, and F/O) | rotary L ↔ R; pushed in = auto, pulled = manual | "zero thickness, vertical profile view along selected (left or right) azimuth angle" | "represented by a white line on the ND. The VD shows a 'VIEW ALONG AZIM xxx' legend, an 'eye' symbol and a grey background outside the aircraft track." |
| TCAS **ABV** key | push (on/off) | "'ABV' key for above mode activation" — traffic display limits −2700 ft to +9000 ft from own A/C | ND message "TA ONLY ABV" when applicable |
| TCAS **BLW** key | push (on/off) | "'BLW' key for below mode activation" — traffic display limits −9000 ft to +2700 ft | ND message "TA ONLY BLW" when applicable |
| TCAS **TA ONLY** key | push | "'TA ONLY' key for Traffic Advisory (TA) mode display activation" | ND message "TA ONLY" |
| (TCAS automatic mode) | no dedicated key | "The automatic mode is activated when the 'ABV' key and 'BLW' key are off." | AUTO shown on MFD SURV page |
| **G/S MODE** key | push (inhibit) | "the 'G/S MODE' key is used to inhibit the corresponding visual and aural alert" (TAWS) | G/S MODE OFF shown on panel / MFD |
| **WXR TAWS** reconfiguration P/BSW | **SYS 1** / **SYS 2** | Selects which AESU hosts the [WXR/TAWS] function group; the AESU with the WXR/TAWS group activated is the **Master AESU** | green bar legend on selected side |
| **XPDR TCAS** reconfiguration P/BSW | **SYS 1** / **SYS 2** | Selects which AESU hosts the [TCAS/XPDR] function group | green bar legend on selected side |

### EFIS Control Panel
| Control | Positions | Command |
|---|---|---|
| **WX** P/B | push on/off | Weather radar background on ND. On the ground, "the weather radar function operates automatically when at least one engine starts **and if** the CAPT (or F/O) EFIS 'WX' key is pushed." |
| **TERR** P/B | push on/off | "the 'TERR' P/B is used to select the terrain background on ND" |
| **TRAF** P/B | push on/off | "On the EFIS control panel the 'TRAF' key is used to display the intruders on ND." |

### MFD SURV page — CONTROLS tab (reached via KCCU **SURV** key)
| Block | Field | Positions | Command |
|---|---|---|---|
| XPDR | **SQWK** | 4-digit code field (examples shown: 2000, 2100) | "The crew enters or changes the XPDR code (squawk code) in the field below the SQWK indication, through the KCCU." |
| XPDR | **IDENT** | push | activation of the identification (IDENT) function |
| XPDR | mode | **AUTO** / **ON** / **STBY** | AUTO: "the XPDR function does not transmit automatic replies (Modes A and C) when the A/C is on the ground". ON: "can send automatic reply when the A/C is in flight or on the ground". STBY: "sends no replies". |
| XPDR | **ALT RPTG** | **ON** / **OFF** | "When it is set to OFF, the XPDR function does not transmit the altitude information." |
| TCAS | mode | **TA/RA** / **TA ONLY** / **STBY** | TA/RA = TA and RA display; TA ONLY = TA only; "In 'STBY' mode, the surveillance and advisory functions are not available. No traffic display is shown on the NDs and no resolution advisory can be shown on the PFDs either." |
| TCAS | scanning | **AUTO** / **ABV** / **BLW** | same three scanning modes as the AESS CP keys |
| WXR | **TILT/ELEVN** | **AUTO** / **ELEVN** / **TILT** | selects automatic, elevation or tilt view |
| WXR | **GAIN** | **AUTO** / **MAN** | gain mode |
| WXR | **MODE** | **WX** / **MAP** | weather or ground-mapping display mode |
| WXR | **WX VD** ("WX ON VD") | **AUTO** / **OFF** | weather on the vertical display |
| WXR | **TURB** | **AUTO** / **OFF** | turbulence detection |
| WXR | **PRED W/S** | **AUTO** / **OFF** | predictive windshear |
| WXR | (WXR) | **AUTO** / **OFF** | weather radar function |
| TAWS | **TERR SYS** | **ON** / **OFF** | terrain system |
| TAWS | **GPWS SYS** | **ON** / **OFF** | basic ground-proximity warning system |
| TAWS | **G/S MODE** | **ON** / **OFF** | glideslope alert mode |
| TAWS | **FLAP MODE** | **ON** / **OFF** | flap-configuration alert mode |
| SURV | **DEFAULT SETTINGS** | push | "The MFD AESS CONTROLS page 'DEFAULT SETTINGS' button sets all modes to WX and AUTO." |
| — | **CLEAR INFO** | push (L1 p.37 panel) | (function not stated in the notes — see 0.8) |

### MFD SURV page — STATUS & SWITCHING tab
Shows, per p.125 diagram: WX DISPLAY 1 / WX DISPLAY 2, TURB 1 / TURB 2, PRED W/S 1 / PRED W/S 2 (WXR block); TERR SYS 1 / TERR SYS 2, GPWS 1 / GPWS 2 (TAWS block); "TAWS: IN USE" SYS1/SYS2 selector; XPDR 1 / XPDR 2, TCAS 1 / TCAS 2. Used to select the Master AESU as an alternative to the AESS control panel.

### RMP — SQWK page
| Control | Command |
|---|---|
| **SQWK** line key | Opens the SQuaWK page (keys: VHF, HF, TEL, SQWK, MENU, NAV) |
| SQWK code field | "transmission of the new-entered transponder code, 'SQWK' code, to each AESU" |
| **IDENT** | "activation of the identification (IDENT) function" |

### Other
| Control | Command |
|---|---|
| ECAM CP **EMERGENCY CANCEL** momentary switch | cancels an AESS aural alert, via an AESU input discrete |
| **AESS RESET SWITCHES** on panels **1231VM** and **1222VM** | AESS reset (maintenance) |
| KCCU **SURV** key | calls the MFD surveillance pages |
| OMS HMI (OMT / OIT / PMAT) | launches the AESS interactive tests |

---

## 0.4 LOGIC (IF/THEN, with priority order)

### L1 — Master / Non-Master determination (priority 1, governs everything else)
1. IF the [WXR/TAWS] function group is activated in AESU *n* (by the AESS CP "WXR TAWS SYS n" P/BSW or the MFD "Status & Switching" page) THEN AESU *n* is the **Master AESU**.
   - "The master AESU is the one with the WXR/TWS function group activated on the AESS control panel or on the 'Status & Switching' page of the 'SURV' menu on the MFDs."
2. IF an AESU is Master THEN it **is the only AESU that sends data to the A/C system**, and it is the only AESU that communicates with the CMS.
3. IF an AESU is Non-Master THEN it "sends data to the Master AESU only".
4. IF the WXR function is available THEN "The Master AESU is the one where the WXR function is available, and thus, the WXR/TAWS function group must be selected in this AESU."
5. IF the same surveillance function/function group is unavailable in BOTH AESUs THEN "The Master AESU is the one where the WXR/TAWS function group is activated. This AESU remains the Master even if the WXR function is not available in the two AESUs."

### L2 — AESS mode of operation (three modes)
6. **Normal mode**: IF both function groups are activated in one and the same AESU THEN that AESU is Master and "The Master AESU does all the surveillance functions."
7. **Mixed mode**: IF both function groups are available but one group is activated in one AESU and the other group in the other AESU THEN mixed mode. Example given: "AESU 1 (TAWS/WXR): MASTER; AESU 2 (XPDR/TCAS): NO-MASTER, send XPDR/TCAS data to AESU 1."
8. **Downgraded mode**: IF the weather radar antenna **or** the radar RF switch is defective, **OR** the system has a minimum of two faults, one after the other THEN downgraded mode. Two types:
   - 8a. A surveillance function in one group is not available in an AESU **and** the other function of the same group is not available in the other AESU. THEN "The AESU where a surveillance function is not available receives the related data from the other AESU. Thus, the AESS can do all the surveillance functions."
   - 8b. The same surveillance function/function group is not available in the two AESUs. THEN "The AESS cannot do the surveillance related to the function/group that is not available, but it can do the functions available."
9. IF a failure occurs THEN "the system may be reconfigured using the AESS control panel thanks to the redundancy between the 2 AESUs."

### L3 — Alert priority management (the AESS's own priority engine)
10. "Visual alerts and audio requests are sent from the AESU function module to the **centralized alert management function** hosted on the I/O module and alert priority Management of the **(master) AESU**."
11. THEN that I/O module "sends the visual alerts via the ADCN bus to the cockpit displays", and, "in coordination with the Flight Warning Computer (FWC), send authorized audio to the A/C audio system."
12. IF the crew presses ECAM CP EMERGENCY CANCEL THEN the aural alert is cancelled (via the AESU input discrete).
> The notes state that a centralized priority management exists and that it arbitrates the audio, but they **do not publish the ranking between WXR/PWS, TAWS, TCAS and XPDR alerts** — see 0.8.

### L4 — Automatic pop-up on the ND
13. IF an AESS function detects a threat THEN "even if it is not selected for display on the ND, its display will automatically pop up on the ND, **overriding the selection made by the crew**."

### L5 — TCAS logic
14. The TCAS "does an active surveillance of the air traffic to track A/C with Mode C and Mode S transponders", sending 1030 MHz interrogations and receiving range, bearing, altitude, A/C Mode S address.
15. Detection volume: "The AESU detects an intruder A/C that flies in a volume of 40 NM to 100 NM around the A/C."
16. Intruder categorisation (in this order of increasing threat):
    - **Other traffic**: "from plus or minus 1200 ft to plus or minus 9900 ft"; on the ND "no collision threat, closer than 30 Nm"; displayed as a hollow (unfilled) diamond.
    - **Proximate (PA)**: "altitude difference with the TCAS A/C less than 1200 ft and their ranges are within 6 NM"; "no collision threat, closer than 6 Nm in lateral and +/- 1200 ft in vertical"; solid white diamond.
    - **TA (Traffic Advisory)**: "A/C is near the TCAS A/C but is not an immediate threat" / "potential collision threat". THEN: intruder position on ND **and aural message**; amber filled circle.
    - **RA (Resolution Advisory)**: "A/C is near the TCAS A/C and is an immediate threat" / "real collision threat". THEN: intruder position on ND, **aural message and avoidance manoeuvre orders on PFD**; red filled square.
17. IF an RA occurs THEN "the TCAS sends to the AFS the data necessary to compute an escape maneuver. It also computes and displays on the PFDs a 'safe vertical speed' scale." Specifically, "If a risk of collision is detected, the TCAS sends to the PRIM: the request to automatically engage the Flight Directors, to guide the crew along an escape manoeuver, if the aircraft is flown manually; the data to compute and perform an automatic escape manoeuvre, if the aircraft is in auto flight. In both cases, a 'safe vertical speed' scale is shown on the PFDs."
18. IF TA ONLY mode is **not** activated THEN "the AESU sends the TA mode and Resolution Advisory (RA) display on NDs."
19. IF TCAS mode = **STBY** THEN "the surveillance and advisory functions are not available. No traffic display is shown on the NDs and no resolution advisory can be shown on the PFDs either."
20. Scanning band selection: IF ABV selected THEN display limits −2700 ft to +9000 ft. IF BLW selected THEN −9000 ft to +2700 ft. IF neither ABV nor BLW is on THEN **AUTO**: "the TCAS function selects the proper altitude band to filter the traffic depending on the flight plan and/or the vertical rate."
21. IF TRAF P/B on EFIS CP is selected THEN intruders are displayed on the ND.

### L6 — XPDR logic
22. IF mode = **AUTO** and A/C is on the ground THEN "the XPDR function does not transmit automatic replies (Modes A and C)".
23. IF mode = **ON** THEN "the XPDR function can send automatic reply when the A/C is in flight or on the ground".
24. IF mode = **STBY** THEN "the XPDR function sends no replies".
25. IF **ALT RPTG = OFF** THEN "the XPDR function does not transmit the altitude information".
26. IF an interrogation is received at 1030 MHz from the ATC ground station or from a TCAS-equipped A/C THEN the AESU "automatically replies" at 1090 MHz — "from the ATC ground station for the air traffic surveillance; from an A/C with TCAS mode S transponder, to send the traffic alert."
27. IF a new SQWK code is entered on the MFD SURV page or on an RMP SQWK page THEN the AESU synchronises the MFD and the RMP ("the AESU synchronizes the MFD and the RMP").

### L7 — TAWS logic
28. "Terrain conflict detection is done by a comparison between the A/C position and trajectory, and a worldwide database."
29. "The Master AESU uses many A/C parameters as inputs. It applies alerting algorithms to give aural and visual alerts to the crew **if the boundaries of the alerting envelope are exceeded**."
30. Alerting functional areas: basic ground-proximity warning modes; terrain awareness mode; terrain clearance floor mode; runway field clearance floor display mode; horizontal-profile terrain display; vertical-profile terrain display. (L1 p.42 lists: basic GPWS, Terrain and runway Clearance Floor (TCF), terrain/obstacle awareness alerting and warning (TAD), horizontal profile terrain display, vertical profile terrain display.)
31. IF **G/S MODE** key is pushed on the AESS CP THEN "the corresponding visual and aural alert" is inhibited.
32. Terrain display colouring is referenced to the aircraft **REF ALTITUDE**, in bands: REF ALTITUDE +2000, +1000, −250/−500, −1000, −2000 (p.123 diagram).
33. The TAWS function "extracts local topographic terrain data from the terrain database to detect the terrain threat, to make a representative terrain image. The WXR surveillance function also uses this information."

### L8 — WXR/PWS logic
34. IF at least one engine starts (EEC "Engine running") **and** the CAPT or F/O EFIS "WX" key is pushed THEN, on the ground, "the weather radar function operates automatically".
35. "In flight, it operates without conditions."
36. EEC "Engine at takeoff power" information is used "to automatically start the PWS".
37. IF DEFAULT SETTINGS is pressed on the MFD AESS CONTROLS page THEN "all modes [are set] to WX and AUTO".
38. "The 'relevant weather' display will normally follow an available FMS flight plan or flight path angle 'envelope'."
39. 3D scanning: "The radar system continuously scans the entire 3-dimensional space in front of the aircraft and stores all reflectivity data in a Volumetric Buffer. This buffer is continuously updated with reflectivity data from new scans, and data is shifted to account for aircraft movement (speed, heading, altitude). extraction and image generation display is done **once per second**."
40. "The TAWS terrain database is used to enhance ground clutter removal and MAP mode."
41. "PWS sends aural alerts." (L1 p.40)

### L9 — BITE / maintenance
42. "Finally the I/O module does the BITE of the whole system to report system failures to the Onboard Maintenance System (OMS) and Flight Warning System (FWS) through the ADCN."
43. "The Master AESU does the BITE function (System BITE) for all the AESS components. Only the Master AESU communicates with the CMS."
44. CAUTION (repeated twice): "the WXR antenna will move and a test pulse will be emitted. Ensure that the WXR antenna area is clear." — applies to the Master AESU WXR test and the Master AESU system test.

---

## 0.5 STATES

| State | Definition per notes | Displays | Aural |
|---|---|---|---|
| **Normal mode (cruise), AESU1 Master** | Both function groups activated in AESU 1; "The Master AESU does all the surveillance functions." | MFD SURV shows SYS 1 selected for both WXR TAWS and XPDR TCAS | none |
| **Normal mode, AESU2 Master** | Same, both groups in AESU 2 ("AESU 1 OR AESU 2: MASTER") | SYS 2 selected on both P/BSWs | none |
| **Mixed mode** | "One function group is activated in one AESU while the other function group is activated in the other AESU." Example: AESU1 [TAWS/WXR] = Master; AESU2 [XPDR/TCAS] = Non-Master, sends its data to AESU1 | SYS1 on WXR TAWS, SYS2 on XPDR TCAS | unchanged |
| **Downgraded mode type 1** | A function of a group unavailable in one AESU and the other function of the same group unavailable in the other AESU. "the AESS can do all the surveillance functions." | Status & Switching page shows the unavailable items | unchanged |
| **Downgraded mode type 2** | The same function/group unavailable in both AESUs. "The AESS cannot do the surveillance related to the function/group that is not available, but it can do the functions available." Example given: "First failure: AESU 1 is not available. Second failure: WXR/TAWS is not available in AESU 2. AESU 2: MASTER (although the WXR is not available)" | affected function absent | affected function's alerts absent |
| **Weather radar selected (WX)** | EFIS CP "WX" P/B pushed; on ground also requires ≥1 engine started | WXR background on ND (and on VD if WX VD = AUTO); "WXR" legend on ND | — |
| **Ground-mapping selected (MAP)** | MFD WXR MODE = MAP | "ground mapping display mode for terrain features presentation" | — |
| **Terrain display selected (TERR)** | EFIS CP "TERR" P/B pushed | Terrain background display on ND (green/yellow/red density bands referenced to REF ALTITUDE) + vertical profile; "TERR" legend on ND | — |
| **Traffic display selected (TRAF)** | EFIS CP "TRAF" P/B pushed | TCAS intruder symbols on ND; "TRAF" legend | — |
| **TCAS AUTO / ABV / BLW band** | scanning mode selection | Traffic filtered to the stated altitude band; ND messages "TA ONLY ABV" / "TA ONLY BLW" | — |
| **TCAS TA** | Intruder is a "potential collision threat" | ND: intruder position, amber filled circle with relative altitude | "AURAL MESSAGE" (message text not given in the notes) |
| **TCAS RA** | Intruder is a "real collision threat" | ND: intruder position, red filled square; **PFD**: avoidance manoeuvre orders / TCAS sector on the vertical-speed scale and "safe vertical speed" scale | "AURAL MESSAGE" (text not given) |
| **TCAS TA ONLY** | TA ONLY key or MFD TA ONLY selected | ND message "TA ONLY"; RA display not sent to NDs | TA aurals only |
| **TCAS STBY** | MFD TCAS = STBY | ND message "TCAS STBY"; "No traffic display is shown on the NDs and no resolution advisory can be shown on the PFDs" | none |
| **Terrain caution / terrain warning** | TAWS alerting envelope boundaries exceeded | terrain display pops up on ND overriding crew selection; visual annunciations | "aural alert messages" (individual messages not named in the notes) |
| **Predictive windshear alert** | PWS detection | image displayed on ND/VD; PWS auto-started at engine takeoff power | "The PWS sends aural alerts." |
| **Turbulence detected (TURB)** | MFD TURB = AUTO | turbulence image on ND | — |
| **G/S alert inhibited** | AESS CP "G/S MODE" key pushed / MFD G/S MODE = OFF | corresponding visual alert inhibited | corresponding aural alert inhibited |
| **XPDR AUTO on ground** | mode AUTO, A/C on ground | — | — (no automatic Mode A/C replies) |
| **XPDR STBY** | mode STBY | — | no replies transmitted |
| **One AESU failed** | e.g. "First failure: AESU 1 is not available" | remaining AESU becomes/remains Master; reconfigure via AESS CP or MFD Status & Switching | functions hosted by the failed AESU unavailable |
| **Both AESUs failed** | not described in the notes | — | — (see 0.8) |

---

## 0.6 INDICATIONS

### ND
| Indication | Detail as stated |
|---|---|
| WXR background display | weather image; "WXR" legend circled on the ND (p.120). Colour scale shown green→yellow→red in the figures. |
| MAP / ground mapping | "ground mapping display mode for terrain features presentation" |
| Terrain background display | terrain image, "TERR" legend on ND; bands referenced to REF ALTITUDE +2000 / +1000 / −250, −500 / −1000 / −2000 (figure colours: red / yellow / light green / green / black; water shown cyan) |
| Vertical display / vertical profile | horizontal- and vertical-profile terrain display; "VIEW ALONG AZIM xxx" legend, an "eye" symbol, grey background outside the aircraft track; white azimuth line on the ND |
| TCAS intruder symbols | OTHER TRAFFIC = open diamond; PROXIMATE = solid white diamond; TA = amber/orange filled circle; RA = red filled square. Each with relative altitude annotation (e.g. "−15↑", "+10↓", "+05↓") |
| TCAS ND messages | **"TCAS STBY"**, **"TCAS"**, **"TA ONLY BLW"**, **"TA ONLY ABV"** (p.117 diagram) |
| Automatic pop-up | any AESS-detected threat pops its display up on the ND, overriding crew selection |

### PFD
| Indication | Detail |
|---|---|
| TCAS sector display on the vertical speed scale | "TCAS SECTOR DISPLAYS ON VERTICAL SPEED SCALE ON PFD" (p.117) |
| "safe vertical speed" scale | computed and displayed on the PFDs on an RA |
| Avoidance manoeuvre orders | "AVOIDANCE MANOEUVRE ORDERS ON PFD" for an RA |
| TCAS annunciation | "TCAS" shown in the PFD upper message area (p.117 figure) |
| Vertical speeds not allowed | "on the PFDs, vertical speeds not allowed when the intruder becomes a threat" |

### MFD SURV pages
| Indication | Detail |
|---|---|
| CONTROLS tab | live state of every XPDR / TCAS / WXR / TAWS control (green legend = selected) |
| STATUS & SWITCHING tab | WX DISPLAY 1/2, TURB 1/2, PRED W/S 1/2, TERR SYS 1/2, GPWS 1/2, "TAWS: IN USE" SYS1/SYS2, XPDR 1/2, TCAS 1/2 |
| SQWK / IDENT | current transponder code (2000 / 2100 in the figures) and IDENT status |

### Aural
| Indication | Detail |
|---|---|
| TCAS TA aural message | "AURAL MESSAGE" listed against the TA row of the TCAS DISPLAY ON ND table (wording not given) |
| TCAS RA aural message | "AURAL MESSAGE AND AVOIDANCE MANOEUVRE ORDERS ON PFD" (wording not given) |
| TAWS aural alerts | "The system gives the crew aural alert messages and visual annunciations" (wordings not given) |
| PWS aural alerts | "The PWS sends aural alerts." |
| Path | AESU analog audio output → AMUs → loudspeakers; and/or via FWS → RAIMS/RAMS. Authorised by the master AESU I/O module in coordination with the FWC. |
| Cancel | ECAM CP EMERGENCY CANCEL momentary switch |

### AESS control panel
Green bar legends on WXR TAWS SYS1/SYS2 and XPDR TCAS SYS1/SYS2 showing the selected AESU; the ABV / BLW / TA ONLY key legends.

### BITE / maintenance readouts (OMS)
| Item | Detail |
|---|---|
| Entry path | OMS HMI (OMT, OIT or PMAT) → SYSTEM REPORT / TEST → ATA SELECTION → **ATA 34 Navigation** → BITE list → **"AESS TEST"** |
| Test menu (5 items) | Master AESU module tests · AESU aural alerts · Master AESU audio test · Master AESU display test · Master AESU system test |
| Master AESU module tests (4) | Master AESU **TAWS** test · Master AESU **TCAS/XPDR** test · Master AESU **WXR** test · Master AESU **IOM** test |
| AESU aural alerts (3) | **TAWS aural alerts** · **WXR aural alerts** · **TCAS aural alerts** |
| Master AESU system test | "does a check of all the AESS functions within the master AESU" |
| CAUTION on WXR test and system test | "the WXR antenna will move and a test pulse will be emitted. Ensure that the WXR antenna area is clear." |
| BITE routing | I/O module BITE → OMS and FWS via ADCN; AESS STATUS → CDAM; only the Master AESU communicates with the CMS |
| Other BITE list entries visible (context) | ADF TEST, ADR TEST, **AESS TEST**, DME TEST, DRA TEST, IR TEST, ISIS TEST, MMR TEST, VOR TEST |

### ECAM
The notes state BITE failures are reported to the FWS through the ADCN, and that the ECAM CP is used to cancel aurals. **No specific ECAM warning/caution message texts for the AESS are given in either note set** (see 0.8).

---

## 0.7 NUMBERS — whitelist of "specified" values

| Value | What it is | Source |
|---|---|---|
| **2** | identical AESUs | L1 p.34; L2&3 p.104, p.108 |
| **5** | modules per AESU | L2&3 p.108 |
| **2** | function groups per AESU ([WXR/TAWS], [TCAS/XPDR]) | p.108 |
| **2** | power supply units per AESU, one per group | p.108 |
| **115 VAC** | AESU power supply | p.108, p.110 & p.125 diagrams |
| **200 VDC** | RTU supply | p.110 diagram |
| **28 VDC** | drive unit and AESS control panel supply | p.110 diagram |
| **1** | AESS Control Panel | L1 p.34; p.104 |
| **3SE** | AESS control panel identifier | L1 pp.35–45 diagrams |
| **1231VM**, **1222VM** | AESS reset switch panel identifiers | p.125 diagram |
| **4** | combined Mode S transponder / TCAS antennae | L1 p.34; p.104; p.114 |
| **1** top + **1** bottom antenna | connected to each AESU, via coaxial cable | p.114 |
| **1** | Weather Radar Antenna | L1 p.34; p.104 |
| **2** | Radar Transceiver Units (RTUs) | p.104, p.106 |
| **1** | antenna drive | p.104 |
| **30 inch** | flat plate antenna size | p.118 |
| **±80°** | antenna azimuth envelope | p.118 |
| **±15°** | antenna tilt envelope | p.118 |
| **45°** | antenna polarization | p.118 |
| **320 NM** | weather radar range | p.118 |
| **X-band** | weather radar band | p.118 |
| **zero to 60000 ft** | ELVN manual planar-view selection range (absolute altitude MSL) | p.118 |
| **1000 ft** | ELVN increment | p.118 |
| **once per second** | WXR extraction and image generation rate | p.118 |
| **1030 MHz** | interrogation frequency (received by XPDR; transmitted by TCAS) | p.112, p.114 |
| **1090 MHz** | reply frequency | p.112, p.114 |
| **40 NM to 100 NM** | TCAS intruder detection volume around the A/C | p.116 |
| **±1200 ft to ±9900 ft** | "other A/C" altitude band | p.116 |
| **less than 1200 ft** and **within 6 NM** | Proximate (PA) criteria | p.116 |
| **closer than 30 Nm** | "other traffic" range on ND | p.117 table |
| **closer than 6 Nm** and **+/− 1200 ft** | proximate criteria on ND | p.117 table |
| **−2700 ft to +9000 ft** | ABV traffic display limits | p.114 |
| **−9000 ft to +2700 ft** | BLW traffic display limits | p.114 |
| **REF ALTITUDE +2000 / +1000 / −250 / −500 / −1000 / −2000** | TAWS/GPWS terrain display reference altitude bands | p.123 diagram |
| **4** | TAWS modes of operation on the MFD (TERR SYS, GPWS SYS, G/S MODE, FLAP MODE) | p.122 |
| **3** | TCAS scanning modes (ABV, BLW, AUTO) | p.114 |
| **3** | AESS modes of operation (normal, mixed, downgraded) | p.124 |
| **2** | types of AESS downgraded mode | p.124 |
| **minimum of two faults** | downgraded-mode trigger | p.124 |
| **3** | WXR rotary selector knobs per side (ELEVN, GAIN, VD AZIM) | p.118 |
| **3** | Radio Altimeter transceivers | p.109 |
| **2** | Multi-Mode Receivers (MMR1, MMR2) | p.109 |
| **2** | FCGUs, included in **3** PRIMary systems | p.109 |
| **2** | RMPs (RMP1, RMP2) | p.112 |
| **CPIOM-D1** | module hosting the ATC application | p.108 |
| **ARINC 429** | RMP↔AESU bus | p.112 |
| **2000**, **2100** | example squawk codes shown on the RMP and MFD figures | L1 p.37; p.113 |
| **5 m** | minimum safety distance from the WXR antenna, in an arc of 135° | L1 p.46 |
| **135°** | arc of the radiation safety area | L1 p.46 |
| **60 m** | minimum safety distance between antenna and any refuelling operation | L1 p.46 |
| **5 m** / **90°** | minimum distance between A/C and any metallic obstacle, in an arc of 90° | L1 p.46 |
| **13.64 kg** | weather radar antenna assembly weight | L1 p.46 |
| **5** | OMS AESS interactive tests | p.126 |
| **4** | Master AESU module tests | p.128 |
| **3** | AESU aural alert tests | p.131 diagram |

Any other number displayed in the simulation must be tagged **"(assumed — illustrative)"**.

---

## 0.8 GAPS (and the conservative assumption chosen)

| # | What the simulation needs | What the notes say | Assumption to use, labelled "(assumed)" |
|---|---|---|---|
| G1 | The ranking between WXR/PWS, TAWS, TCAS and XPDR alerts | Only that a "centralized alert management function" on the master AESU arbitrates, with the FWC | Do **not** display a numeric priority. Show the arbitration as a single "alert priority management" block that queues aurals one at a time, and label the ordering used in the sim "(assumed)". |
| G2 | Whether a TAWS warning inhibits a TCAS RA aural (or vice versa) | Not stated in either set | Model **no cross-inhibition** except the ones the notes do state (G/S MODE inhibit, TA ONLY suppressing RA display, STBY suppressing all). Label any other inhibition "(assumed)". |
| G3 | Aural message wordings (e.g. "TRAFFIC TRAFFIC", "CLIMB CLIMB", "TERRAIN AHEAD", "WINDSHEAR AHEAD") | The notes name **that** aural messages exist but give **no texts** | Display a neutral label — "TCAS TA aural message (text not specified in notes)" — rather than inventing Airbus/Honeywell callouts. |
| G4 | ECAM warning/caution message texts for AESS failures | Not given | Show "ECAM message (not specified in notes)" against a failure; do not invent NAV or SURV ECAM lines. |
| G5 | TA and RA trigger criteria (tau, time-to-CPA, altitude thresholds) | Only the qualitative "not an immediate threat" / "is an immediate threat" and the display volumes | Drive TA/RA in the sim from **range and relative altitude** using the stated PA thresholds as a floor, and tag the trigger numbers "(assumed)". |
| G6 | TAWS caution vs warning envelope numbers | Only the REF ALTITUDE display bands and the list of alerting functional areas | Use the display bands for colouring only; label any caution/warning trigger threshold "(assumed)". |
| G7 | Behaviour with **both** AESUs failed | Not described | Model as: no surveillance functions, no AESS displays, no AESS aurals, BITE unavailable — tagged "(assumed)". |
| G8 | Number of EFIS control panels and MFDs | Notes say "EFIS control panels", "MFDs", "NDs" in the plural without a count | Model 2 (CAPT and F/O) — tagged "(assumed)". |
| G9 | Weather radar colour scale values (dBZ / rainfall rate) | Not given; only the green/yellow/red imagery | Use green/yellow/red qualitatively with no numeric scale. |
| G10 | Function of the MFD "CLEAR INFO" button (L1 p.37) | Shown on the panel figure, never described | Model as inert / label "(function not specified in notes)". |
| G11 | Which AESU is Master by default at power-up | Not stated | Default the sim to **AESU 1 Master, normal mode** and tag it "(assumed default)". |
| G12 | XPDR Mode A/C/S detail beyond "Modes A and C" replies | Only "automatic replies (Modes A and C)" and the Mode S address via software pin-programming | Do not model Mode S data-link content. |
| G13 | Exact routing choice between "directly" and "via FWS" for a given aural | "directly or via Flight Warning System (FWS)" — no rule given | Show both paths on the schematic; do not claim which alert takes which. |
| G14 | Turbulence (TURB) detection ranges/thresholds | Only that TURB detection exists with AUTO/OFF | Qualitative only. |
| G15 | Note-set conflict: RAMS vs RAIMS | L1 p.34 = "Radio and Audio Management System (RAMS)"; L2&3 p.104 = "Radio and Audio Integrating Management System (RAIMS)" | Prefer **RAIMS** (Level 2&3, later revision — Nov 2011/Aug 2013 vs Apr 2007); show "RAMS" as a legacy synonym in the glossary. |

---

## 0.9 LEARNING OUTCOMES (CAAS SAR-66 Cat B2, Level 2)

On completion the student will be able to:
1. **Identify** the AESS line-replaceable units and antennae — 2 AESUs, 4 combined Mode S/TCAS antennae, the weather radar antenna with its drive unit, 2 RTUs and RF switch, and the AESS control panel (3SE) — and state each one's location on the A380.
2. **Explain** how the four integrated functions (ATC XPDR, TCAS, WXR/PWS, TAWS) are distributed as two function groups ([WXR/TAWS] and [TCAS/XPDR]) across five modules per AESU, and state the role of the I/O and alert priority management module.
3. **Trace** the signal path for a given indication — from antenna or source system (ADIRS, RA, FMS, MMR, EEC), through the ADCN and the Master AESU, to the ND, PFD, MFD SURV page or the loudspeakers via the AMUs.
4. **Operate** the AESS controls — AESS CP WXR knobs, TCAS ABV/BLW/TA ONLY, G/S MODE, the two reconfiguration P/BSWs; the EFIS CP WX/TERR/TRAF keys; the MFD SURV CONTROLS page; the RMP SQWK page — and **predict** the resulting displays and transponder behaviour.
5. **Predict** the AESS configuration (normal, mixed or downgraded mode) and which AESU is Master, given a stated set of function failures, and select the correct reconfiguration on the AESS CP or the MFD Status & Switching page.
6. **Isolate** an AESS fault using the OMS interactive tests (Master AESU module tests, aural alert tests, audio/display/system tests) and **apply** the WXR antenna safety precautions (5 m / 135° arc, 60 m refuelling, 13.64 kg assembly, NLG door securing) before working on the system.

---

## 0.10 MISCONCEPTIONS the sim must expose

| # | Misconception | How the sim should break it |
|---|---|---|
| M1 | "The AESS has separate boxes for weather radar, TCAS, TAWS and the transponder." | Clicking any function must open the *same* AESU; the Inspector must show all four as modules inside one unit, grouped [WXR/TAWS] and [TCAS/XPDR]. |
| M2 | "Both AESUs feed the aircraft at the same time — it's an active/active dual system." | Only the **Master** AESU sends data to the A/C system and to the CMS; the Non-Master sends to the Master only. Moving the WXR TAWS P/BSW must visibly move the Master and re-route the arrows. |
| M3 | "Selecting SYS 2 on the XPDR TCAS P/BSW makes AESU 2 the Master." | Mastership follows the **WXR/TAWS** group only. Selecting XPDR TCAS SYS 2 alone must produce **mixed mode**, with AESU 1 still Master. |
| M4 | "If I have TERR deselected on the EFIS CP, a terrain threat will not disturb my ND." | On threat detection the display **automatically pops up, overriding the crew selection**. |
| M5 | "TCAS STBY and TA ONLY are the same thing — both just stop the RAs." | TA ONLY still shows traffic and TA aurals; **STBY** removes the surveillance and advisory functions entirely — no traffic on the ND, no RA on the PFD. |
| M6 | "The transponder always replies; AUTO and ON are the same." | In **AUTO** on the ground the XPDR sends no automatic Mode A/C replies; in **ON** it replies in flight *or* on the ground; **ALT RPTG OFF** removes the altitude even when replying. |
| M7 | "TCAS and the transponder use separate antennae." | The four antennae are **combined Mode S/TCAS**, shared by both functions, 1030 MHz out / 1090 MHz in. |

---

## 0.11 DEFINITIONS & PRECEDENCE

| Term | Definition in the notes' sense |
|---|---|
| **Surveillance (AESS sense)** | Telling the flight crew about all kinds of existing hazards external to the aircraft — weather, windshear, turbulence, airborne collision, terrain collision — by detecting the hazard, warning the crew of an imminent hazard, informing them about the A/C environment and, whenever possible, proposing an escape manoeuvre. |
| **Integrated function** | One of the four surveillance capabilities (ATC XPDR, TCAS, WXR/PWS, TAWS) carried out as a **module inside an AESU** rather than as a separate LRU; the two AESUs "integrate and carry out" all four. |
| **Function group** | A fixed pairing of two modules: **[WXR/TAWS]** and **[TCAS/XPDR]**. A group is activated as a unit in one AESU, and each group has its own power supply unit. |
| **Master AESU** | The AESU with the [WXR/TAWS] function group activated (via the AESS CP or the MFD Status & Switching page). It is the only AESU that sends data to the A/C system, hosts the centralized alert management function, does the System BITE, and communicates with the CMS. |
| **Non-Master AESU** | The other AESU; it sends its data to the Master AESU only. |
| **Normal mode** | Both function groups activated in one and the same AESU; that AESU does all the surveillance functions. |
| **Mixed mode** | Both groups available but activated in different AESUs; only the Master still sends data to the aircraft. |
| **Downgraded mode** | The WXR antenna or the radar RF switch is defective, or the system has at least two faults one after the other. Type 1: complementary function losses across the two AESUs — the AESS can still do all the surveillance functions. Type 2: the same function/group lost in both AESUs — that surveillance is lost, the rest continues. |
| **Other traffic** | Intruder from ±1200 ft to ±9900 ft; no collision threat, closer than 30 NM; shown on ND with position only. |
| **Proximate traffic (PA)** | Intruder with an altitude difference less than 1200 ft and range within 6 NM; no collision threat; shown on ND with position only. |
| **Traffic advisory (TA)** | Intruder near the TCAS A/C but **not an immediate threat** — a *potential* collision threat. Produces intruder position on the ND **and an aural message**. |
| **Resolution advisory (RA)** | Intruder near the TCAS A/C and **an immediate threat** — a *real* collision threat. Produces ND position, an aural message, and avoidance manoeuvre orders on the PFD; the TCAS sends the AFS/PRIM the data for an escape manoeuvre and displays a "safe vertical speed" scale. |
| **Terrain caution / terrain warning** | The notes do **not** use the words "caution" and "warning" as two separate TAWS alert levels. They state that TAWS "applies alerting algorithms to give aural and visual alerts to the crew if the boundaries of the alerting envelope are exceeded", and list the alerting functional areas (basic GPWS modes, terrain awareness, terrain clearance floor, runway field clearance floor, horizontal- and vertical-profile terrain display). Any two-level caution/warning split in the simulation must be tagged **"(assumed)"** — see G6. |
| **Predictive windshear (PWS)** | A detection function of the weather radar (WXR/PWS) that detects, localises and displays atmospheric disturbances ahead of the aircraft and sends aural alerts; auto-started on the EEC "engine at takeoff power" signal; selectable AUTO/OFF as "PRED W/S" on the MFD. |
| **Transponder mode (XPDR)** | AUTO — no automatic Mode A/C replies on the ground; ON — automatic replies in flight or on the ground; STBY — no replies. Independently, ALT RPTG ON/OFF governs whether altitude is transmitted. |
| **SQWK / IDENT** | SQWK = the transponder (squawk) code, entered on the MFD SURV page via the KCCU or on an RMP SQWK page, synchronised by the AESU between MFD and RMP. IDENT = the identification function, activated from either. |
| **Automatic pop-up** | On detection of a threat by an AESS function, that function's display appears on the ND even if not selected, overriding the crew's selection. |
| **Alert priority management** | The centralized function on the master AESU's I/O module that receives visual alerts and audio requests from the function modules, sends the visual alerts to the cockpit displays over the ADCN, and, with the FWC, sends authorised audio to the A/C audio system. |
| **System BITE** | The BITE done by the Master AESU for all AESS components, reported to the OMS and the FWS over the ADCN; only the Master AESU communicates with the CMS. |

### Conflicts between the two note sets, and precedence

| Item | LEVEL I (Apr 2007) | LEVEL 2&3 (Nov 2011 / Aug 2013) | Preferred | Why |
|---|---|---|---|---|
| Audio system name | "Radio and Audio Management System (**RAMS**)" | "Radio and Audio Integrating Management System (**RAIMS**)" | **RAIMS** | Later revision; keep RAMS as a synonym in the glossary. |
| Component list | 2 AESUs, 1 control panel, 4 antennae, 1 WXR antenna | Same **plus** "an antenna drive" and "2 Radar Transceiver Units (RTUs)" | **LEVEL 2&3** | More complete; L1 mentions the RTUs and drive unit only in the AESS Location text, not in the component list. |
| Main users | FWS, RAMS, CDS | **AFS**, FWS, RAIMS, CDS — and "In some situations, the TCAS sends guidance orders to the AFS." | **LEVEL 2&3** | Adds the AFS/PRIM interface that the RA logic depends on. |
| TAWS function list | basic GPWS, TCF (Terrain and runway Clearance Floor), TAD (terrain/obstacle awareness alerting and warning), horizontal profile, vertical profile | basic ground-proximity warning modes, terrain awareness mode, terrain clearance floor mode, runway field clearance floor display mode, horizontal-profile, vertical-profile | **LEVEL 2&3 for the logic wording; LEVEL I for the acronyms TCF and TAD** | Both describe the same six/five areas; L1 supplies the acronyms, L2&3 the operative naming. |
| Naming of the control page | "SURVeillance/CONTROL page", "SURVeillance/STATUS page" | "SURV/CONTROLS" page and "STATUS & SWITCHING" page | **LEVEL 2&3** | Matches the MFD screenshots in both sets. |
| Aircraft-level source list for TAWS | "Radio Altimeter (RA), ADIRS, FMS" (three main sources) | Full interface list: FMS, ATC/CPIOM-D1, RMPs, RAs (three), ADIRS, MMRs, PRIMs, EECs | **LEVEL 2&3** | Level I is a deliberate simplification. |

**General precedence rule adopted:** ratings, quantities and interface detail from **LEVEL 2&3** (later revision, greater depth); Level I used where it supplies material Level 2&3 omits — the WXR antenna safety figures (5 m / 135° / 60 m / 90° / 13.64 kg, NLG access), the TCF/TAD acronyms, and the plain-language statement of the AESS's general purpose. No numeric conflict was found between the two sets.

---

# PART B — DESIGN BRIEF

**File produced:** `aerosim_ata34_aess_surveillance.html`

## Archetype: SYSTEM

The AESS is a redundancy and arbitration problem: two identical units, five modules each, two function groups, and a Master chosen by a switch position. The engine is a master/mode solver over per-unit function availability, wrapped around the surveillance output logic. Three Explore views map onto the three things a technician must be able to reason about: the hardware, the traffic picture, and the reconfiguration rules.

## Page map

| Mode | What this topic gets |
|---|---|
| **Explore** | *Architecture* draws both AESUs with their five modules boxed into the two function groups, the MASTER badge on whichever unit holds WXR/TAWS, the non-Master's data path back to the Master, the four combined antennas and the weather radar antenna, and the users. *TCAS* compares the four intruder categories with their real symbols and criteria, plus the three scanning bands and a live outcome panel. *Reconfiguration* lays out the three modes, both downgraded types and a live function-availability grid. The right rail carries live ND and PFD/aural readouts, a working AESS control panel 3SE, the EFIS and MFD SURV controls, and a per-unit module availability table. 9-step build-up stepper. |
| **Build** | Constructor with 16 palette blocks, undo/redo, JSON export/import, a path continuity tester, three starter architectures and **eight** check-my-build targets covering the alert path, the authorised audio path, the weather radar chain and the Master-only maintenance link. |
| **Fault Lab** | 12 cases. Several are not defects at all — a TA that pops up because pop-up overrides selection, an RA suppressed by TA ONLY, a transponder silent in AUTO on the ground, a terrain alert with no aural because G/S MODE is inhibited. Nine diagnostic tests, the six-step flow, efficiency score, seeded exam mode. |
| **Learn** | 13 lesson steps, then a 12-question quiz mapped to LO1–LO6. |

## The gap the design is most careful about

The notes confirm that a centralized alert priority function exists on the Master AESU's I/O module and that it coordinates the audio with the Flight Warning Computer — but they never publish the ranking between the WXR, TAWS, TCAS and XPDR alerts, and they give no aural wording anywhere. The simulation therefore lists concurrent aurals **by source, in no ranked order**, and states the absence explicitly in the inspector, in the alert trace and in quiz question 12. Nothing is invented to fill it.

## Outcome mapping

| Lesson steps | Quiz questions | Outcome |
|---|---|---|
| 1, 2 | 1 | LO1 identify the units, modules and groups |
| 3, 4, 5 | 2, 3, 4, 5 | LO2 explain the Master rule and the three modes |
| 6 | 6, 7 | LO3 categorise an intruder and state its consequences |
| 7, 8, 9 | 8, 9, 10 | LO4 operate the TCAS and display controls |
| 10, 11 | 11 | LO5 explain the transponder and weather radar conditions |
| 12, 13 | 12 | LO6 trace the alert and maintenance paths, and state what the notes do not say |

## Misconceptions the design forces into the open

The AESU-1-is-always-master belief dies when the badge follows the WXR/TAWS pushbutton (step 3, Q2, fault f1); the separate-black-box belief dies at the five-module diagram (step 1, Q1); the deselecting-hides-the-alert belief dies at the automatic pop-up (step 9, Q10, fault f5); the TA-ONLY-equals-STBY belief dies in the side-by-side comparison (step 7, Q8, faults f6 and f7); the transponder-always-replies belief dies on the ground in AUTO (step 10, Q11, fault f8); and the one-failure-loses-half belief dies in downgraded type 1 (step 5, Q5, fault f2).
