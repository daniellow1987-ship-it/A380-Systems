# ATA 34 — Radio Navigation Aids: Phase 0 System Model (PART A)

**Aircraft:** Airbus A380 (RR Trent 900) · **Module:** Aircraft Electrical & Digital Systems
**Level:** CAAS SAR-66 Cat B2, Level 2 (Level I intro material included)
**Scope:** Radio navigation tuning, MMR (ILS / FLS / GPS / GLS / MIX LOC-VNAV), VOR/Marker, DME, ADF, Radio Altimeter (DRA), OANS. **Out of scope:** ADIRS, AESS/surveillance.

**Source note sets**
- **LEVEL I** — `23402c6a-ATA_34_Navigation.pdf`, doc pp. 12–31 (MMR Presentation (1) pp.12–17; Radio Altimeter Presentation (1) pp.18–21; Dependant Position Determining SYS Pres. (1) pp.22–27; Onboard Airport Navigation System Pres. (1) pp.28–31). Issue Apr 19, 2007.
- **LEVEL 2&3** — `182f4b62-ATA_34_Navigation.pdf`, doc pp. 40–103 (Radio Navigation Tuning Description (3) pp.40–41; Multi-Mode Receiver Description (3) pp.42–65; On-board Airport Navigation System Description (3) pp.66–73; Radio Altimeter System Description (3) pp.74–79; VOR/Marker and DME Systems Description (3) pp.80–87; Automatic Direction Finder System Description (3) pp.88–93; Radio Navigation Aids Systems Maintenance (3) pp.94–103). Issue Nov 21, 2011 / rev 01 AUG 2013.

Throughout: **(L1 p.N)** = Level I page N; **(L3 p.N)** = Level 2&3 page N. Anything marked **(assumed)** is NOT in the notes.

---

## 0.1 COMPONENTS

### Receivers / transceivers / interrogators

| id | Full name | Acronym | Type | Quantity & identifiers (quoted) | Frequencies / ratings | Location & power |
|---|---|---|---|---|---|---|
| MMR1, MMR2 | Multi-Mode Receiver | MMR | Receiver (multi-function) | "two MMR receivers" (L1 p.12); "The 2 Multi-Mode Receivers (MMRs) are part of the radio navigation aids" (L3 p.42) | Functions: ILS, FLS, GPS, GLS (optional), MIX LOC/VNAV, BITE (L3 pp.42–43) | Main avionics compartment (L1 p.17 / L3 p.45 diagram). "MMRs are supplied with 115VAC by EMERgency bus for side 1 and AC BUS 2 for side 2" (L3 p.42) |
| VOR1, VOR2 | VHF Omnidirectional Range receiver | VOR | Receiver | "two VOR receivers" (L1 p.24; L3 p.82) | Antenna receives 108 to 117.95 MHz (L3 p.82) | "The 115VAC EMER BUS supplies the VOR1 and the 115VAC NORMAL BUS 2 supplies the VOR2" (L3 p.82) |
| MKR (in VOR1) | Marker function | MKR | Receiver function | "Marker function only active within VOR1 receiver" (L1 p.24); "one Marker antenna connected to VOR1 receiver only" (L3 p.82) | MKR beacons 75 MHz (L3 p.82) | Hosted in VOR1 (no separate LRU) |
| DME1, DME2 | Distance Measuring Equipment interrogator | DME | Interrogator | "The A/C is equipped with 2 DME systems. Each system is composed of: one DME interrogator, one DME antenna" (L1 p.24); "The A/C has 2 DME systems" (L3 p.84) | "operates in the frequency range of 962 to 1213 MHz" (L3 p.84) | "The 115VAC EMER BUS supplies the DME1 and the 115VAC BUS 4 supplies the DME2" (L3 p.84) |
| ADF1, ADF2 | Automatic Direction Finder receiver (optional) | ADF | Receiver | "optional"; "The A/C might be equipped with 2 ADF systems. Each system includes: one ADF receiver, one ADF antenna" (L1 p.24); "Note that the A/C can be equipped with 1, 2 or no ADF systems" (L3 p.90) | Antennae "operate between 190 and 1750 Khz" (L3 p.90) | "The 115VAC ESSentiel BUS supplies the ADF1 and the 115VAC BUS 2 supplies the ADF2" (L3 p.90) |
| RA1, RA2, RA3 | Radio Altimeter transceiver (a.k.a. DRA in BITE menus) | RA / DRA | Transceiver | "Three RA independent systems are installed on the aircraft" (L1 p.18); "3 RA transceivers" (L1 p.20) | Transmits a frequency-modulated signal "between 4200 MHz and 4400 MHz" (L3 p.76) | "3 RA transceivers installed in the aft cargo compartment" (L1 p.20); rear cargo compartment area (L3 p.76). "RA1 and RA2 are supplied with 115VAC by the 115VAC NORMAL BUS. RA3 is supplied with 115 AC ESS BUS." (L3 p.77) |
| OANC | On-board Airport Navigation Computer | OANC | Computer (hosts OANS software + Airport Data Base) | One OANC implied ("The On-board Airport Navigation System (OANS) is hosted in the On-board Airport Navigation Computer (OANC)", L3 p.66) — quantity not stated | Hosts OANS SOFTWARE, ADB, BITE (L3 p.69) | 115 VAC BUS 4 (L3 p.69 diagram) |

### Antennae

| id | Full name | Type | Quantity (quoted) | Location (quoted) |
|---|---|---|---|---|
| GPS ANT 1, 2 | GPS antenna | Antenna (active) | "two GPS antennae" (L1 p.12); "1 active GPS antenna" per MMR system (L1 p.16; L3 p.44) | "installed on the top of the fuselage, in the A/C longitudinal axis" (L1 p.16 / L3 p.44) |
| LOC ANT | Localizer antenna | Antenna | "a common Localizer antenna" — one, shared by both MMRs (L1 p.12/16; L3 p.44) | "located in the radome" |
| G/S CAPTURE ANT | Glide-Slope capture antenna | Antenna | "one common G/S capture antenna" (L1 p.16; L3 p.44) | "located in the radome" |
| G/S TRACK ANT | Glide-Slope track antenna | Antenna | "one common G/S track antenna" (L1 p.16; L3 p.44) | "located on the nose landing gear" |
| VOR ANT | Dual VOR antenna | Antenna (dual) | "one dual VOR antenna" (L1 p.24; L3 p.82) | "installed on the top of the vertical stabilizer" (L3 p.80) |
| MKR ANT | Marker antenna | Antenna | "one Marker antenna" (L1 p.24; L3 p.82) | "at the bottom of the fuselage" (L1 p.22 / L3 p.80) |
| DME ANT 1, 2 | DME antennae | Antenna | "2 antennae" (L1 p.22); one DME antenna per system (L3 p.84) | "located at the bottom of the fuselage" (L1 p.22; L3 p.80) |
| ADF ANT | ADF antenna(e) | Antenna | "one ADF antenna" per system; 1, 2 or none (L3 p.90) | "located on the top of the fuselage" (L1 p.22; L3 p.88) |
| RA TX ANT ×3 | RA transmission antennae | Antenna | "3 transmission antennae" (L1 p.20; L3 p.76) | "installed at the bottom of the rear fuselage" (L1 p.20); "at the bottom of the fuselage on the rear cargo compartment area" (L3 p.76) |
| RA RX ANT ×3 | RA reception antennae | Antenna | "3 reception antennae" (L1 p.20; L3 p.76) | as above; "A coaxial cable connects each transceiver to each antenna" (L3 p.76) |

### Control panels, displays, data-path units

