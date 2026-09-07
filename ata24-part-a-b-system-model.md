# AeroSim Generator — PART A & PART B
**Topic:** ATA 24 – Electrical Power System Introduction & AC/DC Generation · **Aircraft:** Airbus A380 (RR Trent 900) · **Level:** CAAS SAR-66 Cat B2, Level 2 · **Archetype requested:** SYSTEM · **Session:** 45 min
**Sources:** notes_L1.txt (A380 TTM Level I, Apr 2007, pp. 2–53) = primary; notes_L2.txt (A380 TTM AC & DC Generation Presentation (2) + Architecture Description (2), 2011/2013) = ratings & control/indication detail.

> Terminology note. The two note sets differ on the DC conversion units: L1 calls them **BCRU 1, BCRU 2, BCRU ESS** with a separate **TR 2** as backup of BCRU 2; L2 calls the same three positions **TR 1, TR 2, TR ESS** ("three identical TRs"). Per the input block (L1 primary; palette lists BCRU and TR) the model uses the L1 names and lists the L2 names as aliases in the glossary. Other L1/L2 differences are flagged inline with (L1)/(L2).

---

## PART A — SYSTEM MODEL

### 0.1 COMPONENTS

| id | Full name | Acronym | Type | Ratings quoted from notes | Location (if given) |
|---|---|---|---|---|---|
| VFG1–VFG4 | Variable Frequency Generator 1–4 | VFG | source (AC) | 150 kVA, 3-phase, 115 VAC, 370–770 Hz (according to engine HP spool speed); identical & interchangeable, fit RR or EA engines | one per engine |
| GGPCU1–4 | Generator & Ground Power Control Unit 1–4 | GGPCU | controller | Functions: voltage regulation, connection/disconnection to busbars, generator & network protection, data transmission (ECAM), BITE. GGPCU n manages VFG n **and** EXT PWR n. Identical & interchangeable | — |
| APUGENA, APUGENB | APU Generator A / B | APU GEN | source (AC) | 120 kVA, 3-phase, 115 VAC, 400 Hz constant; driven at constant speed by APU; not interchangeable with VFGs | APU |
| GGPCU5, GGPCU6 | GGPCU 5 (APU GEN A), GGPCU 6 (APU GEN B) | GGPCU | controller | same functions as GGPCU1–4; interchangeable with them | — |
| EXT1–EXT4 | External power connection 1–4 (GPU) | EXT PWR / GPU | source (AC) | each plug: 90 kVA (min), 3-phase, 115 VAC, 400 Hz. GPU types: 90 kVA single output, or 180 kVA with two 90 kVA outputs (feeds 2 plugs) | 4 plugs behind nose landing gear; panels 1935VU (left, EXT 1&2), 1926VU (right, EXT 3&4) |
| EMERGEN | Emergency Generator (RAT-driven) | EMER GEN / RAT | source (AC, emergency) | 70 kVA, 3-phase, 115 VAC, 370–800 Hz (with air/turbine speed) | RAT; STOW panel on Hydraulic Ground Service Panel, left belly fairing |
| GCU | emergency Generator Control Unit | GCU | controller | voltage regulation, connection/disconnection, protection (inhibited in emergency config, L2), data, BITE | — |
| STATINV | Static Inverter | STAT INV | conversion (DC→AC) | 2.5 kVA, single-phase, 115 VAC, 400 Hz; input from BAT 1 + BAT ESS in parallel | — |
| BCRU1, BCRU2, BCRUESS | Battery Charge Rectifier Unit 1 / 2 / ESS (L2: TR 1 / TR 2 / TR ESS) | BCRU | conversion (AC→DC) | 115 VAC → 28 VDC converter, 300 A, + battery charge limiter; regulates DC V, controls/protects itself & its battery, data, BITE; 3 identical | — |
| TR2 | Transformer Rectifier 2 (backup of BCRU 2) (L1) | TR | conversion (AC→DC) | 115 VAC → 28 VDC **unregulated**, 300 A; no battery-charge regulation; also connects/protects BAT 2 when BCRU 2 lost; cooled by air extraction/convection + integral fan (L2) | — |
| APUTR | APU Transformer Rectifier | APU TR / TR APU | conversion | identical/interchangeable with TR 2; 300 A; manages APU BAT; dedicated, cannot connect to DC network | — |
| BAT1, BAT2, BATESS | Main Battery 1, 2; Essential Battery | BAT | source (DC) | 50 Ah; 28 VDC (L1) / 24 V nominal, normally > 25 V charged (L2); identical & interchangeable; FAULT legend if ≤ 25 V with current flow | access door behind NLG (pulley lift GSE) |
| APUBAT | APU Battery | APU BAT / BAT APU | source (DC) | 50 Ah, identical/interchangeable with other 3 batteries; dedicated to APU start | — |
| ACBUS1–4 | AC Main busbar 1–4 (L1: AC network 1–4) | AC BUS | bus | 115 VAC; in PEPDC; primary distribution | PEPDC |
| ACESS | AC ESS BUS (L1: AC ESS network) | AC ESS | bus (emergency distribution) | in EEPDC (L2) / Emergency Power Center (L1) | EEPDC |
| ACEMER | AC EMER BUS (L2) | AC EMER | bus (emergency) | supplied by STAT INV in batteries-only | EEPDC |
| ACGS1–4, DCGS | AC Ground Service busbars 1–4, DC GS BUS (via TR 2) | GS BUS | bus | loads: cockpit/cabin/lav/cargo/service/nav lights, outlets, parking brake, fuel qty & refuel, vacuum toilet, CIDS, water/waste, cargo doors & loading | — |
| DCBUS1, DCBUS2 | DC BUS 1 / 2 (L1: DC NETWORK 1 / 2) | DC BUS | bus | 28 VDC; PEPDC; primary distribution | PEPDC |
| DCESS | DC ESS BUS (L1: DC ESS NETWORK) | DC ESS | bus (emergency) | 28 VDC; EEPDC | EEPDC |
| APUSTART | APU STARTING BUS | — | bus (dedicated DC) | from AC BUS 4 via APU TR **or** APU BAT, never both | — |
| HOT1, HOT2, HOTESS | Hot busbars (L2) | HOT BUS | bus | directly on batteries; permanent loads; BAT 2 hot bus used for battery-only refuel & PDMI | — |
| GLC1–4 | Generator Line Contactor | GLC | contactor | commanded by GGPCU | PEPDC |
| AGCA, AGCB | APU Generator Contactor | AGC | contactor | — | PEPDC |
| EPC1–4 | External Power Contactor | EPC | contactor | — | PEPDC |
| BTC, SIC | Bus Tie Contactor; System Isolation Contactor ("transfer circuit") | BTC / SIC | contactor | reconfigure Main busbars by source availability; segregate side 1/side 2 when both APU GENs connected | PEPDC |
| TRLC1/2/ESS, BATLC1/2/ESS | TR Line Contactor; Battery Line Contactor | TRLC / BATLC | contactor | listed in L2 glossary; positions inferred | — |
| IBLC, GSLC, EHAC | Inter Bus Line Contactor; Ground Service Line Contactor; EHA Contactor | — | contactor | listed in L2 glossary (names only) | — |
| GALLEY | Galleys (shed loads) | — | load (AC, heavy > 15 A) | shed when < 3 VFGs / ≤ 2 GPUs | cabin |
| ESSLOADS | Essential loads (fly & land) | — | load | via emergency distribution | — |
| APUSTARTER | APU starter | — | load (DC) | supplied from APU STARTING BUS | APU |
| CB | Circuit breakers (ECAM C/B page, CBM application) | C/B | circuit breaker | status monitored by CBM app in CPIOM-E1/E2; remote C/Bs controlled via PDMI/PDMC | PEPDC/SEPDC/SPDB |
| PEPDC, SEPDC×2, SPDB×8, EPC(EEPDC) | Primary / Secondary EPDCs, Secondary Power Distribution Boxes, Emergency Power Center | — | distribution (context) | PEPDC side 1/side 2; heavy loads > 15 A; secondary ≤ 15 A; 6 SPDB cabin, 2 lower deck | — |
| GNDSVCE | GND SVCE CTL switch | — | switch | ON: EXT 1 directly supplies GS busbars (main network not powered) | main-deck cabin near door M1L |
| BATPANEL | BAT maintenance panel 1255VM | — | indicator | voltage display independent of ECAM, selectable per battery, works with batteries disconnected | overhead |

