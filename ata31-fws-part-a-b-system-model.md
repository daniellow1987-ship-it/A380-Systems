# A380 ATA 31 — Flight Warning System (FWS)
## Phase 0 System Model for AeroSim Generator

**Source note sets (the ONLY authority for this model):**

| Ref | Document | Section | Doc pages |
|---|---|---|---|
| **L1** | A380 TTM — *MAINTENANCE COURSE - T1 + T2 (RR / Metric), LEVEL I - ATA 31 Ind./Recording Syst.*, Apr 19 2007 | FLIGHT WARNING SYSTEM PRESENTATION (1) | 22–47 |
| **L2a** | A380 TTM — *MECHANICAL & AVIONICS COURSE - T1+T2 (LVL 2&3) (RR Trent 900), 31 - Indicating/Recording Systems*, Nov 21 2011 | FLIGHT WARNING SYSTEM DESCRIPTION (2) | 46–59 |
| **L2b** | same as L2a | FLIGHT WARNING SYSTEM DESCRIPTION (3) | 60–87 |
| **L2c** | same as L2a | INDICATING & RECORDING SYSTEMS OPS/CTL & IND (2) | 88–91 |

**Precedence rule adopted:** where L1 and L2a/L2b differ, the **Level 2&3 set (L2a/L2b, 2011) is preferred** — it is more recent and more detailed. L1 is retained only for wording that L2 does not carry (e.g. the acronym legend box, some flight-phase framing). All conflicts are itemised in §0.11.

**Every number, legend and acronym below is transcribed from the notes.** Anything the simulation needs but the notes do not state is in §0.8 and must be tagged "(assumed)" on screen.

---

## 0.1 COMPONENTS

| id | Full name (as expanded in the notes) | Acronym | Type | Quantity / identifiers quoted | Location given? |
|---|---|---|---|---|---|
| FWS | Flight Warning System | FWS | system (centralized) | 1 system, "mainly composed of two FWS Applications" | not stated |
| FWSAPP1 | FWS Application 1 | — | computer/application (software) | "FWS APPLICATION 1", hosted in CPIOM-C1 | in CPIOM-C1 |
| FWSAPP2 | FWS Application 2 | — | computer/application (software) | "FWS APPLICATION 2", hosted in CPIOM-C2 | in CPIOM-C2 |
| CPIOMC1 | Core Processing Input/Output Module -C1 | CPIOM-C1 | computer (host) | "CPIOM-C1", labelled "1" on the CPIOM-C stack | not stated |
| CPIOMC2 | Core Processing Input/Output Module -C2 | CPIOM-C2 | computer (host) | "CPIOM-C2", labelled "2" on the CPIOM-C stack | not stated |
| ECP | ECAM Control Panel | ECP | control panel | 1 panel, identifier **(1135VM)** printed on the panel | pedestal (implied by cockpit photo; not stated in text) |
| IOMs | Input/Output Modules | IOMs | network interface | "IOMs" generic; **IOM-7** and **IOM-8** named for AMU CALL indications | not stated |
| ADCN | Aircraft Data Communication Network (L2b, L1 prose) / "Avionics Data Communication Network" (L1 legend box) | ADCN | network | 1 network; carries AFDX | not stated |
| AFDX | Avionics Full DupleX Switched Ethernet | AFDX | network protocol | — | — |
| A429 | ARINC 429 | ARINC 429 | network protocol (backup + conventional LRUs) | — | — |
| CAN | CAN buses (ECP→IOM connection) | CAN | network | "through CAN buses connections" | — |
| LRMs | Line Replaceable Modules | LRM | data source | plural, quantity not stated | not stated |
| LRUAFDX | Line Replaceable Units with AFDX interface | LRU | data source | plural, quantity not stated | not stated |
| LRUCONV | Line Replaceable Units (conventional) | LRU | data source | plural, quantity not stated | not stated |
| CDS | Control and Display System (ECAM part) | CDS | display system | 1; drives PFD and EWD (and SD) | cockpit |
| EWD | Engine/Warning Display | EWD | visual indicator (display unit) | 1 EWD referenced throughout | cockpit centre (photo) |
| SD | System Display | SD | visual indicator (display unit) | 1 SD referenced throughout | cockpit centre (photo) |
| PFD | Primary Flight Display | PFD | visual indicator (display unit) | 2 implied ("PFDs Lower Zone", "PFDs lower zones") | cockpit |
| AMU1 | Audio Management Unit 1 | AMU | aural device (amplifier/router) | "AMU 1" | not stated |
| AMU2 | Audio Management Unit 2 | AMU | aural device (amplifier/router) | "AMU 2" | not stated |
| LSPKR | Cockpit loudspeakers | — | aural device | Architecture diagram shows **2 loudspeakers per AMU = 4 total**; note: "EACH FWS APPLICATION MANAGES THROUGH THE 2 AMUs A PAIR OF LOUDSPEAKERS, ONE ON EACH SIDE." L1 architecture diagram shows 2 | cockpit ("one on each side") |
| AG_L | Visual Attention Getters, LH | — | visual indicator | 1 LH unit containing MASTER WARN + MASTER CAUT | LH glareshield (from illustration) |
| AG_R | Visual Attention Getters, RH | — | visual indicator | 1 RH unit containing MASTER WARN + MASTER CAUT | RH glareshield (from illustration) |
| MW | MASTER WARN light / pushbutton | MASTER WARN | visual indicator + control | 2 (one per attention-getter unit); legend "MASTER WARN", red | glareshield |
| MC | MASTER CAUT light / pushbutton | MASTER CAUT | visual indicator + control | 2 (one per attention-getter unit); legend "MASTER CAUT", amber | glareshield |
| CMS | Central Maintenance System | CMS | maintenance computer/application | 1; shown in "OPEN WORLD" | — |
| NSS | (not expanded in the notes) — box labelled "NSS" containing CMS | NSS | network/server domain | 1 (Time Limited Items diagram) | — |
| OMS | (not expanded in the notes) — "OMS HMI DISPLAY (POST FLIGHT REPORT)" | OMS | display / maintenance HMI | 1 | — |
| SCIs | (not expanded in the notes) — "SCIs" block between CMS and ADCN in the OPEN WORLD | SCI | network gateway | plural | — |
| RMP | Radio & Audio Management Panels | RMPs | control panel | plural ("any RMP"); carries the **RST (ReSeT) key** | cockpit pedestal (photo) |
| ECAM | Electronic Centralized Aircraft Monitoring | ECAM | display concept | — | — |
| MEL/MMEL | Minimum Equipment List / MMEL | MEL, MMEL | documentation reference | — | — |
| BRT_PNL | Display brightness panel (PFD DU, PFD/ND, ND DU, OIT, DU RECONF, MFD DU) | — | control panel | 1 (shown in L2c "GENERAL") — **not an FWS control**, listed for completeness | lateral console (photo) |

Acronyms expanded verbatim in the L1 architecture legend box:
> ADCN : Avionics Data Communication Network · CDS : Control and Display System · CMS : Central Maintenance System · ECAM : Electronic Centralized Aircraft Monitoring · ECP : ECAM Control Panel · LRM : Line Replaceable Module · LRU : Line Replaceable Unit
Additional expansions in L1 p.27: **FWS : Flight Warning System · SD : System Display**.

---

## 0.2 TOPOLOGY

Format: **from → via → to**

### Data acquisition (into the FWS)
| # | Path | Notes source |
|---|---|---|
| T1 | LRMs → ADCN (AFDX) → CPIOM-C1 / CPIOM-C2 (FWS Applications) | L2b p.60/61 |
| T2 | LRUs with AFDX interface → ADCN (AFDX) → CPIOM-C1 / CPIOM-C2 | L2b p.60/61 |
| T3 | LRUs (conventional) → **ARINC 429** (direct) → CPIOM-C1 / CPIOM-C2 | L2b p.60 |
| T4 | LRMs → **ARINC 429 direct BACKUP** → CPIOM-C1 / CPIOM-C2 (to overcome total loss of ADCN) | L2b p.60/61 |
| T5 | LRUs with AFDX interface → **ARINC 429 direct BACKUP** → CPIOM-C1 / CPIOM-C2 | L2b p.60/61 |
| T6 | A/C systems (LRMs + LRUs) → ADCN → FWS *(L1 simplified view: "either via the ADCN or directly for some systems through a backup connection")* | L1 p.24/25 |

### Alert indication (out of the FWS)
| # | Path | Notes source |
|---|---|---|
| T7 | FWS Application → ADCN → CDS (ECAM part) → EWD / PFD / SD | L2b p.60/61 |
| T8 | FWS Application → **ARINC 429 BACKUP** (direct) → CDS (ECAM part) | L2b p.60/61 |
| T9 | FWS Application → **analog audio signals** → AMU 1 and AMU 2 → cockpit loudspeakers | L2b p.60/80/81 |
| T10 | FWS Application 1 → (via the 2 AMUs) → a pair of loudspeakers, one on each side | L2b p.81 note |
| T11 | FWS Application 2 → (via the 2 AMUs) → a pair of loudspeakers, one on each side | L2b p.81 note |
| T12 | FWS Application → **discrete signals** → Visual Attention Getters (MASTER WARN / MASTER CAUT, LH and RH) | L2b p.60/61 |