| id | Full name | Acronym | Type | Notes from the notes |
|---|---|---|---|---|
| RMP1, RMP2 | Radio and audio Management Panel | RMP | Control panel | "Each Radio Management Panel (RMP) can tune both MMRs in back-up mode" (L1 p.14). Two shown, RMP1 (CAPT) and RMP2 (F/O), joined by the **RMP DIALOG BUS (CROSS TALK)** (L3 p.41) |
| MFD (×2 shown) | Multifunction Display | MFD | Display / control | POSITION/NAVAIDS page for manual tuning; POSITION/MONITOR and POSITION/GPS pages (L1 p.26; L3 pp.40, 61) |
| KCCU CAPT, KCCU F/O | Keyboard and Cursor Control Unit | KCCU | Control | Manual tuning entry and OANS interactivity; "interfaced with the CAPT KCCU and the F/O KCCU through RS 422" (L3 p.68) |
| EFIS CP (CAPT, F/O) | EFIS Control Panel | EFIS CP | Control panel | LS P/B, VOR1/ADF2 etc. selectors, mode selector (LS/VOR/NAV/ARC/PLAN), range/ZOOM selector (L3 pp.49, 69, 93) |
| AFS CP | AFS control panel | AFS CP | Control panel | "APPR" P/B and "LOC" P/B (L3 p.46) |
| PFD, ND | Primary Flight Display / Navigation Display, part of CDS | CDS | Display | Recipients of MMR, VOR/MKR, DME, ADF, RA data |
| ISIS | Integrated Standby Instrument System | ISIS | Standby display | Receives ILS/FLS/GLS/MIX data by A429 "(back-up of the CDS)" (L3 p.46); GPS position in ISIS ND mode (L3 p.60) |
| IOM 3, IOM 4 | Input Output Module (tuning path) | IOM | Data concentrator | "each active Flight Management Computer (FMC), through the Input Output Module (IOM) automatically tunes its own side radio navigation aids" (L3 p.40). Diagram labels IOM 3 → RMP1 side, IOM 4 → RMP2 side (L3 p.41) |
| IOM-A 1…4 | Input Output Modules (data-out path) | IOM-A | Data concentrator | Send VOR/DME/ADF/RA/MMR data onto the ADCN (L3 pp.83, 85, 91, 78) |
| ADCN | Avionics Data Communication Network | ADCN | Network (AFDX) | Main bus between navigation receivers, FMS, CDS, AESS, FWS |
| AMUs | Audio Management Units | AMU | Audio | "Each VOR/DME/ADF receiver is connected to both Audio Management Units (AMUs) to give to the crew the morse audio signal identification" (L3 pp.82, 84, 90) |
| CMV | Concentrator and Multiplexer for Video | CMV | Video concentrator | OANS image to ND CAPT / ND F/O (L1 p.28; L3 pp.66, 69) |
| ADB | Airport Data Base | ADB | Database | Hosted in OANC; "2 ADB cycles embedded on the OANC" (L3 p.72) |
| PRIMs / FCGUs | PRIMary systems | PRIM | Flight control computers | Generate LAS / FT / TTI discretes to the MMR; receive RA data (L3 pp.46, 76) |
| FCDC (in CPIOM-C) | Flight Control Data Concentrator | FCDC | Application | "gives the precision approach capability to the CDS for display according to the MMRs status (relayed by the PRIMs)" (L3 p.46) |
| FWS / FWC (in CPIOM-C) | Flight Warning System / Computer | FWS/FWC | Warning | RA warnings & auto call-out; RA/MMR/GPS status (L3 pp.46, 76) |
| CMS / OMS, SCI, CDAM | Centralized Maintenance System / Onboard Maintenance System, Secure Communication Interfaces, Centralized Data Acquisition Module | CMS/OMS | Maintenance | "Each MMR has a BITE module connected to the Centralized Maintenance System (CMS)" (L3 p.42); VOR/DME/ADF/RA connect to SCIs and CDAM (L3 pp.82, 84, 90, 76) |
| LGERS | Landing Gear Extension and Retraction System | LGERS | Discrete source | Gives GND/FLT discrete to VOR, DME, ADF, RA and OANS (L3 pp.82, 84, 90, 76, 68) |
| RF RELAYS (G/S) | Radio-frequency relays for G/S antenna selection | — | RF switch | Between G/S capture & track antennae and the MMR (L3 pp.46–47) |

---

## 0.2 TOPOLOGY (from → via → to)

### Antenna → receiver
| From | Via | To |
|---|---|---|
| GPS ANTENNA 1 | coax | MMR1 (GPS function) |
| GPS ANTENNA 2 | coax | MMR2 (GPS function) |
| LOCALIZER ANTENNA (common) | coax | MMR1 and MMR2 (ILS / MIX LOC / GLS functions) |
| G/S CAPTURE ANTENNA (common) | **RF RELAY** | MMR (ILS G/S) — selected when NLG retracted |
| G/S TRACK ANTENNA (common) | **RF RELAY** | MMR (ILS G/S) — selected when NLG extended |
| DUAL VOR ANTENNA | coax | VOR1 and VOR2 |
| MARKER ANTENNA | coax | VOR1 receiver only |
| DME ANTENNA 1 / 2 | coax | DME1 / DME2 interrogator |
| ADF ANTENNA(E) | coax | ADF1 / ADF2 |
| RA transmitter antenna ×3 | coaxial cable, one per transceiver | RA1/RA2/RA3 (transmit 4200–4400 MHz FM) |
| RA receiver antenna ×3 | coaxial cable | RA1/RA2/RA3 |
| GLS ground station | LOC ANTENNA | MMR (GLS function) — pseudo-range corrections + satellite integrity + final approach segment data (L3 p.62) |

### Tuning path (auto / manual / back-up) — L3 pp.40–41
| From | Via | To |
|---|---|---|
| FMS (FMCs) | ADCN → **IOM 3** ("DATA TO PORT A") → RMP 1 ("DATA FROM FMCs") | VOR1 / DME1 / ADF1 / MMR1 — **port B** normally, via the on-side RMP |
| FMS (FMCs) | ADCN → **IOM 4** → RMP 2 | VOR2 / DME2 / ADF2 / MMR2 — **port B** via RMP2 |
| MFD POSITION/NAVAIDS (manual entry via KCCU) | ADCN → IOMs → RMPs | **port B** of the related radio navigation receivers |
| RMP 1 / RMP 2 (NAV back-up, RAD NAV P/B) | direct wiring | **port A** of own-side receivers (by-passing the IOM/FMS path) |
| Port A/B SELECTION | discrete from RMP | each receiver's port selector |
| RMP 1 ↔ RMP 2 | **RMP DIALOG BUS (CROSS TALK)** | allows an ILS back-up tuning from RMP1 or RMP2 to be sent to **both** MMR1 and MMR2 (L3 p.40) |