### 0.2 TOPOLOGY (from → via → to)

| From | Via | To | Condition / note |
|---|---|---|---|
| VFG n | GLC n (GGPCU n) | AC BUS n | normal, engine n running, GEN n P/B on |
| EXT PWR n | EPC n (GGPCU n) | AC BUS n | GPU plugged, EXT n pressed in |
| APU GEN A | AGC A (GGPCU 5) + transfer circuit | AC BUS 1 and AC BUS 2 | when no other sources |
| APU GEN B | AGC B (GGPCU 6) + transfer circuit | AC BUS 3 and AC BUS 4 | when no other sources |
| AC BUS n | BTC / SIC (transfer circuit) | other AC BUS | reconfiguration (see 0.4) |
| AC BUS 1 | (contactor, assumed name ESS-LC) | AC ESS BUS | normal |
| AC BUS 4 | (assumed) | AC ESS BUS | backup if AC BUS 1 not available |
| EMER GEN (RAT) | GCU line contactor (assumed) | AC ESS BUS + AC EMER BUS | RAT extended, emergency config |
| AC ESS BUS | (assumed) | AC EMER BUS | normal |
| STAT INV | (assumed) | AC EMER BUS only | batteries-only; AC ESS BUS not supplied (L2) |
| BAT 1 + BAT ESS (parallel) | — | STAT INV | |
| AC BUS 2 | BCRU 1 → TRLC 1 | DC BUS 1 | |
| AC BUS 3 | BCRU 2 → TRLC 2 | DC BUS 2 | normal |
| AC BUS 3 (assumed same feed) | TR 2 | DC BUS 2 | on loss of BCRU 2 |
| AC ESS BUS | BCRU ESS → TRLC ESS | DC ESS BUS | |
| BAT 1 | BATLC 1 | DC BUS 1 (parallel with BCRU 1) | normal; NBPT |
| BAT 2 | BATLC 2 | DC BUS 2 (parallel with BCRU 2 / TR 2) | normal; not connected in batteries-only |
| BAT ESS | BATLC ESS | DC ESS BUS | normal |
| BAT 1 + BAT ESS | — | DC ESS BUS | batteries-only / STAT INV config |
| BAT 1/2/ESS | — | HOT BUS 1/2/ESS | permanent |
| AC BUS 4 | APU TR | APU STARTING BUS | |
| APU BAT | (contactor) | APU STARTING BUS | never together with APU TR |
| AC BUS 1–4 | GSLC (assumed) | AC GS BUS 1–4 | when main busbars energised |
| TR 2 | — | DC GS BUS | |
| EXT PWR 1 | GND SVCE CTL = ON | AC GS 1–4, TR 2 → DC GS BUS | on ground, main network NOT powered |