### Crew interface
| # | Path | Notes source |
|---|---|---|
| T13 | ECP → IOMs (**CAN buses**) → ADCN (**AFDX**) → FWS Applications | L2b p.60/61 |
| T14 | ECP → **discrete connections BACKUP** → CPIOM-C (FWS Applications) — "in case of ADCN loss, discrete connections keep most of its functions operational" | L2b p.60 |
| T14' | (L1 wording) ECP → **backup connection** → FWS; "in case of ADCN loss, a backup connection keeps **all** its functions operational" | L1 p.24 |

### Maintenance / audio call
| # | Path | Notes source |
|---|---|---|
| T15 | FWS → (BITE messages; alerts / cockpit effects; flight phases) → ADCN → CMS (for maintenance data consolidation/correlation) | L1 p.24, L2b p.60 |
| T16 | CMS ↔ SCIs ↔ ADCN (OPEN WORLD ↔ avionics) | L2b p.61 diagram |
| T17 | AMU 1 / AMU 2 → **CALL indication discrete (SELCAL/CALL, SATCOM)** → IOM-7 / IOM-8 → ADCN (AFDX) → FWS Applications | L2b p.80/81 |
| T18 | RMP **RST key** → AMU → resets **only the aural alert** | L2b p.80 |
| T19 | A/C systems → **class 4 alarms and timer reset signal** → FWS (Time Limited Item counters) | L2b p.84/85 |
| T20 | FWS → alerts + fault message + counter value → CMS (in NSS); A/C systems → fault message → CMS | L2b p.85 |
| T21 | FWS → alert (when timer expired) → CDS → ECAM-EWD ("MAINTENANCE TIME LIMITED ITEM") | L2b p.85 |
| T22 | CMS → OMS HMI DISPLAY (post flight report) | L2b p.85 |
| T23 | FWS flight phases → CDS (to compute the ECAM normal mode) and → CMS (contextual information about failures) | L1 p.26/27, L2b p.65 |

---

## 0.3 CONTROLS

### ECAM Control Panel — ECP (1135VM). Layout transcribed from the panel illustration.

Top row (left→right): `T.O CONFIG` · `C/L` · `✓` · `✓` · `ABN PROC` · `EMER CANC` (red legend, guarded/lit)
Left key group: `ENG` `BLEED` `PRESS` `EL/AC` / `APU` `COND` `DOOR` `EL/DC` / `VIDEO`
Left lower: `CLEAR` · `RCL LAST`
Centre: `↑` (up arrow) / `↓` (down arrow) / `STS`
Right key group: `FUEL` `HYD` `C/B` / `WHEEL` `F/CTL` `ALL`
Right lower: `MORE` · `RCL` · `CLEAR`
Knobs (bottom): `VIDEO` · `EWD DU` (OFF↔BRT) · `SD DU` (OFF↔BRT)

| Control | Legend on panel | Positions / action | What it commands (per the notes) |
|---|---|---|---|
| T.O CONFIG | `T.O CONFIG` | pushbutton | *Not described in these notes.* (Take-off configuration test; see §0.8 GAP-1) |
| C/L | `C/L` | pushbutton | Manually calls the **C/L Menu page**, which lists and designates the checklists to be done at the different flight phases. |
| Tick key ×2 | `✓` | pushbutton (two identical keys) | **Validate**: validating the designated line calls the selected C/L; validating the «ACTIVATE» line activates a Supplementary Abnormal Procedure; un-ticking the ACTIVE line deactivates it; used to manually confirm actions for **non-sensed items**. |
| ABN PROC | `ABN PROC` | pushbutton | Manually activates the **Supplementary Abnormal Procedures Menu page** on the EWD (organised in sub-menus). |
| EMER CANC | `EMER CANC` (red) | pushbutton | **Level 1 / Level 2 alert:** cancels the associated display, the audio signal and the MASTER CAUT light. **Level 3 alert:** cancels **only** the audio signal and the MASTER WARN light. Also manually deactivates a Supplementary Abnormal Procedure. Cancelled cautions are listed on the Status More Info page ("CANCELLED CAUTION"). |
| ENG | `ENG` | system page key | Calls the ENG system (synoptic) page on the SD. |
| BLEED | `BLEED` | system page key | Calls the BLEED page. |
| PRESS | `PRESS` | system page key | Calls the PRESS page. |
| EL/AC | `EL/AC` | system page key | Calls the electrical AC page. |
| APU | `APU` | system page key | Calls the APU page. |
| COND | `COND` | system page key | Calls the COND page. |
| DOOR | `DOOR` | system page key | Calls the DOOR page. |
| EL/DC | `EL/DC` | system page key | Calls the electrical DC page. |
| FUEL | `FUEL` | system page key | Calls the FUEL page. |
| HYD | `HYD` | system page key | Calls the HYD page. |
| WHEEL | `WHEEL` | system page key | Calls the WHEEL page (shown as the SD page for the BRAKES A-SKID level 2 example). |
| F/CTL | `F/CTL` | system page key | Calls the F/CTL page. |
| C/B | `C/B` | system page key | Calls the circuit-breaker page. |
| ALL | `ALL` | pushbutton | *Function not described in these notes.* (See §0.8 GAP-2) |
| VIDEO | `VIDEO` | pushbutton | *Function not described in these notes.* (See §0.8 GAP-2) |
| STS | `STS` | pushbutton | **Access to the Status Page** on the SD (manual call). The "STS" reminder appears at the bottom of the memos/limitations page on the EWD when the Status page is not empty. |
| MORE | `MORE` | pushbutton | **Access to the MORE page** — "CLICK ON THE 'MORE' BUTTON ON THE ECP TO ACCESS TO THE STATUS MORE INFO PAGE". |
| RCL | `RCL` | pushbutton | **Recall cleared procedures** / recall the automatic alert displays. |
| RCL LAST | `RCL LAST` | pushbutton | Recall (last). *Distinct function from RCL is not described.* (See §0.8 GAP-2) |
| CLEAR (left) | `CLEAR` | pushbutton | **Manual warning inhibition (CLEAR)** — lets the crew cancel the alert presentation when corrective actions have been done; on a normal C/L page returns to the C/L Menu page; on a deferred-procedure page returns to the C/L Menu page; in the Supplementary Abnormal Procedures menu, navigates back to the previous menu level. |
| CLEAR (right) | `CLEAR` | pushbutton | Same legend, second CLEAR key (right-hand side of the panel). |
| ↑ / ↓ | `↑` `↓` | arrow pushbuttons | Move the designation frame / navigate lines (the notes state "The designation frame can be manually moved by the crew"; they do not name the arrow keys explicitly — see §0.8 GAP-3). |
| EWD DU knob | `EWD DU`, `OFF` … `BRT` | rotary, OFF → BRT | EWD display-unit brightness / OFF. |
| SD DU knob | `SD DU`, `OFF` … `BRT` | rotary, OFF → BRT | SD display-unit brightness / OFF. |
| VIDEO knob | `VIDEO` | rotary | Video brightness (implied by placement; not described). |

### Controls elsewhere

| Control | Legend | Location | Action |
|---|---|---|---|
| MASTER WARN pushbutton ×2 | `MASTER WARN` (red) | LH and RH attention-getter units, glareshield | Red-**flashing** on Level 3 alert. Extinguished by EMER CANC (which cancels the audio signal and the MASTER WARN light for Level 3). The notes do **not** describe pressing it (see §0.8 GAP-4). |
| MASTER CAUT pushbutton ×2 | `MASTER CAUT` (amber) | LH and RH attention-getter units, glareshield | Amber **steady** on Level 2 alert. Cancelled by EMER CANC for Level 1/2. Pressing action not described (GAP-4). |
| RST key | `RST` | any Radio & Audio Management Panel (RMP) | "When the crew push the ReSeT key on any RMP, it resets **only the aural alert**." |
| C/L page items | `COMPLETE` , `RESET` , `CLEAR` | soft items on the EWD C/L page | «C/L COMPLETE» manually declares a normal C/L complete → the C/L page is automatically deactivated and frozen in its current state; the C/L title turns from cyan to grey in the C/L Menu and the C/L items are greyed. «RESET» manually resets the whole content of a C/L. «CLEAR» returns to the C/L Menu page. |
| Supplementary Abnormal Procedure item | `ACTIVATE` / `ACTIVE` | soft line on the EWD | Validating the «ACTIVATE» line below the heading activates the selected failure's procedure; un-ticking the ACTIVE line at the top deactivates it. |

---

## 0.4 LOGIC (IF / THEN, with priority)

### L-A. Alert level classification
| Rule | IF | THEN (class) |
|---|---|---|
| A1 | Emergency situation requiring an **immediate reaction** of the crew — A/C in dangerous configuration or limit flight conditions (e.g. OVERSPEED), or system failure (e.g. ENGINE/APU FIRE, EXCESS CABIN ALT) | **Level 3 — WARNING** ("emergency configuration…") |
| A2 | Abnormal situation of the aircraft where **immediate crew awareness** is required but **not** immediate crew corrective action; the crew must decide how soon action has to be taken | **Level 2 — CAUTION** ("abnormal configuration…") |
| A3 | Configuration requiring **crew monitoring**; mainly failures leading to a loss of redundancy or performance degradation of a system (e.g. loss of FUEL TANK PUMP LH **or** RH but not both) | **Level 1 — CAUTION** ("configuration to monitor…") |