### Receiver output paths
| From | Via | To |
|---|---|---|
| MMR (ILS data) | A429 | PRIMs and ISIS |
| MMR (ILS/FLS/GLS/MIX data) | IOMs-A → ADCN | FMS, CDS (PFD/ND/MFD), FWS, AESS |
| MMR (ILS ground-station ident) | analog signal | AMUs (Morse code listening) |
| MMR (GPS data: PVT, UTC/date, ground speed, track angle, GPS measurement, actual & predictive integrity) | direct | the three ADIRUs |
| ADIRU | — | computes GPIRS; transmits GPS + GPIRS data to FMS, AESS, FWS |
| MMR1 (GPS data) | — | ISIS 1 and ISIS 2 — "only used if there is a loss of GPIRS data" |
| MMR1 (UTC + date) | **ARINC 429 link** | CLOCK |
| MMRs (GPS position) | — | OANS (A/C position) |
| ADIRS (present position + time) | A429 | MMRs (initialization) |
| FMS (present position) | AFDX | MMRs (initialization) |
| VOR / MKR | IOM-A → ADCN | FWC, PFDs, NDs, FMS, MFDs, KCCUs |
| VOR receiver | analog | both AMUs (Morse ident) |
| DME | IOM-A → ADCN | FWC, PFDs, NDs, FMS |
| DME | direct | AESUs (suppressor pulse path shown L3 p.85), AMUs |
| ADF | IOM-A → ADCN | FWC, NDs, MFDs |
| RA transceiver | **ARINC 429 output bus 1** (basic means) | PRIM systems — PRIM1: RA1 & RA3; PRIM2: RA2 & RA3; PRIM3: RA1 & RA2 (3rd RA via PRIM interconnections) |
| RA transceiver | **A429 output bus 2** → ADCN (and IOMs as backup if output bus 1 not available) | PFDs, AESUs/TAWS, FMS |
| RA transceiver | A429 output bus | FWC application hosted in CPIOM-C (warnings + auto call-out) |
| RA | ADCN | ECAM — "RA FAULT MESSAGES TO ECAM" |
| VOR / DME / ADF / RA / MMR | SCIs + CDAM | OMS/CMS (maintenance data; normal & interactive mode commands returned) |
| LGERS | discrete | VOR, DME, ADF, RA (GND/FLT), OANS |
| MASTER LEVER ON | discrete (own-side) | each RA transceiver — engine power ON/OFF |
| PRIMs | discretes **LAS, FT, TTI** | MMR |
| MMR | **VASC** discrete | RF relay (G/S antenna select command) |
| RF relay | **VASA** discrete | MMR (select acknowledge) |

### OANS topology — L3 pp.66–69
| From | Via | To |
|---|---|---|
| ADIRS, FMS, MMRs (A/C GPS position) | ADCN / IOM-A | OANC |
| Airport Data Base (in OANC) | — | OANS software |
| OANC | **DVI** → **CMV** | ND CAPT and ND F/O (two independent images) |
| CAPT KCCU / F/O KCCU | **RS 422** | OANC |
| FCU / EFIS CP (mode, airport range, TRUE/MAG selection) | IOM-A → ADCN | OANC |
| OANC (BITE) | CMS COMMAND / OANS INFORMATION, via SCIs | OMS |
| LGERS | GND/FLT discrete | OANC |
| OANC | — | PRIMs, for **BTV** and **ROP** display |
| OANC | — | FWS (fault + ROP warning messages) |
| ADB / OANS software | **DLCS** (Data Loading and Configuration System) | OANC (upload) |
| F/O RESET PANEL — "ARPT NAV" pushbutton | — | OANC reset |

---

## 0.3 CONTROLS

| Control | Location | Positions / actions | What it commands | Indications |
|---|---|---|---|---|
| **MFD POSITION/NAVAIDS page** | MFD, driven by KCCU | Enter IDENT / FREQUENCY / COURSE per navaid line (VOR1, VOR2, ILS/MLS…); "LIST OF DESELECTED NAVAIDS"; GPS SELECTED / DESELECTED radio buttons | Manual tuning — settings sent on **port B** of the related receivers via IOMs and RMPs | Columns IDENT, FREQUENCY, CLASS (VOR/DME, ILS/DME), **TUNING MODE = AUTO or MAN**; "TUNED FOR FMS 1 NAVIGATION"; RADIO NAVIGATION MODE; FMS1 RADIO POSITION (L1 p.27) |
| **MFD POSITION/MONITOR page** | MFD | Consultation | Shows FMS/RADIO/MIX IRS/GPIRS positions, ACCURACY HIGH, EPU, RNP, GPS PRIMARY, FREEZE POSITION, POSITION UPDATE; soft keys NAVAIDS / GPS / IRS (L1 p.15) | — |
| **MFD POSITION/GPS page** | MFD | Consultation | GPS1 / GPS2 columns | MODE, NBR OF SAT, ACCURACY, TRK, UTC, ALT, GND SPD (L3 p.61) |
| **RMP NAV page P/B ("NAV")** | RMP 1 and RMP 2 | Press to call the NAV page | Selects the radio-nav tuning page on the RMP | Page shows LS, VOR, ADF lines (L1 p.27) |
| **RMP NAV BACK-UP P/B (RAD NAV / STBY)** | RMP, lower area | STBY ↔ RAD NAV | Selects back-up tuning: RMP tunes own-side receivers directly on **port A** | On the ND, a **"B" underlined and dimmed** appears near the navaid identification (L3 p.41 callout "BACKUP TUNING") |
| **RMP rotary selector switch** | RMP | Positions **ADF 1 / ADF 2 / LS 1 / LS 2 / VOR 1 / VOR 2 / MKR** | Selects which navaid audio / line is being handled (L1 p.27) | — |
| **RMP NAV lines: ILS ► / GLS ► / MLS ►** | RMP NAV page | Select line, enter FREQ and CRS | Back-up tuning of the ILS, GLS or MLS mode of the MMR; "The tuning selection is done by the FMS, or the RMP in back up when the GLS line is selected on 'NAV' page" (L3 p.62) | Displays FREQ (e.g. 110.70 / 103.20) and CRS (L3 pp.47, 55, 63) |
| **NAV SYSTEMS AUDIO CONTROL / VOICE P/B** | RMP audio management | VOICE selected | Filters the navaid audio to voice only ("AUDIO MANAGEMENT (VOICE ONLY)" on the VOR path, L3 p.83) | — |
| **"LS" P/B** | EFIS Control Panel, each side | ON / OFF | "allows display of G/S and LOC deviation scales on relative EFIS Display Units"; deviation scales appear on the PFD when LS is ON | Green bar on the P/B; scales appear on PFD/ND |
| **"VV" P/B** | EFIS CP (next to LS) | ON/OFF | Not described in these notes — **(gap)** | — |
| **EFIS CP NAVAID selectors: VOR1 / VOR2 / ADF1 / ADF2, and CSTR/WPT/VORD/NDB/ARPT, WX/TERR/TRAF** | EFIS CP | Push | "the VOR function is selected on the EFIS control panel in order to show the VOR and DME information on the lower left and/or right corners of the NDs"; likewise ADF (L3 pp.86, 92) | VOR1/ADF2 label blocks appear in the lower corners of the ND |
| **EFIS CP mode selector** | EFIS CP | **LS / VOR / NAV / ARC / PLAN** | Selects ND mode: ROSE-LS (ILS/FLS/GLS/MIX), ROSE-VOR, NAV, ARC, PLAN. OANS map shown in PLAN, NAV, ARC (L3 p.68) | — |
| **EFIS CP range / ZOOM selector** | EFIS CP | **ZOOM, 10, 20, 40, 80, 160, 320, 640** | "The onside EFIS control panel range selector (ZOOM position) enables the display of the Airport Navigation image, on each ND" | Green ZOOM cue lit |
| **TRUE / MAG selection** | FCU | TRUE / MAG | North reference for the airport moving map (L3 p.68) | — |
| **AFS CP "APPR" P/B** | AFS control panel | Push (arm) | "arms the Autopilot / Flight Director (AP/FD) lateral and vertical approach modes" | FMA modes on PFD |
| **AFS CP "LOC" P/B** | AFS control panel | Push (arm) | "arms the AP/FD lateral approach mode only" | FMA modes on PFD |
| **KCCU (CAPT / F/O)** | Pedestal | Keyboard + trackball, cursor | Manual navaid entry on the MFD; "direct interactivity with the Airport Navigation image"; drives the OANS soft control panel | Cursor on ND |
| **OANS soft control panel — MAP DATA page** | ND interactive zone (bottom), via KCCU | RWY / TWY / STAND / OTHER radio buttons; drop-down element selector; **ADD FLAG**, **ADD CROSS**, **CENTER MAP ON …** | Map annotation, elements centring, airport elements information | Shows e.g. RWY : 14L, LENGTH : 3000 (example values) |
| **OANS soft control panel — ARPT SELECTION page** | ND | ICAO / IATA / CITY NAME radio buttons, DISPLAY AIRPORT, **ORIGIN / DEST / ALTN** keys | Airport information and selection | Airport name, ICAO/IATA, lat/long |
| **OANS soft control panel — STATUS page** | ND | **SWAP** between ACTIVE DATABASE and SECOND DATABASE | Switch between the 2 ADB cycles embedded in the OANC | ADB cycle dates, ARPT NAV DATABASE part number, "DATABASE CYCLE NOT VALID" message |
| **F/O RESET PANEL "ARPT NAV" P/B** | F/O reset panel | Push | Resets the OANC (L3 p.69) | — |
| **OMS HMI on the OMT** | Onboard Maintenance Terminal | SYSTEM REPORT / TEST → ATA 34 Navigation → select BITE → side → test | Launch interactive tests | See 0.6 |