### 0.3 CONTROLS

| Control | Panel | Positions | Commands | Legends / lights |
|---|---|---|---|---|
| DRIVE 1–4 P/BSW | overhead ELEC | pressed in (normal) / released (DISC) | mechanical disconnection of VFG (drive fault); not reconnectable in flight (assumed) | FAULT (amber, assumed colour), OFF/DISC |
| GEN 1–4 P/BSW | overhead ELEC | in (ON) / out (OFF) | electrical disconnection (fault) and connection (after fault reset) of VFG to/from network | FAULT, OFF |
| APU GEN A / B P/BSW | overhead ELEC | in / out | connection/disconnection of APU gen to Main busbars | FAULT, OFF (both off = normal) |
| EXT 1–4 P/BSW | overhead ELEC | in / out | connect/disconnect GPU to its AC Main busbar; shows GPU status | green AVAIL, blue ON |
| BAT 1 / BAT 2 / BAT ESS P/BSW | overhead ELEC | in / out | manual connect/disconnect of battery | FAULT (≤ 25 V with current flow, or fault preventing connection), OFF |
| BAT APU P/BSW | overhead ELEC | in / out | connect/disconnect APU battery | FAULT, OFF (assumed same legends) |
| BUS TIE P/BSW | overhead ELEC | AUTO / OFF | transfer circuit auto reconfiguration enabled / inhibited (assumed – notes name the BTC but not the P/B) | OFF |
| RAT MAN ON P/BSW (guarded) | overhead EMER ELEC PWR | guarded / pressed | forces RAT extension if auto fails | EMER GEN red FAULT (generator not connected in emergency config) |
| GND SVCE CTL SW | main deck near door M1L | ON / OFF | EXT 1 → GS busbars directly | — |
| External power panels 1935VU / 1926VU | nose | — | — | amber AVAIL; white NOT IN USE |
| BAT panel 1255VM | overhead | select BAT 1 / 2 / ESS / APU / OFF | display battery voltage independent of ECAM | voltage readout |
| RAT STOW panel | belly fairing | stow | retract RAT on ground (maintenance) | — |