### L-B. Alert activation (aural + visual outputs)
| Level | Aural | Attention getters | EWD | SD |
|---|---|---|---|---|
| **3** | Continuous Repetitive Chime (CRC) **or** a specific sound **or** a synthetic voice, via cockpit loudspeakers | **Both MASTER WARN** lights, **red flashing** | **Red** warning message (generally) | Automatic display of the affected system synoptic ECAM page, **when existing** |
| **2** | **Single chime**, via cockpit loudspeakers | **Both MASTER CAUT** lights, **amber steady** | **Amber** caution message (generally) | Automatic display of the affected system synoptic ECAM page, **when existing** |
| **1** | **No chime** — does not trigger any aural attention getter | **None** — does not trigger any visual attention getter | **Amber** caution message | Automatic display of the affected system synoptic ECAM page, **when existing** |

### L-C. Failure categorisation and EWD display effect
| Rule | IF | THEN classification | THEN EWD display characteristics |
|---|---|---|---|
| C1 | Failure affects an isolated system or item of equipment **without affecting another one** (L1 example: TR failure; L2a example: Main fuel pump failure) | **Independent failure** | red **or** amber message; **system indication underlined** |
| C2 | Failure of a system/equipment which **causes the loss of other systems or equipments** (e.g. green hydraulic system failure) | **Primary failure** | red **or** amber message; system indication underlined; **warning text surrounded** (boxed) |
| C3 | Loss of a system/equipment **resulting from a primary failure** (e.g. loss of spoilers 2, 4, 6, 8) | **Secondary failure** | **amber asterisked message** (`*` prefix) |

### L-D. Priority and inhibition
| Rule | Statement |
|---|---|
| D1 | Priority order for display / attention getters / aural announcements: **Level 3 alerts > Level 2 alerts > Level 1 alerts**. |
| D2 | "The most critically classified alerts have preeminence over less critically classified alerts and the last has preeminence over prior alerts of the same criticism." Level 3 has priority over Level 2 and Level 1. |
| D3 | **Within each level an order of priority between warnings is also defined** (WARNINGS PRIORITY LIST for L3; CAUTIONS PRIORITY LIST for L2 and for L1). Alerts are sent to the CDS **from higher to lower priority order**. |
| D4 | Several warning messages with their relevant procedures may be displayed **within the limit of the available area on the EWD**. They are **always displayed in the same order**, which is **not dependent on the chronology** of occurrence. |
| D5 | **Two different sounds cannot be broadcast at the same time**; **two different synthetic voices cannot be broadcast at the same time**; **but one sound and one synthetic voice can be broadcast together**. |
| D6 | **The MASTER WARN and MASTER CAUT lights can come on simultaneously.** |
| D7 | Inhibition function 1 — *proper alerts only when necessary*: a warning or indication which has no signification in a given configuration is not activated (e.g. hydraulic low-pressure warning is inhibited before engine starting) → **"misleading warnings inhibition"**. |
| D8 | Inhibition function 2 — *avoid alerts without interest for a flight phase*: the inhibition logic filters the presentation of alerts **according to the flight phase**, knowing that the flight is divided into **12 phases** → **"warnings inhibition related to flight phase"**. |
| D9 | Inhibition function 3 — *let the crew cancel alerts presentation when corrective actions have been done* → **CLEAR function** ("warning manual inhibition (CLEAR)"). |
| D10 | **During takeoff and landing phases, lots of warnings and cautions are inhibited** to avoid nuisances and useless workload to the crew. This information is given in **MAGENTA** in the memo list presented on the EWD: **"T.O INHIB"** and **"LDG INHIB"**. |
| D11 | **EMER CANC:** for a Level 1 or Level 2 alert → cancels the associated display, the audio signal **and** the MASTER CAUT light. For a Level 3 alert → cancels **only** the audio signal and the MASTER WARN light. |
| D12 | Cancelled cautions are recorded and listed as **"CANCELLED CAUTION"** on the **Status More Info** page. |

### L-E. Flight-phase computation and transitions
| Rule | Statement |
|---|---|
| E1 | The FWS computes the flight phases according to: **engine parameters, computed air speed, altitude, gear compressed / not compressed information from the L/G system**. |
| E2 | **If the data are not available to compute the flight phases, the FWS selects by default the cruise phase (8).** |
| E3 | Flight phases are used (a) by the **CDS** to compute the **ECAM normal mode**, (b) by the **FWS itself to inhibit**, during critical flight phases, alerts related to non-critical flight failures, and (c) to provide **contextual information about failures to the CMS**. |
| E4 | Phase transitions (arrow annotations on the flight-phase bar) — see §0.7 table N-1. |

### L-F. Checklist / procedure sequencing
| Rule | Statement |
|---|---|
| F1 | Normal checklists (C/L) that can be carried out at different flight phases are implemented into the FWS. The crew chooses the related checklist and its associated procedures on the EWD. |
| F2 | For **non-sensed items**, actions are **manually confirmed through the ECP**. For **sensed items**, an **automatic feedback** is given. |
| F3 | The **C/L Menu page** is either manually called (C/L pushbutton) **or automatically activated**. It lists and designates the C/L that must be done during the different flight phases. |
| F4 | Auto-activation case 1: **when the last failure message (independent, primary, secondary) is cleared on the EWD, AND there is at least one active deferred procedure.** |
| F5 | Auto-activation case 2: **in approach phase, below 2000 ft**, when the baro-corrected altitude is selected by the crew **or** when slats are extended, **AND** there is at least one active deferred procedure. |
| F6 | When the C/L menu page is activated, the **cyan designation frame** is automatically located on the **first incomplete C/L appearing after the last complete C/L**. The frame can be manually moved by the crew. Validating (tick pushbutton) the designated line calls the selected C/L. |
| F7 | «C/L COMPLETE» manually declares a normal C/L complete → the C/L page is automatically deactivated and **frozen in its current state**; the C/L title turns from **cyan to grey** in the C/L Menu and the C/L items are greyed. |
| F8 | «RESET» manually resets the whole content of a C/L. «CLEAR» on a normal C/L page returns to the C/L Menu page. |
| F9 | For some alerts, some procedure actions are **deferred to a more appropriate phase of flight** and are contained in a **deferred procedure**. |
| F10 | Deferred procedures are of **three types: APPROACH, LANDING and PENDING**; they are displayed at **fixed positions in the C/L menu**, only if some deferred procedures of the related type are really active. |
| F11 | A deferred-procedure page is manually activated from the C/L Menu page. When **all** items of a deferred procedure are done, its **title turns from amber to white** in the C/L Menu. CLEAR on a deferred-procedure page returns to the C/L Menu page. |
| F12 | **Supplementary Abnormal Procedures**: emergency/abnormal procedures **not sensed by the systems** (e.g. «COCKPIT WINDOW CRACKED»). Pushing **ABN PROC** activates the Supplementary Abnormal Procedures Menu page, organised in sub-menus; CLEAR navigates back to the previous menu level. |
| F13 | In the Supplementary Abnormal Procedures Menu, **procedure titles at the top are red or amber alerts requiring quick access**; the other lines at the bottom in **white** are sub-menu titles related to less critical warnings (generally amber cautions, and eventually red warnings). |
| F14 | Activation is performed by **validating the «ACTIVATE» line** located below the heading and title of the selected failure. Once activated, Supplementary Abnormal Procedures are **displayed and processed in the same way as the other warnings** on the Alert/Supplementary Abnormal Procedures page on the EWD. |
| F15 | Manual deactivation of a Supplementary Abnormal Procedure: by **EMER CANC** function key on the ECP, **or** by **un-ticking the ACTIVE line** at the top of the procedure. |
| F16 | If a Supplementary Abnormal Procedure is **cleared** and the crew tries to re-access it through the Supplementary Abnormal Procedure Menu, **it will automatically be recalled**. |

### L-G. Status page rules
| Rule | Statement |
|---|---|
| G1 | The **Status page mainly appears once the crew has cleared all the pages related to the current warning/caution management**, or **upon manual call** (STS). |
| G2 | If the **Status page is not empty**, an **«STS» reminder is displayed at the bottom of the memos/limitations page on the EWD**. |
| G3 | The Status page gathers: the **«LIMITATIONS» reminder** (recalling the presence of limitations on the EWD and the PFD); the **deferred-procedure reminder** (wording depends on the category of active deferred procedures — e.g. `DEFERRED PROCs : ALL PHASES. APPR. LDG`); the **inoperative systems** of the types **«ALL PHASES»** and **«APPR & LDG»**; and the **«MORE» reminder** at the bottom indicating the presence of messages in the Status More Info page. |
| G4 | The **Status More Info** page gathers: inoperative systems of the type **«REDUND LOSS»** (functions no longer redundant); the **cancelled cautions list** (cautions cancelled by the EMER CANC function); and some complementary information. |
| G5 | In normal operation, the **EWD, PFD and SD** can display status messages: an operational summary of the aircraft condition; an explanation of possible auto land capability downgrading; indications of the aircraft status (inoperative systems) following all failures, some affecting the flight and some not (redundancy loss); general contents, limitations (speed, altitude), peculiar or emergency deferred procedures, information, etc. |