---

## 0.4 LOGIC (IF/THEN, in priority order)

**Tuning priority (L3 pp.40–41)**
1. **IF** normal operation **THEN** each active FMC, via its IOM, automatically tunes its own-side radio navigation aids (VOR, DME, ADF, MMR) through the associated RMP. Navaid identification/frequency data come from the **navigation database**.
2. **IF** the radio navigation computers receive tuning data on **port B** from their own-side RMP **THEN** they use it (normal auto path).
3. **IF no activity is detected by the RMP on port B THEN** the port A/B selection switches and the receivers are told to listen to **port A**, by-passing the RMP.
4. **IF** the crew enters a navaid on the **MFD POSITION/NAVAIDS page THEN** manual settings are sent on **port B** via the IOMs and RMPs, and an **"M" underlined and dimmed** is displayed near the navaid identification on the NDs.
5. **IF both IOMs (IOM 3 and IOM 4) have failed THEN** the receivers can be manually tuned via the RMPs (back-up); CAPT and F/O each control their own-side receivers; an **"R" underlined and dimmed** is displayed near the navaid identification on the NDs. *(Note: the text says "R"; the p.41 illustration labels the same field "B" for BACKUP TUNING — see 0.11 conflict.)*
6. **ILS constraint:** **IF** ILS is tuned **THEN** ILS 1 and ILS 2, inside each MMR, **must be tuned on the same frequency**. An ILS back-up tuning from RMP 1 or RMP 2 is sent to **both** MMR 1 and MMR 2 via the RMP dialog busses.
7. **GLS back-up:** tuning is by FMS, or by the RMP in back-up **when the GLS line is selected on the "NAV" page**.
8. **MIX LOC/VNAV:** "tuning selection is done by the FMS, or the RMP in back up".
9. **FLS:** "The FLS function is autonomous and does not require any additional information from the ground. Thus, in this mode, **there is no need to tune the MMRs**."

**MMR mode / function selection**
- **IF** precision approach with ground ILS **THEN** ILS function: LOC + G/S deviations from the ground station.
- **IF** non-precision approach **THEN** FLS function: MMR acquires the **FLS beam** defined by FMS-supplied Anchor Point (lat, long, alt, ident), course, runway-threshold lat/long and local magnetic deviation, computed from the FMS database + ADIRS position; outputs pseudo-LOC (F-LOC) and pseudo-G/S (F-G/S).
- **IF** non-precision approach with a usable LOC **THEN** MIX LOC/VNAV: real LOC deviation from the ground station **+** pseudo-G/S from FMS data.
- **IF** GLS (optional) selected **THEN** MMR receives the GLS ground station via the **LOC antenna** plus GPS position; the GLS station supplies pseudo-range corrections, satellite integrity and final-approach-segment data; MMR computes a more accurate position than GPS raw and defines an approach "Beam", then computes pseudo-LOC and pseudo-Glide deviations.
- GPS function runs continuously (position/velocity/time to the ADIRUs) independently of the landing-mode selection.

**G/S antenna (RF relay) selection — L3 p.46**
- **IF** NLG **retracted THEN** use the **capture** antenna.
- **IF** NLG **extended THEN** use the **track** antenna.
- Selection is based on two discrete inputs — **LAS (Landing Antenna Select)** and **FT (Functional Test)** — given by the PRIMs "according to the landing gear extension status combined with the radio-altimeters data". The MMR commands its RF relay through the **VASC** discrete and receives **VASA** as acknowledgement.

**Tune/Test Inhibit — L3 p.46**
- **IF** the A/C is near the ground — "below 700 ft **and** Nose Landing Gear (NLG) extended" — **THEN** the PRIMs set the **TTI** discrete, which freezes the tuning (avoids untimely tuning change) and inhibits the MMR test.

**Approach capability / display**
- **IF** LS P/B ON on an EFIS CP **THEN** G/S and LOC deviation scales are shown on the related PFD.
- **IF** the ILS ground signals are correctly received by the MMR **THEN** the deviation symbols are shown on those scales (otherwise scales without symbols).
- The **FCDC** (in CPIOM-C) computes the **approach capability** for CDS display "according to the MMRs status (relayed by the PRIMs)".

**Marker**
- **IF** the A/C overflies a marker beacon (75 MHz) **THEN** VOR1 gives aural + visual indications: **OM in blue, MM in amber, IM in white** on the PFD.

**DME pairing**
- "The selected ground station can be of **VOR or ILS type**" — the MFD NAVAIDS page CLASS column shows **VOR/DME** or **ILS/DME**, and the PFD shows the **ILS/DME distance** in the ILS information block. *(The notes state DME pairs with a VOR- or ILS-type station but do not state the pairing algorithm — see 0.8.)*

**Radio altimeter validity / band**
- The RA measures vertical distance A/C-to-ground; "This vertical distance is **valid for user systems up to 5000 ft**".
- "The information is displayed on the PFD **from ground up to 2500 ft**" (L3 p.74); L1 p.18 says radio height is displayed on the PFD "up to 2500 ft".
- Antenna operating range: "limited to ± 30° for roll and pitch angles" — outside that the measurement is not guaranteed.
- **IF** a RA fault is detected **THEN** the RA sends its status to the FWCs and a warning message is shown on the **ECAM**.
- **IF** the A/C is in flight (LGERS / MASTER LEVER ON discretes) **THEN** the RA **interactive mode** (and RA BITE interactive function) is **inhibited**; normal mode is active in flight, interactive mode only on ground. The MASTER LEVER ON engine power ON/OFF discrete is "a complementary mean with the LGERS".
- RA data path priority: **A429 output bus 1** is "the basic means of communication" to the PRIMs; **ADCN transmission through A429 output 2 and the IOMs is used as a backup if the A429 output bus 1 is not available**.

**GPS / GPIRS**
- Each ADIRU uses MMR/GPS measurement data to compute **GPIRS**, transmits GPS and GPIRS to FMS, AESS and FWS, and gives MMR/GPS status to the FWS.
- **IF** GPIRS data are lost **THEN** the GPS data MMR1 sends to ISIS 1 and 2 are used ("these data are only used if there is a loss of GPIRS data").
- ND shows **GPS PRIMARY**, or **GPS PRIMARY LOST** (L3 p.61).

**OANS**
- Position source: OANC uses **A/C GPS position from the MMRs**, plus ADIRS and FMS data and the ADB.
- **IF** the on-side EFIS CP range selector is at **ZOOM** **THEN** the Airport Navigation image is displayed on that ND; map modes ARC, NAV, PLAN.
- **IF** on ground **THEN** the map reference point is the A/C position; in flight, the airport reference point ("for determination of the map reference point (map centered on A/C position on ground instead of airport reference point)").
- **IF** in flight **THEN** runway proximity advisory is inhibited (OANS/LGERS interface).
- **IF** the ADB cycle is out of date **THEN** "DATABASE CYCLE NOT VALID" is shown on the STATUS page; SWAP selects the other of the 2 embedded cycles.