### 0.4 LOGIC (priority order)

1. **VFG availability:** VFG n available IF engine n running AND DRIVE n connected AND GEN n on AND no GGPCU n protection trip.
2. **Own source first:** each AC BUS n takes its own VFG n; on ground with engines off, its own EXT PWR n when pressed in and within limits (L2: "First priority for each busbar is its own External Power source").
3. **Paralleling forbidden:** a busbar has exactly one source; when both APU GENs are connected the transfer circuit segregates side 1 (BUS 1, 2) and side 2 (BUS 3, 4).
4. **Transfer circuit reconfiguration:** IF a Main busbar has no own source THEN it is supplied from another available source in priority order: same-side neighbour busbar > side APU GEN (A→1,2; B→3,4) > cross-side. IF only ONE source (VFG or 90 kVA GPU) is available THEN only the two Main busbars on its side are supplied.
5. **Load shedding (ELM):** 3 VFGs → all busbars and loads incl. galleys; 2 VFGs → all busbars, some loads shed; 4×90 kVA GPUs or 2×180 kVA → everything; 3 GPUs → all busbars, galleys may shed on overload; 2 GPUs → all busbars, galleys shed; 1 GPU → its side only. Loads reconnect when power is sufficient.
6. **AC ESS BUS:** from AC BUS 1; if AC BUS 1 not available → AC BUS 4; if no Main AC → EMER GEN when RAT extended.
7. **AC EMER BUS:** with EMER GEN → supplied with AC ESS; batteries-only with BAT 1 and BAT ESS pressed in → STAT INV automatically supplies AC EMER BUS only (AC ESS BUS not supplied).
8. **DC normal:** DC BUS 1 ← BCRU 1 (AC BUS 2); DC BUS 2 ← BCRU 2 (AC BUS 3); DC ESS ← BCRU ESS (AC ESS). Batteries permanently in parallel with their BCRU (charged by it).
9. **BCRU 2 loss:** TR 2 takes over DC BUS 2 (unregulated 28 VDC) and connects/protects BAT 2.
10. **NBPT (DC only):** during AC source reconfiguration the battery holds its DC busbar; no NBPT on the AC side.
11. **Batteries only (no AC anywhere):** BAT 1 + BAT ESS in parallel → DC ESS BUS; BAT 2 not connected to DC BUS 2; DC BUS 1 & 2 not supplied; Hot busbars always live; STAT INV → AC EMER BUS.
12. **Batteries off:** all three P/B released → all batteries disconnected (hot buses still fed, assumed).
13. **Emergency (RAT):** RAT extends automatically on TEFO or LMES (loss of all AC Main busbar supply in flight); else RAT MAN ON. EMER GEN → AC ESS + AC EMER; DC ESS from BCRU ESS (L2) (L1: in parallel with ESS BAT and BAT 1). EMER GEN disconnects at low airspeed on landing → STAT INV again. IF emergency config AND EMER GEN not connected THEN EMER GEN FAULT red.
14. **APU start:** APU STARTING BUS ← APU TR when AC BUS 4 live, ELSE ← APU BAT when pressed in; never both.
15. **Ground service:** IF Main AC busbars energised THEN GS busbars fed from their Main busbars and GND SVCE config de-energised; ELSE IF EXT 1 available AND GND SVCE CTL ON THEN EXT 1 directly feeds AC GS 1–4 and TR 2 → DC GS; main network stays dark.
16. **Battery FAULT:** IF battery ≤ 25 V with current flow THEN BAT FAULT legend.