### L-H. Memos and limitations
| Rule | Statement |
|---|---|
| H1 | The FWS generates **all memos indications**, which inform the crew about the A/C configuration following **routine crew action**. |
| H2 | **All memos generated by the FWS are displayed on the EWD.** In addition, the memos **directly related to the flight** are also displayed on the **PFDs lower zone** (e.g. `ENG A. ICE`). |
| H3 | **All memo information are strings of twenty characters maximum.** |
| H4 | The FWS generates **all limitations indications**, informing the crew about the A/C flight capabilities. **All limitations generated by the FWS are displayed on the EWD**; limitations **related to the flight** are also displayed on the **PFDs lower zone** (e.g. speed limitation). |
| H5 | Limitations on the EWD are split into **«ALL PHASES»** and **«APPR & LDG»** columns. |
| H6 | The Memos/limitations page on the EWD indicates the **active limitations** — messages indicating operational constraints following a degradation of the aircraft capability. **Up to 8 of them can also be displayed on the PFD.** |

### L-I. Redundancy / degraded-network logic
| Rule | Statement |
|---|---|
| I1 | The FWS is "mainly composed of **two** FWS Applications hosted in the CPIOM-C1 and C2". Both acquire data from A/C systems. *(The notes do not state master/slave, cross-monitoring or failover behaviour — see §0.8 GAP-5.)* |
| I2 | **Each FWS application manages, through the 2 AMUs, a pair of loudspeakers, one on each side.** |
| I3 | **On total loss of the ADCN:** LRMs and LRUs with AFDX interface are **also directly connected in ARINC 429** to the CPIOMs-C, so data acquisition continues; warning/caution messages reach the CDS via the **ARINC 429 backup**; the ECP keeps **most of its functions** operational via **discrete connections** (L2b). L1 states the ECP backup keeps **all** its functions operational. |
| I4 | Aural signals to the loudspeakers are **analog** signals from the FWS to the AMUs — i.e. they do not transit the ADCN. Attention getters are driven by **discrete** signals — likewise independent of the ADCN. |

### L-J. Time Limited Items (Level 3 depth)
| Rule | Statement |
|---|---|
| J1 | The TIME LIMITED ITEM philosophy monitors **faulty items which are minor faults and which are time limited**, enabling the airline to manage repair within an airworthiness-approved time limit **without cockpit effect triggering**. |
| J2 | Such faults are detected by the systems **BITE** and known as **class 4 messages**. **Several class 4 faults in the same system trigger only one counter.** |
| J3 | Systems transmit these faults to the FWS, which **increments its specific timer counters**. Counters are reported to the CMS and displayed in the **post flight report**: `"TIME LIMITED ITEM / Remain time before display XXX Hrs"`. |
| J4 | **IF the time counter expires (reaches Tmax) THEN the FWS triggers the ECAM caution "MAINTENANCE TIME LIMITED ITEM".** |
| J5 | **This message is presented on the ECAM in flight phase 1 and 12 only** (generic warning message provided **on the ground**, during flight phases **1 or 12**, to minimise cockpit effect for multiple Class 4 faults and to allow a unique MMEL entry point). In this case **dispatch can be granted under the MEL**. |
| J6 | **Warning reset:** once a counter has been triggered it can be reset to 0 by an emission of a **warning reset signal from the subscriber system**, emitted after a **successful System Test and/or interactive BITE test**. The timer counter is then set to zero. |
| J7 | **Spurious failure:** if a failure disappears by itself without maintenance action, the related counter **starts to decrement for a maximum of 100 FH, then drops to 0**. If during this period the defect appears again, the counter **increments again**. |

---

## 0.5 STATES

### S-A. System / architecture configurations
| State | Definition (from the notes) | Implication for the sim |
|---|---|---|
| **NORMAL** | Both FWS Applications (CPIOM-C1 and CPIOM-C2) available; ADCN available; ECP via IOMs/ADCN; CDS via ADCN. | All acquisition paths active; both loudspeaker pairs, both attention-getter units, full ECP function. |
| **SINGLE FWS APPLICATION LOST** | One of the two FWS Applications (CPIOM-C1 **or** C2) unavailable. | The remaining application still manages **a pair of loudspeakers, one on each side** through the 2 AMUs (I2). The notes give **no** further degradation statement — see GAP-5. |
| **BOTH FWS APPLICATIONS LOST** | Not described in the notes. | GAP-6 — must be shown as "(assumed)" if simulated. |
| **ADCN LOSS (backup active)** | Total loss of the ADCN. | LRM / AFDX-LRU data reaches the CPIOMs-C over **ARINC 429 direct**; CDS driven over **ARINC 429 backup**; ECP over **discrete connections**, keeping **most** of its functions operational (L2b) / **all** (L1). Conventional LRUs are unaffected (they were always ARINC 429). |
| **AURAL RESET** | RST key pressed on any RMP. | Only the **aural** alert is reset; visual indications unchanged. |
| **EMER CANC applied (L1/L2)** | EMER CANC pressed with a Level 1 or 2 alert active. | Display + audio + MASTER CAUT cancelled; caution appears in "CANCELLED CAUTION" on the Status More Info page. |
| **EMER CANC applied (L3)** | EMER CANC pressed with a Level 3 alert active. | **Only** audio + MASTER WARN cancelled; the red warning message and its procedure remain. |

### S-B. The 12 flight phases (state machine)
| Phase # | Verbatim name | Grouping | Entered on | Max duration stated |
|---|---|---|---|---|
| 1 | **PREFLIGHT** | — | (initial / after Last Engine Shutdown + 5 min) | — |
| 2 | **TAXI OUT** | — | **1st Engine Start** | — |
| 3 | **STEP 1** | **TAKE OFF** | **2nd Engine TO POWER** | — |
| 4 | **STEP 2** | **TAKE OFF** | **80 kts** | — |
| 5 | **STEP 3** | **TAKE OFF** | **V1** | — |
| 6 | **STEP 1** | **CLIMB** | **Lift Off** | — |
| 7 | **STEP 2** | **CLIMB** | **Lift Off + 400 ft** | **FP6 Max = 15 sec** (i.e. phase 6 lasts at most 15 s before phase 7) |
| 8 | **CRUISE** | — | **1500 ft** | **FP7 Max = 2 min** |
| 9 | **APPROACH** | — | **800 ft** | — |
| 10 | **LANDING** | — | **Touch Down** | **FP9 Max = 3 min** |
| 11 | **TAXI IN** | — | **80 kts** | — |
| 12 | **POSTFLIGHT** | — | **Last engine Shutdown** | **FP12 Max = 5 min** — ends at **Last Engine Shutdown + 5 min** |

*(Transition labels are transcribed exactly as annotated under the flight-phase bar, L2b p.65. The "FPn Max" annotations are printed with the transition that terminates phase n.)*

Phase-related behaviour:
- **Default:** if data are not available to compute the flight phases → **phase 8 (CRUISE)** is selected by default.
- **Take-off and landing phases:** many warnings and cautions are inhibited; shown as magenta **T.O INHIB** / **LDG INHIB** in the EWD memo list.
- **Phases 1 and 12 (on ground):** the only phases in which the "MAINTENANCE TIME LIMITED ITEM" caution is presented.
- Phases 3/4/5 are named STEP 1/2/3 of **TAKE OFF**; phases 6/7 are named STEP 1/2 of **CLIMB** — the number-plus-group pair is what makes each name unique.

### S-C. Alert-presence states
| State | Live indications |
|---|---|
| **No alert** | EWD shows engine parameters + LIMITATIONS + memos; SD shows the ECAM normal-mode page for the current flight phase (e.g. CRUISE page); no attention getters, no chime. |
| **Level 1 active** | Amber caution on EWD; SD affected-system page if existing; **no** chime, **no** attention getter. |
| **Level 2 active** | Amber caution on EWD; **SINGLE CHIME**; both MASTER CAUT amber steady; SD affected-system page if existing. |
| **Level 3 active** | Red warning on EWD; **CRC or specific sound or synthetic voice**; both MASTER WARN red flashing; SD affected-system page if existing. |
| **All alerts cleared** | Status page mainly appears; if not empty, **STS** reminder at bottom of EWD memos/limitations page. |
| **Deferred procedures pending** | C/L Menu auto-activates per F4/F5; deferred-procedure reminder on the Status page (`DEFERRED PROCs : ALL PHASES. APPR. LDG`). |

---

## 0.6 INDICATIONS

### Visual attention getters
| Indicator | Legend | Colour / behaviour | Trigger |
|---|---|---|---|
| MASTER WARN (LH + RH) | `MASTER WARN` | **red, flashing** | Level 3 alert |
| MASTER CAUT (LH + RH) | `MASTER CAUT` | **amber, steady** | Level 2 alert |
| (both) | — | **can come on simultaneously** | concurrent L3 + L2 |
| (none) | — | not triggered | Level 1 alert |

### Aural indications — full list from L2b pp.82–83