**Ground-station audio**
- Each VOR / DME / ADF receiver feeds **both** AMUs so the crew can listen to the Morse ident of the selected station; ILS ident is sent to the AMUs as an analog signal by the MMR.

**Power-supply-driven availability (derived directly from 0.1)**
- **IF** only the EMER/ESS busses are alive **THEN** MMR1, VOR1, DME1, ADF1 and RA3 remain supplied; MMR2, VOR2, DME2, ADF2, RA1, RA2 and OANC (BUS 4) are lost.

---

## 0.5 STATES

| State | What is true | Display implication |
|---|---|---|
| **S1 — Normal auto-tuned cruise** | FMCs auto-tune own-side VOR/DME/ADF/MMR via IOM 3/4 and RMP port B; MFD TUNING MODE column = AUTO | ND: navaid ident with no M/R prefix; VOR/DME/ADF blocks in ND corners if selected on EFIS CP; GPS PRIMARY on ND |
| **S2 — Manual tuning** | Crew enters ident/frequency on MFD POSITION/NAVAIDS; sent to port B | MFD TUNING MODE = MAN; **"M" underlined and dimmed** next to the navaid ident on the NDs |
| **S3 — Back-up (NAV BACK-UP) tuning** | Both IOMs (3 and 4) failed, or loss of ADCN/FMS; CAPT and F/O tune own-side receivers from their RMPs, receivers listening on **port A** | **"R" (illustrated as "B") underlined and dimmed** next to the navaid ident on the NDs; RMP NAV page in use |
| **S4 — ILS approach, LS selected** | ILS tuned on the same frequency in both MMRs; LS P/B ON; APPR (or LOC) armed | PFD: G/S + LOC scales with magenta diamonds, magenta dagger course, ILS ident/freq/ILS-DME distance lower-left, FMA G/S + LOC, approach capability (e.g. CAT3 DUAL, DH), "ILS" message. ND ROSE/LS: ILS2 109.30, CRS 324°, ident TBN, "ILS APP", magenta LOC bar and G/S diamond |
| **S5 — FLS (non-precision) approach** | No ground ILS; MMR builds the FLS beam from FMS anchor-point data; **no tuning needed** | PFD: FMA **F-G/S / F-LOC**, F-APP + RAW, MDA; **doubled** magenta diamond indices; RWY32L, 3.0°, distance to runway datum. ND ROSE/LS: FLS1 3.0°, CRS 315°, TROC, "VOR 32L" approach type |
| **S6 — MIX LOC/VNAV approach** | Real LOC + pseudo G/S | PFD: FMA G/S and LOC, "LOC" indication left of LOC scale, "F-G/S" above the G/S scale, double-diamond F-G/S index, single-diamond LOC index. ND: "LOC/FLS1 109.30", approach type "LOC 32L" |
| **S7 — GLS approach (optional)** | GLS ground station received via LOC antenna + GPS; MMR computes pseudo LOC/Glide | PFD: "GLS" message, GLS info TOU 103.20 1.8 NM, CAT3 DUAL. ND: **GLS2 103.20**, CRS 327°, TOU, "GLS 33L", GPS PRIMARY |
| **S8 — RA inside band (≤2500 ft)** | Radio height available and displayed | Radio height in large digits at the bottom of the PFD attitude sphere (e.g. 100); auto call-outs by FWS |
| **S9 — RA above the display band** | Height >2500 ft; data still valid to user systems up to 5000 ft | No radio height on the PFD; AFS/TAWS still fed up to 5000 ft |
| **S10 — RA failed** | RA fault detected, status sent to FWCs | **RA fault message on the ECAM**; affected PRIM loses that RA source (PRIM1: RA1&3, PRIM2: RA2&3, PRIM3: RA1&2) |
| **S11 — Receiver failed (VOR/DME/ADF/MMR)** | Loss of that side's data on the ADCN | Corresponding ND/PFD field lost; BITE records the fault for the CMS; the other side unaffected |
| **S12 — GPS degraded** | GPS PRIMARY lost | ND lower part: **GPS PRIMARY LOST**; MFD POSITION/GPS shows MODE/NBR OF SAT/ACCURACY |
| **S13 — OANS active on the ND** | EFIS CP range selector at ZOOM | Airport moving map on ND (NAV/ARC/PLAN), fixed A/C symbol, cursor, soft control panel (MAP DATA / ARPT SELECTION / STATUS) |
| **S14 — Near-ground tuning frozen (TTI)** | Below 700 ft with NLG extended | Tuning frozen; MMR test inhibited |
| **S15 — Ground, interactive mode** | LGERS = GND and MASTER LEVER OFF | OMS interactive tests available (MMR/VOR/DME/ADF/DRA) |

---

## 0.6 INDICATIONS

**PFD**
- ILS/GLS/MIX information block, lower-left: station **identification, frequency, ILS-DME distance** (e.g. TBN 109.30 1.8 NM; TOU 103.20 1.8 NM).
- ILS/FLS/GLS **course** = magenta **dagger** symbol on the heading scale.
- **G/S deviation** = magenta **diamond** on the right vertical scale; **LOC deviation** = magenta diamond on the lower horizontal scale. In FLS and MIX the index is a **double** diamond for F-G/S.
- FMA (top): armed/active lateral and vertical AP/FD modes (G/S, LOC, F-G/S, F-LOC, F-APP + RAW) and the **approach capability** computed by the FCDC (e.g. CAT3 DUAL, AP1+2, 1FD2, A/THR, DH 200 / MDA 10000).
- Messages: **"ILS" / "FLS" / "GLS"** message field.
- **DME information** lower-left corner (e.g. 9.8 NM).
- **Marker**: OM (blue), MM (amber), IM (white).
- **Radio height** in large digits at the bottom of the attitude sphere, ground → 2500 ft.

**ND**
- ROSE/LS mode: ILS/FLS/GLS/MIX approach information top-right (e.g. ILS2 109.30 CRS 324° TBN; FLS1 3.0° CRS 315° TROC; GLS2 103.20 CRS 327° TOU; LOC/FLS1 109.30); approach type top-centre (ILS APP, VOR 32L, GLS 33L, LOC 32L); magenta LOC bar around the centre; magenta G/S/F-G/S diamond on the right scale; magenta dagger course pointer.
- ROSE/VOR mode: **VOR information** top-right (VOR1 117.70 CRS 010° TOU), **lateral deviation bar**, **VOR station bearing**, **selected course pointer**.
- Lower corners: **VOR/DME information** block (e.g. ▲VOR1 / TOU / 37 NM) and **ADF information** block (e.g. ADF2 / TW). Two needles give relative bearings — **single pointer = VOR1/ADF1, double pointer = VOR2/ADF2**; VOR data in **blue**, ADF data in **green**.
- Tuning-mode annunciation next to the navaid ident: **"M"** (manual) or **"R"** (back-up), underlined and dimmed.
- **GPS PRIMARY** / **GPS PRIMARY LOST** on the lower part of the ND; GPS status on the lower part of the NDs.
- OANS: airport moving map with airport name/ICAO (e.g. TOULOUSE LFBO TLS), runways, taxiways, stands, GS readout, fixed A/C symbol, cursor, flags/crosses, soft control panel.