### 0.5 STATES

| State | Live AC | Live DC | Notes |
|---|---|---|---|
| S1 Normal flight (4 VFG) | AC BUS 1–4, AC ESS (from 1), AC EMER, GS 1–4 | DC 1, DC 2, DC ESS, APU START (APU TR), Hot | galleys on |
| S2 Ground – 4 GPUs | all | all | EXT n → AC BUS n; galleys on |
| S3 Ground – 2 GPUs (EXT 1 & 2 ON, 3 & 4 AVAIL) | all Main via transfer | all | galleys shed; EXT 3/4 AVAIL green, NOT IN USE white on panel |
| S4 APU only (both gens) | A→1,2; B→3,4; ESS from 1 | all | side segregation |
| S5 Single VFG failure (VFG 2 lost) | all via transfer | all | galleys still on (3 VFGs) |
| S6 Two VFGs lost | all Main | all | some loads (galleys) shed |
| S7 One VFG only | its side's two Main buses only | side DC + ESS if side 1 | |
| S8 BCRU 2 failure | all | DC 2 via TR 2 | unregulated |
| S9 Batteries only (ground) | AC EMER (STAT INV) | DC ESS (BAT 1 + BAT ESS), Hot | DC 1/2 dark; ECAM STAT INV dashes on ground |
| S10 Emergency – RAT/EMER GEN | AC ESS, AC EMER | DC ESS (BCRU ESS) | LMES; EMER GEN 70 kVA |
| S11 Ground service (EXT 1 + GND SVCE CTL ON) | AC GS 1–4 | DC GS (TR 2) | main network dark; EXT 1 AVAIL green |
| S12 APU start on battery | — | APU START (APU BAT), Hot | |
| Free-play | — | — | any switch |

### 0.6 INDICATIONS

- **ECAM ELEC AC page:** each generator's load %, voltage, frequency and busbar allocation; EXT n voltage/frequency/allocation; STAT INV V/Hz (dashes on ground).
- **ECAM ELEC DC page:** connected batteries: voltage & current (charging/discharging); disconnected: "OFF"; DC supply status; STAT INV DC status.
- **ECAM C/B page:** C/B status from CBM application.
- **Overhead ELEC panel legends:** GEN/DRIVE/APU GEN/BAT FAULT & OFF; EXT AVAIL (green) / ON (blue); EMER GEN FAULT (red).
- **External power panels:** amber AVAIL, white NOT IN USE.
- **BAT panel 1255VM:** independent battery voltage display.
- **BITE:** GGPCU, GCU, BCRU/TR each have a BITE function; CBM sends cockpit status message on any tripped protective device.
- Warning captions (e.g. "ELEC GEN 2 FAULT") are **not** in the notes; the sim uses the legend text and tags captions "(assumed wording)".

### 0.7 NUMBERS (only these may be shown as "specified")

115 VAC · 28 VDC · VFG 150 kVA, 3 ph, 370–770 Hz · APU GEN 120 kVA, 400 Hz · GPU plug 90 kVA (min), 400 Hz; GPU 90 kVA single / 180 kVA dual (2 × 90) · EMER GEN 70 kVA, 370–800 Hz · STAT INV 2.5 kVA, 1 ph, 115 VAC, 400 Hz · BCRU 300 A · TR 2 300 A · APU TR 300 A · BAT 50 Ah, 28 VDC (L1) / 24 V nominal, > 25 V charged (L2), FAULT ≤ 25 V with current · heavy loads > 15 A, secondary ≤ 15 A · 4 VFG, 4 GGPCU (+ GGPCU 5, 6), 2 APU GEN, up to 4 GPU/plugs, 3 BCRU, 1 TR (+ APU TR), 3 BAT (+ APU BAT), 4 AC Main busbars, 4 AC GS + 1 DC GS, 2 SEPDC, 8 SPDB (6 cabin + 2 lower deck), 2 CPIOM-E, 2 PDMC · 3 VFGs needed for whole network incl. galleys · panels 1935VU, 1926VU, 1255VM · door M1L.