**General sounds**
- the **Single Chime (SC)** — related to the **cautions**
- the **Continuous Repetitive Chime (CRC)** — related to **most of the warnings**
- the **specific sounds** for instinctive reactions
- the **synthetic voices**

**Specific sounds**
| Sound | Used for |
|---|---|
| **cavalry charge** | involuntary Autopilot (AP) disconnect |
| **cavalry charge** | voluntary AP disconnect |
| **triple click** | landing capability change |
| **buzzer** | calls and SELCAL |
| **"C" chord** | altitude alert |
| **RING** | ATC messages |

**Synthetic voices**
| Announcement | Used for |
|---|---|
| (radio-altitude callouts) | reporting of significant radio altitudes |
| **HUNDRED ABOVE**, **MINIMUM**, **PLUS_HUNDRED** | decision height |
| **WINDSHEAR-WINDSHEAR-WINDSHEAR** | windshear |
| **SPEED-SPEED-SPEED** | — |
| **RETARD** (single or continuous), **TEN RETARD**, **TWENTY RETARD** | retard |
| **STICK PRIORITY** (PRIORITY LEFT, PRIORITY RIGHT), **V_ONE**, **DUAL INPUT** | stick priority / V1 / dual input |
| **PITCH-PITCH** | pitch attitude warning |
| **BANK-BANK** | bank angle warning |
| **RUNWAY TOO SHORT** | included in **BTV** option |

**Hybrid aural messages** (a sound + a synthetic voice)
| Message | Composition |
|---|---|
| **CRICKET STALL** | synthetic voice **"STALL-STALL"** + sound **CRICKET** — for stall warning |
| **COCKPIT DOOR** | sound **CKPT DOOR** + synthetic voice **"DOOR PLEASE"** — for cockpit door emergency opening |
| **TIME MARKER** | sound **TIME MKR** + synthetic voice **"TIME MARKER"** |
| **CPNY ALERT**, **CPNY MSG**, **CALL CPNY** | each composed of a specific sound (chime) and a synthetic voice — shown on the summary chart as "COMPANY ALERT", "COMPANY MESSAGE", "CALL COMPANY" |

Summary chart (L2b p.83) groups them as **SOUNDS**: CAVALRY CHARGE · CONTINUOUS REPETITIVE CHIME · SINGLE CHIME · BUZZER · C CHORD · TRIPLE CLICK — **SYNTHETIC VOICES**: WINDSHEAR-WINDSHEAR-WINDSHEAR · RADIO HEIGHT, HUNDRED ABOVE, MINIMUM, RETARD · PRIORITY LEFT & RIGHT · DUAL INPUT · SPEED-SPEED-SPEED · BANK-BANK · PITCH-PITCH · RUNWAY TOO SHORT — **HYBRID AURAL MESSAGES**: Sound CRICKET & Synthetic Voice STALL-STALL · Sound COCKPIT DOOR & Synthetic Voice DOOR PLEASE · Sound & Synthetic Voice TIME MARKER · Sound & Synthetic Voice COMPANY ALERT · Sound & Synthetic Voice COMPANY MESSAGE · Sound & Synthetic Voice CALL COMPANY.

Also aural: **aural announcements in approach** are listed as a normal-operation FWS function (L1/L2a General).

### EWD content
| Zone / item | Content |
|---|---|
| Engine parameters (top) | THR %, N1 %, EGT °C per engine; FLEX / temperature; PACKS/NAI — *(RR parameters used on EWD "as an example")* |
| **LIMITATIONS** block | Two columns: **ALL PHASES** and **APPR & LDG**. Example content: `MAX SPD : 200 KT` \| `LDG DIST x 1. 4`, `CAT 3 SINGLE ONLY` |
| Memo zone | All memos. Example: `SEAT BELTS`, `NO SMOKING`, `ENG A. ICE`. Take-off/landing memo block example: `T.O` `-SIGNS` `-CABIN READY` `-SPLRs ARM` `-FLAPs.........T.O` `-AUTO BRAKE....RTO` `-T.O CONFIG....TEST` |
| Inhibition memos | **T.O INHIB** and **LDG INHIB** in **MAGENTA** |
| Warning / caution zone | Red warning messages and amber caution messages with their procedures, in fixed priority order |
| Independent failure example | `FUEL FEED TK 1 MAIN PMP FAULT` (underlined system indication) with procedure line `-FEED TK 1 MAIN PMP ..............OFF` |
| Primary failure example | `HYD GREEN SYS LOW PRESS` (underlined + surrounded) |
| Secondary failure example | `* F/CTL` (amber asterisked) |
| Level 3 EWD example | `SMOKE IFE BAY SMOKE` / `LAND ASAP` / `-IFE ...........OF` / `-CKPT / CABIN COM ..........ESTABLISH` / `CLEAR` |
| Level 2 EWD example | `BRAKES A-SKID FAULT ON ONE BODY L/G ON RIGHT BODY L/G` / `TAXI WITH CARE` / `LDG DIST : COMPUTE` (SD auto-calls the **WHEEL** page) |
| Level 1 EWD example | `ELEC STATIC INV FAULT` / `CLEAR` |
| **STS** reminder | Displayed at the bottom of the memos/limitations page when the Status page is not empty |
| C/L Menu page | `CHECKLISTS` : `BEFORE START`, `AFTER START`, `BEFORE TAKEOFF`, `AFTER TAKEOFF / CLIMB`, `APPROACH`, `LANDING`, `AFTER LANDING`, `PARKING`, `SECURING AIRCRAFT` — with tick boxes and a cyan designation frame |
| C/L page example | `APPROACH` : `☑ ECAM STATUS CHECK`, `BRIEFING...................CONFIRM`, `V BUG.........................SET`, `SEAT BELTS ON`, `BARO.........................SET`, `MDA / DH.....................SET`, `COMPLETE`, `RESET` |
| ABN PROC menu | `ABNORMAL PROC` — red: `SMOKE / TOXIC FUMES REMOVAL`, `EMER DESCENT`, `DITCHING`, `FORCED LANDING`, `ON GROUND EMERGENCY EVAC`; white sub-menus: `FIRE PROTECTION`, `FLIGHT CONTROLS`, `INDICATING / RECORDING`, `LANDING GEAR`, `NAVIGATION`, `POWER PLANT`, `MISCELLANEOUS`, `OPERATING TECHNIQUES`, `AIRLINE PROCEDURES` |
| Time Limited Item | `MAINTENANCE TIME LIMITED ITEM` (amber ECAM caution, flight phases 1 and 12 only) |

### SD content
| Page | Content |
|---|---|
| **STATUS page** | `STATUS` header; `DEFERRED PROCs : ALL PHASES. APPR. LDG`; `LIMITATIONS`; `INFO` block — example `INR TKs XFR BY GRVTY ONLY`, `OUTR TKs XFR BY GRVTY ONLY`, `F/O BARO REF : STD ONLY`, `SLATS SLOW`, `FLAPS SLOW`; `INOP SYS` block in two columns **ALL PHASES** / **APPR&LDG** — example `PRIM 2+3`, `ENG 2 REV`, `SEC 2+3`, `FUEL ALL FEED PMPs`, `VHF 1+2+3`, `RA SYS A+B+C`, `FMS2` \| `AUTO CALLOUT`, `SLAT SYS 2`, `FLAP SYS 2`, `INR TKs MOST PMPs`; `MORE` reminder at the bottom |
| **STATUS MORE INFO page** | `STATUS MORE`; `INOP SYS REDUND` (system redundancy loss) — example `YAW DAMPER 1`; `CANCELLED CAUTION` (list of alerts cancelled with EMER CANC P/B) — example `HYD GREEN RSVR OVHT`; complementary/additional info to procedure — example `IF HYDRAULIC IS RECOVERED CORRESPONDING LIMITATIONS WILL NOT APPLY` |
| **Affected-system synoptic page** | Automatically displayed on any alert level "when existing" (e.g. WHEEL page for the A-SKID caution) |
| **ECAM normal mode page** | Selected by the CDS from the FWS flight phase — example `CRUISE` page |

### PFD content driven by the FWS
- **Flight-related memos** in the PFD lower zone — example `ENG A. ICE`.
- **Flight-related limitations** in the PFD lower zone — example `MAX SPD VLE = 200 KTS`.
- **Up to 8** limitations can also be displayed on the PFD.

### CMS / maintenance indications
- FWS **BITE messages**; **alerts / cockpit effects** and **flight phases** sent to the CMS for maintenance data consolidation/correlation.
- Post flight report on the **OMS HMI DISPLAY**: `TIME LIMITED ITEM / Remain time before display XXX Hrs`.

---

## 0.7 NUMBERS — whitelist of "specified" values