**MFD**
- **POSITION/NAVAIDS**: IDENT, FREQUENCY, CLASS (VOR/DME, ILS/DME), **TUNING MODE (AUTO/MAN)** per navaid; RADIO NAVIGATION MODE; FMS1 RADIO POSITION; LIST OF DESELECTED NAVAIDS; GPS SELECTED/DESELECTED; ILS/MLS block.
- **POSITION/MONITOR**: ACCURACY HIGH, EPU, RNP, GPS PRIMARY, FMS1/FMS2, RADIO, MIXIRS, GPIRS, IRS1-3 and GPS1-2 positions, deviation from FMS1, FREEZE POSITION, POSITION UPDATE.
- **POSITION/GPS**: per GPS — MODE, NBR OF SAT, ACCURACY, TRK, UTC, ALT, GND SPD.

**ISIS**
- ND mode: GPS position below the rose (GPIR3 N 4815.5 / E 00332.3), GS upper-left; ILS/FLS/GLS/MIX data received by A429 as CDS back-up.

**CLOCK** — UTC and date from MMR1 by ARINC 429 (GPS selected).

**ECAM** — RA fault messages; FWS warning messages and auto call-outs; FWS shows messages linked to OANS faults and ROP warnings.

**BITE / maintenance (OMS HMI on the OMT, SYSTEM REPORT/TEST → ATA 34 Navigation)**
| BITE entry | Side selection | Tests offered |
|---|---|---|
| MMR TEST | "MMR 1", "MMR 2" | **System Test** — "checks the integrity of the MMR, all its inputs and of the switching logic of the glide antennae" |
| VOR TEST | — | **VOR 1**, **VOR 2** |
| DME TEST | — | **DME 1**, **DME 2** |
| ADF TEST (when ADF installed) | — | **ADF 1**, **ADF 2** |
| DRA TEST (radio altimeter) | "RA 1", "RA2", "RA3" | **RAMP TEST**, **SYSTEM TEST** |
Also listed in the same ATA 34 BITE menu (not in this scope): ADR TEST, AESS TEST, IR TEST, ISIS TEST, SNS TEST.
OANS: "A BITE module is hosted in OANC for the communication with CMS"; OANS HEALTH STATUS and OANS INFORMATION signals; MMR BITE module connected to the CMS.

---

## 0.7 NUMBERS — whitelist of "specified" values

| Value | Meaning | Source |
|---|---|---|
| **2** | MMR receivers | L1 p.12; L3 p.40, p.42 |
| **2** | GPS antennae (1 active GPS antenna per MMR system) | L1 p.12, p.16; L3 p.44 |
| **1** | common Localizer antenna | L1 p.12/16; L3 p.44 |
| **1** | common G/S track antenna (nose landing gear) | L1 p.16; L3 p.44 |
| **1** | common G/S capture antenna (radome) | L1 p.16; L3 p.44 |
| **2** | VOR receivers | L1 p.24; L3 p.40, p.82 |
| **1** | dual VOR antenna | L1 p.24; L3 p.82 |
| **108 to 117.95 MHz** | VOR ground-station frequency range | L3 p.82 |
| **1** | Marker antenna (connected to VOR1 receiver only) | L1 p.24; L3 p.82 |
| **75 MHz** | Marker beacon frequency | L3 p.82 |
| **2** | DME systems / DME interrogators | L1 p.24; L3 p.40, p.84 |
| **2** | DME antennae (bottom of fuselage) | L1 p.22; L3 p.80 |
| **962 to 1213 MHz** | DME operating frequency range | L3 p.84 |
| **2** (optional; **1, 2 or none**) | ADF receivers / systems | L1 p.24; L3 p.40, p.90 |
| **1** | ADF antenna per ADF system | L1 p.24; L3 p.90 |
| **190 to 1750 kHz** | ADF antenna operating range | L3 p.90 |
| **3** | RA independent systems / RA transceivers | L1 p.18, p.20 |
| **3** | RA transmission antennae | L1 p.20; L3 p.76 |
| **3** | RA reception antennae | L1 p.20; L3 p.76 |
| **4200 MHz to 4400 MHz** | RA transmitted FM signal band | L3 p.76 |
| **± 30°** | RA antenna operating range for roll and pitch | L3 p.76 |
| **2500 ft** | RA radio height displayed on the PFD (ground up to 2500 ft) | L1 p.18; L3 p.74 |
| **5000 ft** | RA vertical distance valid for user systems up to | L3 p.74 |
| **700 ft** | TTI: tuning frozen near the ground below 700 ft with NLG extended | L3 p.46 |
| **115 VAC** | Supply voltage of MMR, VOR, DME, ADF, RA, OANC | L3 pp.42, 77, 82, 84, 90, 69 |
| MMR1 = **EMER bus**, MMR2 = **AC BUS 2** | MMR power | L3 p.42 |
| VOR1 = **115VAC EMER BUS**, VOR2 = **115VAC NORMAL BUS 2** | VOR power | L3 p.82 |
| DME1 = **115VAC EMER BUS**, DME2 = **115VAC BUS 4** | DME power | L3 p.84 |
| ADF1 = **115VAC ESSentiel BUS**, ADF2 = **115VAC BUS 2** | ADF power | L3 p.90 |
| RA1, RA2 = **115VAC NORMAL BUS**; RA3 = **115 AC ESS BUS** | RA power | L3 p.77 |
| OANC = **115 VAC BUS 4** | OANS power | L3 p.69 diagram |
| **IOM 3, IOM 4** | The two tuning-path IOMs | L3 pp.40–41 |
| **IOM-A 1…4** | Data-out IOMs shown on the VOR/DME/ADF/RA/OANS diagrams | L3 pp.83, 85, 91, 78, 69 |
| **RMP 1, RMP 2** | Radio and audio Management Panels | L3 p.41 |
| **ARINC 429 / A429** | Bus type: RA output bus 1 & 2, MMR→ISIS, MMR1→CLOCK, GLS/MIX data to PRIMs & ISIS | L3 pp.46, 54, 58, 62, 76 |
| **RS 422** | OANC ↔ CAPT KCCU and F/O KCCU | L3 p.68 |
| PRIM1 = **RA1 & RA3**; PRIM2 = **RA2 & RA3**; PRIM3 = **RA1 & RA2** | RA→PRIM A429 source allocation | L3 p.78 diagram |
| **3** | ADIRUs receiving MMR GPS data | L3 p.58 |
| **ISIS 1 and 2** | Units receiving MMR1 GPS data | L3 p.58 |
| **2** | ADB cycles embedded on the OANC | L3 p.72 |
| **3** | OANS soft-control-panel pages (MAP DATA, ARPT SELECTION, STATUS) | L3 p.72 |
| **3** | OANS/ND display modes (ARC, NAV, PLAN) | L1 p.30; L3 p.68 |
| EFIS CP ranges **10, 20, 40, 80, 160, 320, 640** + **ZOOM** | Range selector positions | L1 p.31; L3 pp.67, 71 |
| **2** | Independent OANS images generated by the OANC (ND CAPT, ND F/O) | L3 p.66 |
| **2** | Needles/pointers per navaid family on the ND (single = 1, double = 2) | L3 pp.86, 92 |

**Screen-example values (illustrative only — from TTM screenshots labelled "PARAMETERS SHOWN AS EXAMPLES (NOT CONSISTENT)"; do NOT present as system specifications):** ILS2 109.30 / CRS 324° / TBN / 1.8 NM; VOR1 117.70 / CRS 010° / TOU / 37 NM; GLS2 103.20 / CRS 327° / TOU; FLS1 3.0° / CRS 315° / TROC; RWY32L 3.0°; RWY33L 3.10° 9.8 NM; DME 9.8 NM; radio height 100; DH 200 / MDA 550 / MDA 1000 / MDA 10000; QNH 1013 / 1010; GS 130 / TAS 140; ADB cycles 16MAR–13APR and 14APR–12MAY, ARPT NAV DATABASE AD23122004; RWY 14L LENGTH 3000; LFBO / TOULOUSE / TLS; GPS accuracy 100 M, 6 satellites; FMS EPU 0.20 NM, RNP 0.30 NM.