### 0.8 GAPS → assumptions (all tagged "(assumed)" in the page)

| Gap | Assumption used |
|---|---|
| Transfer-circuit contactor layout | BTC 1-2 (side 1), BTC 3-4 (side 2), SIC between sides |
| Priority VFG vs EXT PWR when both available on same bus | VFG has priority; EXT stays AVAIL |
| Single APU GEN alone | supplies its own side only (same rule as single VFG/GPU) |
| Galley shedding with mixed/APU sources | galleys on only when ≥ 3 direct sources (VFG or GPU); APU-only → galleys shed |
| AC EMER BUS normal supply | from AC ESS BUS |
| TR 2 AC supply | AC BUS 3 (same as BCRU 2) |
| Contactor names not in notes (ESS line contactor, EMER GEN line contactor, GSLC positions) | generic names, labelled |
| BUS TIE P/B, legend colours (amber FAULT, white OFF), ECAM caption wording | standard Airbus practice, tagged |
| DC BUS 1/2 hold-up time by battery during NBPT | shown as "momentary" text, no numeric value |
| Load values (kVA/A on ECAM %) | illustrative percentages, tagged |

### 0.9 LEARNING OUTCOMES (derived)

- **LO1 Identify** the A380 AC and DC generation sources, their control units and their ratings (V, Hz, kVA, A, Ah).
- **LO2 Trace** the normal supply path from each source to each AC and DC busbar, including the AC ESS / DC ESS backups.
- **LO3 Predict** the transfer-circuit reconfiguration and load-shedding result when one or more sources are lost.
- **LO4 Operate** the ELEC overhead panel controls and interpret their legends and the ECAM ELEC AC/DC pages.
- **LO5 Isolate** a generation fault (drive, generator, GPU, BCRU/TR, battery) to the failed LRU using indications and a multimeter.
- **LO6 Explain** the batteries-only, static-inverter and RAT/EMER GEN emergency configurations.

### 0.10 MISCONCEPTIONS the sim must expose

- M1 "DRIVE and GEN P/BSW do the same thing" — DRIVE disconnects mechanically (irreversible in flight); GEN disconnects electrically (resettable).
- M2 "One generator can power the whole aircraft" — a single VFG/GPU only feeds its side.
- M3 "Batteries feed DC BUS 1 and 2 when everything else is lost" — batteries-only feeds DC ESS (and Hot) only.
- M4 "The STAT INV supplies the AC ESS BUS" — it supplies the AC EMER BUS only.
- M5 "GPUs and VFGs can be paralleled" — one source per busbar; EXT stays AVAIL.
- M6 "TR 2 is just another BCRU" — it is unregulated and has no battery-charge regulation.

*(Scope check: ~35 components, one subsystem family — buildable in one page; the distribution centres (SEPDC/SPDB/PDMI) are kept as context only.)*

---

## PART B — DESIGN BRIEF

**Archetype: SYSTEM** (as requested). The topic is a source-priority / bus-reconfiguration network, so an ECAM-style synoptic with a power-flow graph solver teaches exactly the outcomes above; a nodal circuit solver would add nothing at Level 2. Build mode therefore uses the aircraft palette with a connectivity solver (source → contactor/C-B → bus → converter → bus → load) rather than MNA.

### Page map