### N-1 Flight phases
| Item | Value |
|---|---|
| Number of flight phases | **12** |
| Phase names | 1 PREFLIGHT · 2 TAXI OUT · 3 TAKE OFF STEP 1 · 4 TAKE OFF STEP 2 · 5 TAKE OFF STEP 3 · 6 CLIMB STEP 1 · 7 CLIMB STEP 2 · 8 CRUISE · 9 APPROACH · 10 LANDING · 11 TAXI IN · 12 POSTFLIGHT |
| Default phase when data unavailable | **8 (cruise)** |
| Transition 1→2 | **1st Engine Start** |
| Transition 2→3 | **2nd Engine TO POWER** |
| Transition 3→4 | **80 kts** |
| Transition 4→5 | **V1** |
| Transition 5→6 | **Lift Off** |
| Transition 6→7 | **Lift Off + 400 ft** — **FP6 Max = 15 sec** |
| Transition 7→8 | **1500 ft** — **FP7 Max = 2 min** |
| Transition 8→9 | **800 ft** |
| Transition 9→10 | **Touch Down** — **FP9 Max = 3 min** |
| Transition 10→11 | **80 kts** |
| Transition 11→12 | **Last engine Shutdown** |
| Transition 12→1 | **Last Engine Shutdown + 5 min** — **FP12 Max = 5 min** |

### N-2 Quantities and identifiers
| Item | Value |
|---|---|
| FWS Applications | **2** (FWS Application 1, FWS Application 2) |
| Host computers | **CPIOM-C1**, **CPIOM-C2** (labelled 1 and 2) |
| Audio Management Units | **2** — **AMU 1**, **AMU 2** |
| Loudspeakers | **2 per AMU** on the architecture diagram (**4** total); "a pair of loudspeakers, one on each side" per FWS application; L1 architecture diagram shows **2** |
| IOMs named for CALL indication | **IOM-7**, **IOM-8** |
| Attention-getter units | **2** (LH and RH), each with `MASTER WARN` + `MASTER CAUT` → **4 lights** |
| ECAM Control Panel identifier | **1135VM** |
| Alert levels | **3** (Level 1, Level 2, Level 3) |
| Failure types | **3** (independent, primary, secondary) |
| Deferred-procedure types | **3** (APPROACH, LANDING, PENDING) |
| Memo string length | **twenty (20) characters maximum** |
| Limitations displayable on the PFD | **up to 8** |
| C/L Menu auto-activation altitude (approach) | **below 2000 ft** |
| Normal checklists listed | **9**: BEFORE START, AFTER START, BEFORE TAKEOFF, AFTER TAKEOFF / CLIMB, APPROACH, LANDING, AFTER LANDING, PARKING, SECURING AIRCRAFT |
| ABN PROC menu entries listed | **14** (5 red + 9 white, see §0.6) |
| Data buses named | **AFDX**, **ARINC 429**, **CAN** |

### N-3 Time Limited Items
| Item | Value |
|---|---|
| BITE message class monitored | **class 4** |
| Class-4 counter rule | several class 4 faults in the **same system** trigger **only one** counter |
| ECAM caution presented in flight phases | **1 and 12** |
| Spurious-failure counter decrement window | **maximum 100 FH**, then drops to 0 |
| Graph example 1 | **T MAX = 120** FH; failure at **20** FH; warning on ECAM at ≈**140** FH; repair action / system-BITE test OK at **160** FH; "MAX TIME AS PER MMEL" spans ≈140→160 FH |
| Graph example 2 | **T MAX = 200** FH; failure at **40** FH; failure disappeared at **200** FH; counter reaches 0 at **300** FH; "RESET TIME MAX 100 FH" |
| Post flight report string | `TIME LIMITED ITEM / Remain time before display XXX Hrs` |

### N-4 Numbers appearing on example screens (display content, not FWS parameters)
`MAX SPD : 200 KT` · `LDG DIST x 1. 4` · `CAT 3 SINGLE ONLY` · `MAX SPD VLE = 200 KTS` · secondary-failure example `loss of spoilers 2, 4, 6, 8` · `PRIM 2+3`, `SEC 2+3`, `VHF 1+2+3`, `RA SYS A+B+C`, `FMS2`, `SLAT SYS 2`, `FLAP SYS 2`, `ENG 2 REV`, `YAW DAMPER 1` · EWD engine example `FLEX 83.9 % 59°C`, `THR % 83.9` ×4, `N1 % 84.7` ×4, `EGT °C 751` ×4 · PFD example `QNH 1016`, `TBN 109.30`, `4.0 NM`, `3000`, `1260` · SD CRUISE page example `FF 4100 KG/H` ×4, `FU 20050 / 20050 / 20000 / 20000`, `FU TOTAL 80100 KG`, `LDG ELEVN 300 FT`, `DELTA P 0.0 PSI`, `AUTO CAB V/S 0 FT/MIN`, `AUTO CAB ALT 500 FT`, cabin temp `18 TO 24`, `TAT +10 °C`, `SAT +10 °C`, `13:28:00 GPS`, `GW 500000 KG`, `GWCG 40.0 %`, `FOB 246900 KG`, `ACTIVE ATC : LFBO`, `2 ADS CONNECTIONS`.
**These are screen-capture examples in the manual, not FWS specifications.** They may be reproduced verbatim as illustrative display content but must not be presented as FWS ratings.

---

## 0.8 GAPS (things the simulation needs that the notes do not state)

| # | Gap | Conservative assumption to display, tagged "(assumed)" |
|---|---|---|
| GAP-1 | **T.O CONFIG** key function is never described in these notes. | "(assumed) Initiates the take-off configuration test; the FWS checks the take-off configuration and announces the result." Label the key non-functional in the sim unless the instructor enables it. |
| GAP-2 | **ALL**, **VIDEO**, **RCL LAST** key functions are not described. | "(assumed) ALL = cycle through all system pages in sequence; VIDEO = select a video source on the SD; RCL LAST = recall the last cleared alert page." Mark all three as "(assumed)". |
| GAP-3 | The **↑ / ↓ arrow keys** are shown on the panel but never named in the text; the text only says "the designation frame can be manually moved by the crew". | "(assumed) The ↑ / ↓ keys move the cyan designation frame between selectable lines." |
| GAP-4 | Pressing **MASTER WARN / MASTER CAUT** is not described (only that they illuminate). | Model them as **indicators only** in the sim; if a press is offered, tag "(assumed) acknowledges the alert". Note the notes only give **EMER CANC** and the RMP **RST** key as the cancelling controls. |
| GAP-5 | **Redundancy behaviour between FWS1 (CPIOM-C1) and FWS2 (CPIOM-C2)** — master/slave, cross-comparison, automatic switchover, and what is lost on a single-application failure — is not stated. | "(assumed) The two applications run in parallel; loss of one leaves the alert function available, with the surviving application still driving one loudspeaker per side (per the stated pairing rule)." Do not claim any degradation the notes do not state. |
| GAP-6 | **Total loss of both FWS applications** is not described. | "(assumed) No FWS alert generation, no attention getters, no aural alerts, no automatic ECAM alert pages; the CDS/SD normal-mode function is a separate system." Present only as an instructor-injected extreme case. |
| GAP-7 | The exact **quantity of cockpit loudspeakers** is ambiguous (L1 diagram shows 2; L2b architecture diagram shows 4, i.e. 2 per AMU). | Model **4 loudspeakers (2 per side, 2 per AMU)** per the more detailed L2b diagram; label the count "(per L2b architecture diagram)". |
| GAP-8 | **Individual inhibition tables** (which specific alerts are inhibited in which phase) are not given — only the principle and the T.O INHIB / LDG INHIB memos. | Simulate inhibition **as a rule** ("this alert is inhibited in phases 3–7 (assumed set)") and label every specific inhibition mapping "(assumed, illustrative)". |
| GAP-9 | The **within-level priority lists** (WARNINGS PRIORITY LIST, CAUTIONS PRIORITY LIST) exist but their content is not given. | Use a fixed, visibly "(assumed)" ordering; teach the *rule* (fixed order, not chronological) rather than a specific list. |
| GAP-10 | **Timings** for CRC repetition rate, MASTER WARN flash rate, single-chime duration are not stated. | "(assumed) MASTER WARN flashes at ~1 Hz; CRC repeats continuously until cancelled; SC is a single ~1 s tone." Tag on screen. |
| GAP-11 | **Acronym expansions not given in the notes**: SCI, NSS, OMS, BTV, IFE, MMEL (used but not expanded), RMP (expanded only as "Radio & Audio Management Panels" in a diagram caption). | Show the acronym alone in the glossary with "(not expanded in the notes)". Do **not** substitute expansions from memory. |
| GAP-12 | **ECP physical location** and attention-getter/loudspeaker physical locations are not stated in words (only visible in cockpit photos). | "(assumed from the illustrations) ECP on the centre pedestal; attention getters on the LH and RH glareshield; loudspeakers one per side overhead." |
| GAP-13 | Whether the **two tick (✓) keys** are per-pilot or serve different functions is not stated. | "(assumed) Two identical validate keys, one for each pilot." |
| GAP-14 | Whether the **left CLEAR and right CLEAR** keys differ is not stated. | "(assumed) Two identical CLEAR keys, one per side of the panel." |
| GAP-15 | **Attention-getter and loudspeaker part/panel identifiers** are not given (only the ECP carries **1135VM**). | Omit identifiers rather than invent them. |
| GAP-16 | Level-3 aural selection logic — **when** CRC vs a specific sound vs a synthetic voice is used — is stated only as "either…or". | "(assumed, illustrative) CRC is the default Level-3 sound; specific sounds/voices are used for the instinctive-reaction alerts named in the aural list." |

---

## 0.9 LEARNING OUTCOMES (CAAS SAR-66 Cat B2, Level 2)