---

## 0.8 GAPS (and the conservative assumption to use)

| # | What the simulation needs | Notes status | Assumption to label "(assumed)" |
|---|---|---|---|
| G1 | ILS localizer/glide frequency band and channel spacing | **Not stated** anywhere (only VOR 108–117.95 MHz is given) | Do **not** display an ILS band. If a band must be shown, label "ILS frequencies are tuned in the VOR band 108–117.95 MHz (assumed from the VOR antenna range quoted in the notes)" |
| G2 | Number of VOR/ILS/DME/ADF **channels** | Not stated | Omit channel counts entirely |
| G3 | DME/VOR–ILS **pairing rule** (which DME follows which navaid) | Notes only say the selected station "can be of VOR or ILS type" and the MFD CLASS shows VOR/DME or ILS/DME | "DME1 follows the navaid tuned on side 1 and DME2 the navaid tuned on side 2 (assumed)" |
| G4 | GLS frequency band / channel numbering | Not stated (example shows 103.20) | Omit; treat the GLS "frequency" as an opaque channel identifier |
| G5 | RA accuracy, resolution, update rate | Not stated | Omit any accuracy figure |
| G6 | RA lower limit of the measuring band (does it read 0 ft?) | Not stated; only "from ground up to 2500 ft" for PFD | "Display band = 0 to 2500 ft (assumed lower limit)" |
| G7 | Marker OM/MM/IM discrimination (tone frequencies / durations) | Not stated; only the colours | Model the three markers as discrete events with the stated colours only |
| G8 | ADF fitment on the simulated aircraft | "1, 2 or no ADF systems" | Simulate **2 ADF** and provide a switch to remove them; label "(assumed fit: 2 ADF)" |
| G9 | Exact quantity of OANCs | Not stated | "One OANC (assumed)" |
| G10 | Behaviour on **single** IOM failure (only "both IOMs failed" is described) | Not stated | "One IOM failed → that side loses FMS auto-tune and reverts to RMP back-up on that side only (assumed)" |
| G11 | "R" vs "B" back-up annunciation on the ND | Text says "R", diagram callout shows "B" | Display **"B"** on the schematic and note "text says R (note conflict)" — see 0.11 |
| G12 | VOR/ADF **audio ident** volume/selection detail beyond the VOICE P/B | Not stated | Model audio as ON/OFF per selected navaid |
| G13 | ADIRU/FMS position blending algorithm and GPS PRIMARY criteria | Not stated | Model GPS PRIMARY as a boolean driven by "GPS data valid AND used by FMS" (assumed) |
| G14 | "VV" P/B function on the EFIS CP | Not stated in these pages | Leave inert and labelled "not covered in these notes" |
| G15 | MLS installation | RMP NAV page shows an "MLS ►" line and the MFD an ILS/MLS block; no MLS system described | Show the line as present but not implemented; "MLS not described in these notes" |
| G16 | LRU part numbers | Not given for any nav LRU | Omit |
| G17 | Timings (test durations, warm-up, tuning latency) | Not stated | Omit; animate without stated timings |

---

## 0.9 LEARNING OUTCOMES (CAAS SAR-66 Cat B2, Level 2)

On completion the learner will be able to:
1. **Identify** the quantity, identifier, antenna and power source of each A380 radio-navigation LRU (2 MMR, 2 VOR, 2 DME, 0/1/2 ADF, 3 RA, 1 OANC) and **locate** each antenna on the airframe.
2. **Trace** the tuning path of a given navaid from the FMC through the IOM and the on-side RMP to port B of the receiver, and contrast it with the manual (MFD) and back-up (RMP port A) paths.
3. **Predict** the ND and MFD tuning-mode annunciation ("M", back-up) and the affected equipment for a stated failure (IOM 3+4 loss, RMP loss, VOR2 loss, MMR1 loss, RA3 loss).
4. **Operate** the ILS approach configuration — tune both ILS on the same frequency, select LS on the EFIS CP, arm APPR — and **explain** each resulting PFD/ND indication.
5. **Distinguish** the five MMR landing functions (ILS, FLS, MIX LOC/VNAV, GLS, GPS) by their signal source, whether tuning is required, and their PFD/ND symbology.
6. **Explain** the radio-altimeter architecture: three transceivers, the ±30° antenna limit, validity to 5000 ft, PFD display to 2500 ft, the A429 bus-1 / ADCN-backup path, the PRIM source allocation, and the ground/flight inhibition of interactive mode.
7. **Isolate** a radio-nav fault to an LRU using the ECAM indication plus the OMS interactive test menu (MMR System Test, VOR 1/2, DME 1/2, ADF 1/2, DRA RAMP/SYSTEM test), and state the post-replacement verification.

---

## 0.10 MISCONCEPTIONS the simulation must expose

1. **"There is one ILS receiver and one GPS receiver."** In fact both live inside each **MMR**, and the ILS, FLS, GPS, GLS and MIX LOC/VNAV functions are all functions of the same two boxes — losing MMR1 loses ILS 1 *and* GPS 1.
2. **"Each receiver has its own antenna."** The Localizer, both G/S antennae and the VOR antenna are **common/dual** — a single LOC antenna feeds both MMRs, one dual VOR antenna feeds both VOR receivers, and the **Marker antenna feeds VOR1 only**, so a VOR1 failure also kills the Marker.
3. **"FLS is just ILS from a different station."** FLS needs **no ground station and no tuning** — the beam is computed from FMS anchor-point data and ADIRS position; MIX LOC/VNAV mixes a *real* LOC with a *computed* G/S.
4. **"Manual tuning bypasses the RMP."** Manual (MFD) tuning still goes **through the IOMs and RMPs to port B**; only the RMP NAV **back-up** mode drives **port A** and by-passes the FMS/IOM chain.
5. **"The radio altimeter only works below 2500 ft."** 2500 ft is only the **PFD display** limit; the height is valid for user systems (AFS, TAWS, FWS) up to **5000 ft** — and it is the **±30° roll/pitch** antenna limit, not the height, that invalidates a reading in a steep manoeuvre.
6. **"The G/S antenna is selected by the pilot."** It is switched automatically by the RF relay from the **LAS/FT** discretes generated by the PRIMs from landing-gear status + radio-altimeter data (capture antenna gear up, track antenna gear down), acknowledged by VASA.

---

## 0.11 DEFINITIONS & PRECEDENCE