| Tab | Contents for this topic |
|---|---|
| **Explore** | SVG synoptic (pan/zoom/fit): 4 VFG, APU GEN A/B, EXT 1–4, EMER GEN/RAT, STAT INV, AC BUS 1–4, AC ESS, AC EMER, BCRU 1/2/ESS, TR 2, DC BUS 1/2/ESS, BAT 1/2/ESS, APU TR, APU BAT, APU START BUS, GS buses, galleys & ESS loads; animated flow dots (amber AC / green DC / magenta emergency / grey dead / red fault). Overhead ELEC panel with clickable DRIVE 1–4, GEN 1–4, APU GEN A/B, EXT 1–4, BUS TIE, BAT 1/2/ESS/APU, RAT MAN ON, GND SVCE CTL + engine/APU/GPU environment toggles. Scenario selector (S1–S12 + Free-play), signal trace (click bus/load), inspector panel, build-up stepper (18 steps), ECAM ELEC AC/DC mini-pages. |
| **Build** | Palette: VFG, APU GEN, EXT PWR, EMER GEN, contactor, C/B, AC BUS, AC ESS BUS, BCRU, TR, STAT INV, BAT, DC BUS, load. Click-to-place on grid, wire port-to-port (orthogonal), rotate, delete, duplicate, undo/redo, select-all/move; Run/Pause/Step/Reset + speed; voltmeter probe + 2-channel scope (AC 400/VF sine vs DC); 3 starter circuits; "Check my circuit" against target "DC ESS BUS supply path"; JSON export/import + URL hash. |
| **Fault Lab** | Instructor switch (hide-able) with 10 faults + Random + seeded Exam mode; system reacts per 0.4; multimeter (V / Ω-continuity on any bus or contactor), C/B panel, ECAM pages, isolate & replace-LRU actions; O-H-T-I-R-V flow with step counter and efficiency score; debrief with correct path, note excerpt and misconception hint. |
| **Learn** | 8-step lesson rail with action + auto-detected completion + predict-observe-explain + "Ask the class"; 8-question quiz mapped to LO1–LO6; results block (name, date, score per LO) to copy into Brightspace; glossary with hover definitions. |

### Scenarios (Explore)
S1 Normal flight · S2 Ground 4 GPU · S3 Ground 2 GPU · S4 APU only · S5 VFG 2 lost · S6 Two VFGs lost · S7 One VFG only · S8 BCRU 2 fail → TR 2 · S9 Batteries only · S10 Emergency RAT · S11 Ground service · S12 APU start on battery · Free-play.

### Faults (Fault Lab)
F1 VFG 2 electrical fault (GGPCU 2 trip → GEN 2 FAULT) · F2 VFG 3 drive fault (DRIVE 3 FAULT) · F3 APU GEN A fault · F4 GPU 2 unplugged while ON · F5 BCRU 2 failure → TR 2 takeover · F6 BCRU ESS failure · F7 BAT 1 depleted (≤ 25 V, FAULT) · F8 GLC 1 welded open (GEN 1 on, AC BUS 1 via transfer) · F9 LMES in flight → RAT · F10 EMER GEN failure after RAT (red FAULT) · plus "wrong switch" (BAT ESS off in batteries-only) reachable by Random.

### Starter circuits (Build)
B1 "VFG 1 → GLC 1 → AC BUS 1 → galley load" · B2 "AC BUS 2 → BCRU 1 → DC BUS 1 ∥ BAT 1 → DC load" · B3 "APU starting network: AC BUS 4 → APU TR → APU START BUS ← APU BAT".

### Lesson steps → outcome
L1 Normal flight: trace AC BUS 1 back to VFG 1 (LO2) · L2 Predict, then release GEN 1: AC ESS moves to AC BUS 4 (LO3) · L3 Ground: press EXT 1, AVAIL→ON (LO4) · L4 APU only: A→1,2 B→3,4 (LO2) · L5 DRIVE vs GEN: release DRIVE 2, try to reconnect (LO4, M1) · L6 Batteries only: which buses live? (LO6, M3/M4) · L7 Fault Lab: inject BCRU 2 failure, isolate with multimeter (LO5) · L8 Build: assemble DC ESS supply path, Check my circuit (LO2).

### Quiz (8) → outcome
Q1 VFG rating (LO1) · Q2 APU GEN frequency vs VFG (LO1) · Q3 AC ESS backup source (LO2) · Q4 Single GPU supplies what (LO3, M2) · Q5 DRIVE vs GEN P/B (LO4, M1) · Q6 Batteries-only live buses (LO6, M3) · Q7 STAT INV output & bus (LO6, M4) · Q8 BCRU 2 lost → which unit and what differs (LO5, M6).