On completion of this simulation the learner will be able to:

**LO1 — Identify** the FWS line-replaceable architecture: the two FWS Applications and their host CPIOM-C1/C2, the ECP (1135VM), the IOMs, the AMUs, the loudspeakers, the visual attention getters, the CDS/ECAM display units and the CMS interface.

**LO2 — Trace** any alert from its data source (LRM / AFDX LRU / conventional LRU) through the acquisition path (ADCN-AFDX, ARINC 429, or the ARINC 429 direct backup) into a FWS Application and out to each cockpit peripheral (loudspeaker via AMU, attention getter via discrete, EWD/SD via CDS).

**LO3 — Predict**, for a given failure, its alert level (1/2/3) and its failure category (independent / primary / secondary), and state the exact aural, attention-getter, EWD and SD consequences of that level — including the EWD display characteristics (underlined, surrounded, asterisked).

**LO4 — Operate** the ECAM Control Panel to call system pages, the Status and Status More Info pages, the normal C/L menu and a checklist, and a Supplementary Abnormal Procedure; and to apply CLEAR, RCL and EMER CANC correctly for each alert level.

**LO5 — Explain** the flight-phase logic: name the 12 phases and their transition conditions, state the default phase when data are unavailable, and explain how the phase drives ECAM normal mode, alert inhibition (T.O INHIB / LDG INHIB) and CMS contextual data.

**LO6 — Isolate** a degraded FWS configuration (single FWS application lost, total ADCN loss) and state which paths remain, which backup carries the data, and which ECP functions survive.

---

## 0.10 MISCONCEPTIONS the simulation must expose

| # | Misconception | How the sim must break it |
|---|---|---|
| M1 | **"Level 1 is just a quieter Level 2."** Students expect every alert to chime and light something. | Inject a Level 1 fault (e.g. `ELEC STATIC INV FAULT`): **no chime, no attention getter**, only the amber EWD message and the SD page. Ask the student to predict first. |
| M2 | **"EMER CANC clears the warning."** Students assume EMER CANC removes a Level 3 warning like it removes a Level 2 caution. | Inject a Level 3 warning, let the student press EMER CANC: **only** the audio and MASTER WARN go; the red message and procedure stay. Then repeat with Level 2 — the display, audio and MASTER CAUT all go, and the caution reappears under `CANCELLED CAUTION` on the Status More Info page. |
| M3 | **"Warnings appear in the order they happen."** | Trigger two failures in a deliberately reversed chronological order; the EWD shows them in the **fixed priority order**, not the order of occurrence (rule D4). |
| M4 | **"Losing the ADCN kills the FWS."** Students conflate the network with the function. | Inject total ADCN loss: LRMs and AFDX LRUs still feed the CPIOMs-C over **ARINC 429 direct**, the CDS is driven over the **ARINC 429 backup**, and the ECP keeps **most** of its functions via **discrete connections**. Aural (analog to AMU) and attention getters (discrete) never used the ADCN at all. |
| M5 | **"Attention getters and loudspeakers hang off the ADCN like the displays."** | Signal-trace the aural path (FWS → analog → AMU 1/2 → loudspeakers) and the attention-getter path (FWS → discrete → MASTER WARN/CAUT) and show that neither passes through the ADCN. |
| M6 | **"A secondary failure is a second, separate fault."** | Inject the green hydraulic system failure: one **primary** failure (boxed, underlined) plus the **secondary** `* F/CTL` amber asterisked message for spoilers 2, 4, 6, 8 — one root cause, two message types. |
| M7 | **"The flight phase comes from a switch or from the FMS."** | Show that the FWS computes the phase from **engine parameters, computed air speed, altitude and gear compressed/not compressed**, and that removing those data drops the system to the **default cruise phase (8)** — which then changes which alerts are inhibited. |

---

## 0.11 DEFINITIONS & PRECEDENCE

### Operative definitions (in the notes' sense)

| Term | Definition as used by these notes |
|---|---|
| **Alert** | An indication generated by the FWS when a system failure or a configuration change is detected, or in case of A/C abnormal configuration. Alerts are classified in three levels according to the **importance** and the **urgency of the crew corrective actions required**. Alerts are identified as either **"Normal" alerts** (memos, autocall out, C/L) or **"failure-linked" alerts**. |
| **Warning** | A **Level 3** alert — an emergency situation requiring an **immediate reaction of the crew** (A/C in dangerous configuration or limit flight conditions, e.g. OVERSPEED; or system failure, e.g. ENGINE/APU FIRE, EXCESS CABIN ALT). Displayed as a **red** message, generally on the EWD. Corresponds to an "emergency configuration". |
| **Caution (Level 2)** | An alert for an **abnormal situation** of the aircraft where **immediate crew awareness is required, but not immediate crew corrective action**; the crew must decide how soon action has to be taken. **Amber** message. Corresponds to an "abnormal configuration". |
| **Caution (Level 1)** | An alert for a **configuration requiring crew monitoring**; mainly failures leading to a **loss of redundancy** or **performance degradation** of a system (e.g. loss of FUEL TANK PUMP LH **or** RH but not both). **Amber** message, **no** attention getter, **no** chime. Corresponds to a "configuration to monitor". **Note: in this manual set, Level 1 is called a CAUTION, not an "advisory".** |
| **Advisory** | **Not a term used in these notes.** The three levels are Level 3 WARNING, Level 2 CAUTION and Level 1 CAUTION. A simulation must not label Level 1 an "advisory" without tagging it "(assumed / not the notes' term)". |
| **Memo** | An indication generated by the FWS informing the crew about the **A/C configuration following routine crew action**. Displayed on the EWD (all memos) and, for flight-related memos, on the PFDs lower zone. **Strings of twenty characters maximum.** |
| **Limitation** | An indication generated by the FWS informing the crew about the **A/C flight capabilities** — messages indicating operational constraints following a degradation of the aircraft capability. Displayed on the EWD in **ALL PHASES** / **APPR & LDG** columns and, for flight-related ones, on the PFDs lower zone (up to 8). |
| **Inhibition** | The filtering of alert presentation so that (a) a warning or indication with no signification in a given configuration is not activated ("misleading warnings inhibition"); (b) alerts without interest for a flight phase are suppressed ("warnings inhibition related to flight phase" — many warnings and cautions inhibited during take-off and landing, shown as magenta **T.O INHIB / LDG INHIB**); (c) the crew can cancel presentation once corrective action is done (**CLEAR** — "warning manual inhibition"). |
| **Flight phase** | One of the **12** divisions of a normal aircraft flight computed by the FWS. Each phase corresponds either to an **A/C** or a **flight configuration change**. Computed from engine parameters, computed air speed, altitude and gear compressed/not compressed. Used by the CDS to compute the ECAM normal mode, by the FWS to inhibit alerts, and by the CMS as contextual failure information. |
| **Sensed item** | A checklist / procedure item for which the system state is monitored: **an automatic feedback is provided/given for sensed items**. |
| **Non-sensed item** | A checklist / procedure item whose completion the system cannot detect: **actions are confirmed manually through the ECP** (tick pushbutton). Non-sensed **procedures** (e.g. «COCKPIT WINDOW CRACKED») are the Supplementary Abnormal Procedures reached via **ABN PROC**. |
| **Attention getter** | A cockpit peripheral controlled by the FWS via **discrete signals** that draws the crew's attention visually: the **MASTER WARN** (red flashing, Level 3) and **MASTER CAUT** (amber steady, Level 2) lights, on the LH and RH units. Level 1 triggers **no** attention getter, visual or aural. |
| **Independent failure** | A failure which affects an isolated system or item of equipment **without affecting another one** (L1: TR failure; L2a: main fuel pump failure). EWD: red or amber message, system indication **underlined**. |
| **Primary failure** | A failure of a system or item of equipment **which causes the loss of other systems or equipments** (e.g. green hydraulic system failure). EWD: red or amber message, system indication underlined, **warning text surrounded**. |
| **Secondary failure** | The loss of a system or item of equipment **resulting from a primary failure** (e.g. loss of spoilers 2, 4, 6, 8). EWD: **amber asterisked** message. |
| **Status** | The **operational status of the A/C after system failures**. Draws crew attention to **limitations** and **deferred procedures** (part of the normal checklist); presents **inoperative systems** and **general information**. When the **MORE** indication is displayed, deeper information is available in the **Status More Info Page**. |
| **Deferred procedure** | Procedure actions deferred to a more appropriate phase of flight. Three types: **APPROACH, LANDING, PENDING**, displayed at fixed positions in the C/L menu only if some of the related type are really active. Title turns **amber → white** when all its items are done. |
| **Supplementary Abnormal Procedure** | An emergency/abnormal procedure **not sensed by the systems**, manually activated from the ABN PROC menu by validating the «ACTIVATE» line. Once activated it is displayed and processed like any other warning. |
| **Class 4 message / Time Limited Item** | A **minor, time-limited** fault detected by a system's **BITE**, reported to the FWS as a class 4 message; the FWS increments a per-system timer counter; on expiry it triggers the ECAM caution **MAINTENANCE TIME LIMITED ITEM** (flight phases 1 and 12 only). |
| **Backup connection** | A direct **ARINC 429** link (LRMs/AFDX-LRUs → CPIOMs-C, and FWS → CDS) and direct **discrete** links (ECP → CPIOM-C) that bypass the ADCN so that the FWS keeps working on total ADCN loss. |