| Term | Definition in the notes' sense |
|---|---|
| **Dependent position determining system** | A navigation system that "is dependent on ground stations" for its data — DME, VOR/Marker and (optional) ADF. It computes navigation data (bearing, slant distance) *from* ground stations (L1 pp.22, 24). |
| **Independent (position determining) system** | A system needing no ground station. The notes apply this word explicitly to the **Radio Altimeter**: "The Radio Altimeter (RA) is an **independent** system, which gives radio height information" (L1 p.18). By the same criterion the **FLS** function is described as "autonomous and does not require any additional information from the ground". |
| **Auto(matic) tuning** | Normal operation: each active FMC, through its IOM, tunes its own-side navaids via the associated RMP, using identification/frequency data stored in the navigation database. MFD TUNING MODE column reads AUTO. |
| **Manual tuning** | Crew tuning on the MFD **POSITION/NAVAIDS** page via the KCCU; settings sent on **port B** of the receivers via the IOMs and RMPs; **"M"** underlined and dimmed on the ND. |
| **Backup tuning (NAV back-up)** | Used when both IOMs (3 and 4) have failed: receivers are tuned directly from the RMPs, CAPT and F/O each on their own side, receivers listening on **port A**; annunciated on the ND. |
| **Port A / Port B** | The two tuning inputs of every radio-nav receiver. Port B = the normal FMS/manual path via the RMP; port A = the direct RMP/back-up path used when no activity is detected on port B. |
| **Multi-mode (receiver)** | One LRU computing several landing/positioning functions from several antennae: ILS, FLS, GPS, GLS (option) and MIX LOC/VNAV, plus a BITE module. |
| **Ground-based augmentation (GLS / GNSS Landing System)** | A GLS **ground station** sends pseudo-range corrections, satellite integrity information and final-approach-segment data to the MMR over the **LOC antenna**; the MMR combines these with GPS to compute a more accurate position and an approach "Beam", then pseudo-LOC and pseudo-Glide deviations. |
| **Marker** | A VOR1-hosted function giving aural and visual indication when the A/C overflies a 75 MHz ground marker beacon: Outer Marker (blue), Middle Marker (amber), Inner Marker (white). |
| **Pseudo LOC / pseudo G/S (F-LOC / F-G/S)** | Lateral and vertical deviations *computed* by the MMR relative to a defined beam (FLS or GLS), not received from a LOC/G/S ground transmitter. |
| **Approach capability** | The CAT/DH-type capability computed by the **FCDC** (in CPIOM-C) from MMR status relayed by the PRIMs, and displayed on the PFD FMA. |
| **TTI (Tune/Test Inhibit)** | A PRIM-generated discrete that freezes navaid tuning and inhibits the MMR test when the A/C is near the ground (below 700 ft with NLG extended). |
| **Normal mode / interactive mode (OMS)** | Normal mode is active in flight; interactive mode (interactive BITE tests) is active **only on ground**, gated by the LGERS GND/FLT discrete and, for the RA, additionally by MASTER LEVER ON. |
| **ADB cycle** | One of the **2** airport-database cycles embedded in the OANC; the crew swaps active/second on the OANS STATUS page; an expired cycle raises "DATABASE CYCLE NOT VALID". |
| **BTV / ROP** | Brake To Vacate and Runway Overrun Protection — PRIM functions whose data the OANS displays. |

### Conflicts between the two note sets, and precedence

| Item | LEVEL I (2007) | LEVEL 2&3 (2011/2013) | Preference and reason |
|---|---|---|---|
| Back-up tuning annunciation | not covered | Text (p.40) says **"R"**; the p.41 illustration callout shows **"B"** for BACKUP TUNING | **Internal conflict inside the Level 2&3 set.** Show **"B"** on screen (the illustration is the display artefact) and record the "R" wording in the inspector text. Flag as a note ambiguity, not as fact. |
| RA validity height | "displayed on the PFD up to 2500 ft" only | Adds: "valid for user systems **up to 5000 ft**", displayed on PFD "from ground up to 2500 ft" | **Level 2&3** — more detailed and more recent; the two are complementary, not contradictory. |
| RA antenna wording | "3 transmission antennae and 3 reception antennae, all installed at the bottom of the rear fuselage" | "installed at the bottom of the fuselage on the **rear cargo compartment area**" | **Level 2&3** for the precise location; both agree on 3 + 3. |
| RA transceiver location | "aft cargo compartment" | rear cargo compartment (diagram) | Equivalent; use "aft/rear cargo compartment". |
| MMR GPS antenna count | "two GPS antennae" (system level) and "1 active GPS antenna" (per MMR) | identical wording | No conflict — 2 total, 1 per MMR. |
| ADF fit | "The A/C might be equipped with 2 ADF systems" | "the A/C can be equipped with **1, 2 or no** ADF systems" | **Level 2&3** — the more complete statement. |
| Tuning description | "tuned automatically by FMS in normal operation, manually by the crew (KCCU + MFD POSITION/NAVAIDS, RMP for back-up)" | Full three-mode description with ports A/B, IOMs and the RMP dialog bus | **Level 2&3 for logic** (0.4), Level I for the plain-language framing used in Learn mode. |
| OANS | Presentation only (ADIRS/FMS/MMR → OANS → CMV → ND; ARC/NAV/PLAN; ZOOM) | Adds OANC/ADB/BITE, RS 422, LGERS, BTV/ROP, DLCS, 2 ADB cycles, soft-control-panel pages | **Level 2&3** throughout. |

**General precedence rule applied here:** ratings and quantities from the **higher-level, more recent Level 2&3 set** (Nov 2011 / Aug 2013); Level I used where it adds the only statement on a point (e.g. "Marker function only active within VOR1 receiver" appears in both, "3 RA transceivers installed in the aft cargo compartment" is clearest in Level I) and for Level-1 framing text in the lesson rail. Where only Level I gives a fact, it is used and cited as such.

---

# PART B — DESIGN BRIEF

**File produced:** `aerosim_ata34_radio_nav_aids.html`

## Archetype: SYSTEM

Every item here is a receiver with an antenna, a power source and a data path. The interesting logic is the tuning priority chain and the conditions that gate each output — not a nodal circuit — so the engine is a health-and-routing solver. Three Explore views are used because the topic has three different pictures a technician must hold: what the boxes and antennas are, how they get tuned, and what the five MMR functions actually do.

## Page map

| Mode | What this topic gets |
|---|---|
| **Explore** | *Receivers & antennas* draws every LRU with its quantity, frequency range and supply bus against the antenna column, making the shared Localizer, glide slope and dual VOR antennas visible, and marking which glide slope antenna is currently selected. *Tuning chain* lays the three paths — automatic, manual and back-up — one above the other and lights the active one. *MMR landing functions* compares ILS, MIX, FLS, GLS and GPS side by side with a TUNING REQUIRED badge on each. The right rail carries live PFD and ND readouts, every control, and a per-LRU failure grid. 10-step build-up stepper. |
| **Build** | Constructor with 18 palette blocks — receivers, antennas, tuning-path units and users — undo/redo, JSON export/import, a path continuity tester, three starter architectures and **eight** check-my-build targets. |
| **Fault Lab** | 12 cases. Half are real defects; half are conditions or control positions that look like defects — the radio height missing at 3000 ft, the tuning frozen by TTI on short final, the airport map absent because the range selector is not at ZOOM. Eight diagnostic tests, the six-step flow, efficiency score, seeded exam mode. |
| **Learn** | 13 lesson steps, then a 12-question quiz mapped to LO1–LO6. |

## Outcome mapping

| Lesson steps | Quiz questions | Outcome |
|---|---|---|
| 1, 2, 3 | 1, 2, 3 | LO1 identify each LRU, its antenna and its power source |
| 4, 5, 6 | 4, 5 | LO2 trace the three tuning paths |
| 12 | 11 | LO3 explain which side of each pair is essential |
| 8, 9, 13 | 7, 8, 12 | LO4 operate the approach and airport-map configuration |
| 7 | 6 | LO5 distinguish the five MMR functions |
| 10, 11 | 9, 10 | LO6 explain the radio altimeter architecture and its two limits |

## Misconceptions the design forces into the open

The one-ILS-one-GPS belief dies when MMR 1 fails and both go (step 1, Q1, fault f2); the every-receiver-has-its-own-antenna belief dies at the shared antenna column and again when VOR 1 takes the Marker with it (steps 2 and 3, Q2, Q3, fault f1); the FLS-is-just-ILS belief dies at the TUNING REQUIRED badges (step 7, Q6); the manual-tuning-bypasses-the-RMP belief dies in the tuning view (step 5, Q5); the radio-altimeter-only-works-below-2500-ft belief dies twice, once on height and once on roll (step 10, Q9, Q10, faults f6 and f7); and the pilot-selects-the-glide-slope-antenna belief dies at the LAS/FT/VASC/VASA trace (step 8, Q7).