### Conflicts between the two note sets, and the resolution used

| # | Conflict | L1 (2007, Level I) | L2a/L2b (2011, Level 2&3) | Resolution |
|---|---|---|---|---|
| C-1 | **Expansion of ADCN** | Prose: "Aircraft Data Communication Network (ADCN)". Legend box: "ADCN : **Avionics** Data Communication Network". | "Aircraft Data Communication Network (ADCN)". | Use **"Aircraft Data Communication Network"** (agreed by both prose texts and by the newer set). Note the L1 legend-box variant in the glossary. |
| C-2 | **Expansion of CPIOM** | Not expanded ("CPIOMs-C1 and C2"). | "**Core Processing Input/Output Modules (CPIOM)** -C1 and C2". | Use the **L2b** expansion. |
| C-3 | **ECP backup on ADCN loss** | "a backup connection keeps **all** its functions operational". | "discrete connections keep **most** of its functions operational". | Prefer **L2b ("most")** — more recent and more specific. State the L1 wording as the Level I simplification. |
| C-4 | **What the FWS sends to the CMS** | "its own BITE messages, and data such as **alerts** and flight phases … for maintenance data **consolidation**". | "its own BITE messages, and data such as **cockpit effects** and flight phases … for maintenance data **consolidation/correlation**". | Prefer **L2b**; both are compatible ("alerts" ⊂ "cockpit effects"). |
| C-5 | **Independent-failure example** | Transformer Rectifier (TR) failure. | Main fuel pump failure. | Both valid; use the **L2b** example (main fuel pump) as primary because it matches the EWD screenshot `FUEL FEED TK 1 MAIN PMP FAULT`, and offer the TR example as a second case. |
| C-6 | **Acquisition-path detail** | "either via the ADCN or directly for some systems through a backup connection". | Explicit: AFDX via ADCN for LRMs and AFDX-LRUs; **ARINC 429** for conventional LRUs; **plus** direct ARINC 429 backup for LRMs and AFDX-LRUs. | Model the **L2b** three-path topology; the L1 statement is a simplification of it. |
| C-7 | **Loudspeaker path** | FWS → loudspeakers (drawn direct). | FWS → **analog signals → AMU 1 / AMU 2** → loudspeakers. | Model the **L2b** AMU path. |
| C-8 | **Loudspeaker quantity** | 2 shown. | 4 shown (2 per AMU) + "a pair … one on each side" per application. | Model **4** per L2b; label the count as a diagram-derived figure. |
| C-9 | **EWD limitations example** | Same screenshot, no `T.O` memo block. | Adds the `T.O` memo block (`-SIGNS`, `-CABIN READY`, `-SPLRs ARM`, `-FLAPs…T.O`, `-AUTO BRAKE…RTO`, `-T.O CONFIG…TEST`) and labels it "TAKE OFF OR LANDING RELATED MEMOS INDICATIONS". | Use the **L2b** richer version. |
| C-10 | **Depth of Status description** | One paragraph. | Full detail: LIMITATIONS reminder, deferred-procedure reminder, ALL PHASES / APPR & LDG inop systems, MORE reminder, STS reminder, Status More Info contents. | Use **L2b** for all Status logic. |

**Overall precedence applied:** ratings/quantities and logic both taken from **L2a/L2b (2011, Level 2&3)**; L1 (2007, Level I) used only where L2 is silent (notably the acronym legend box, and the "FWS : Flight Warning System / SD : System Display" expansions) and to provide the Level-1 introductory framing of the four FWS roles.

---

### Appendix — the four FWS roles (verbatim framing, common to L1 and L2a)

In case of aircraft systems failure or A/C dangerous configuration, the FWS:
- alerts the crew in real time about the **seriousness level** of the failure,
- gives **failure identification and categorization** through caution and warning messages,
- helps pilots to **isolate the failure** through an associated procedure,
- provides **failure consequences on A/C status and flight operations (limitations)**.

In normal operations the FWS also provides operational assistance to the crew via **Normal Checklist, memos and aural announcements in approach**.

FWS functional breakdown (L2b p.62/63):
1. **Relevant FW Data Acquisition and Computation** — signals acquisition and computation from different sensors to detect an A/C system failure; also **flight phases calculation**.
2. **Alerts Identification** — identifies "Normal alerts" (memos, autocall out, C/L) and "failure-linked" alerts.
3. **Alerts Management** — alert **level identification**, alert **prioritization**, alert **inhibition**.
4. **Automatic Alerts and Associated Information Display and Recording** — records deferred alerts and associated timers; aural announcements management; attention getters management; warning and caution display and associated procedures; limitations, A/C status and memos display; C/L, abnormal and deferred procedures display.
5. **Alerts and Associated Info Display on Crew Input** — inhibit/recall the automatic alerts displays; access to system pages, to the Status Page, to the MORE Page, to the C/L and validations; recall cleared procedures; display Abnormal/Supplementary procedures.

---

# PART B — DESIGN BRIEF

**File produced:** `aerosim_ata31_flight_warning_system.html`

## Archetype: SYSTEM

The FWS is an alerting architecture plus two state machines — the alert classifier and the 12-phase flight-phase machine. Neither is a circuit, so there is no nodal solver and no oscilloscope; the engine is a directed signal-flow graph over the acquisition, display, aural, discrete and crew-input paths, evaluated against level, category, priority and inhibition rules. A CIRCUIT zoom would add nothing the notes support, so pure SYSTEM is chosen.

## Page map

| Mode | What this topic gets |
|---|---|
| **Explore** | Two switchable SVG views. *Architecture* draws data sources → network → the two CPIOM-C-hosted applications → the four indication paths, with each path colour-coded by its physical medium — AFDX, ARINC 429, analog audio, discrete, CAN — so that "the aural and getter paths never touch the ADCN" is visible rather than asserted. *Flight phases* lays out all 12 phases with their verbatim names, entry conditions and FPn Max limits. The right rail is a working cockpit: live MASTER WARN / MASTER CAUT boxes, an aural readout, mock EWD and SD screens that re-render from the engine, and a full clickable ECP 1135VM. Six signal traces highlight their own links on the schematic. 13-step build-up stepper. |
| **Build** | Constructor for the FWS signal architecture — 12 palette blocks, orthogonal wiring, undo/redo, JSON export/import, a path continuity tester that reports which sources reach each sink, three starter architectures and **eight** check-my-build targets including the two ADCN-loss paths. |
| **Fault Lab** | 12 cases — deliberately mixing real defects with correct-but-surprising behaviour (inhibition, TLI phase restriction, priority order) so the student must decide *whether* there is a defect. Seven diagnostic tests, the six-step troubleshooting flow, efficiency score, seeded exam mode, debrief naming the misconception. |
| **Learn** | 13 lesson steps with predict-observe-explain, then a 12-question quiz mapped to LO1–LO6 with a copyable results block. |

## Scenarios (0.5)

S0 normal cruise · SA1 Level 1 · SA2 Level 2 · SA3 Level 3 · SA4 primary + secondary · SA5 concurrent L3 and L2 · SP1 take-off phase 4 · SP2 landing phase 10 · SP3 phase data unavailable · SD1 ADCN lost · SD2 FWS Application 1 lost · SD3 ECP failed · ST1 Time Limited Item expired · FREE free play.

## Faults

Level 1 caution · Level 3 with EMER CANC misuse · primary with secondary · total ADCN loss · FWS Application 1 lost · ECP failed · both AMUs lost · take-off inhibition · flight-phase data unavailable · Time Limited Item in cruise · both attention getter units lost · concurrent Level 3 and Level 2.

## Check-my-build targets

Normal acquisition · acquisition on ADCN loss · aural path · attention getter path · normal crew input · crew input on ADCN loss · alert display · maintenance path.

## Outcome mapping

| Lesson steps | Quiz questions | Outcome |
|---|---|---|
| 1, 2 | 1 | LO1 identify the FWS architecture |
| 3 | 10, 11 | LO2 trace an alert from source to each peripheral |
| 4, 5, 6, 7 | 2, 3, 5, 6 | LO3 predict level, category and consequences |
| 8, 9 | 4 | LO4 operate the ECP correctly per alert level |
| 10, 11, 13 | 7, 8, 9, 12 | LO5 explain the flight-phase logic and inhibition |
| 12 | 10, 11 | LO6 isolate a degraded FWS configuration |

## Misconceptions the design forces into the open

M1 by giving the Level 1 case no chime and no light at all (step 5, Q2, fault f1); M2 by making EMER CANC behave differently on a Level 3 (step 8, Q4, fault f2); M3 by injecting the Level 2 first and still displaying the Level 3 first (fault f12, Q6); M4 by keeping the alert chain alive through an ADCN loss (step 12, Q10/Q11, fault f4); M5 by colour-coding analog audio and discrete separately from AFDX on the schematic (fault f7, f11); M6 by rendering the boxed primary and the asterisked secondary together (step 6, Q5, fault f3); M7 by dropping to the default cruise phase when the phase data are removed (step 11, Q8, fault f9).
