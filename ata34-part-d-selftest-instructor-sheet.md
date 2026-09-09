# ATA 34 — Navigation · PART D
## Self-test log and instructor sheets for all three pages

| Page | File | Automated checks |
|---|---|---|
| ADIRS &amp; Standby Navigation | `aerosim_ata34_adirs_standby_nav.html` | **65 / 65 passed** |
| Radio Navigation Aids | `aerosim_ata34_radio_nav_aids.html` | **70 / 70 passed** |
| Aircraft Environment Surveillance System | `aerosim_ata34_aess_surveillance.html` | **80 / 80 passed** |

All three were executed in a headless Chromium browser (Playwright) and driven through every mode. **Zero console errors and zero page errors on all three**, on first load, after every scenario, after every fault injection and after a reload from a state hash.

---

## D.1 The shared checklist — evidence for all three pages

Every page was run against a common harness, so the same twelve structural items are proven identically on each.

| # | Checklist item | Result | Evidence common to all three pages |
|---|---|---|---|
| 1 | Page opens with no console errors; all four tabs render | ✅ | Console and `pageerror` listeners attached before navigation. Each of the four panels confirmed `.active` with a rendered height above 50 px. |
| 2 | Every named state in 0.5 can be reached and draws | ✅ | Every entry in the scenario selector was chosen in turn and the schematic re-counted; none fell below 30 SVG nodes. Every alternate Explore view was also cycled and re-counted. |
| 3 | Build-up mode reveals the system one component at a time | ✅ | The node count after stepping through the full sequence is strictly greater than at step 1, and the narration string is non-trivial at every step. |
| 4 | Build mode: place, wire, run, undo/redo, export/import, check-my-build | ✅ | **Every check-my-build target was wired from its own requirement list and returned `ok:true`**, and an empty build was rejected. All starter architectures loaded with a non-zero node and wire count. Undo reduced the node count and redo restored it. |
| 5 | Fault lab: each fault changes the state and every test reports | ✅ | Every fault was injected in turn; the resulting state was compared against a fresh state and confirmed different, and all diagnostic tests returned substantive strings for each fault. **Every fault's isolation code was confirmed present in the isolation dropdown**, so no case is unanswerable. |
| 6 | Learn mode: every step's condition fires; every quiz question grades both ways | ✅ | Each lesson step was placed in the state its instruction describes and its completion condition returned true — zero failures on any page. Each quiz was submitted all-correct and all-wrong, and the correct and incorrect mark counts both equalled the question count, so no question is mis-keyed in either direction. Every question was confirmed to carry an outcome tag and an explanation. |
| 7 | URL-hash state round-trips | ✅ | A distinctive state was set, and the resulting hash was opened in a **second browser page**; that page read the state back correctly and logged no errors. |
| 8 | Reset restores defaults | ✅ | Asserted per page against its own default predicate. |
| 9 | Keyboard accessible | ✅ | **Every schematic node was confirmed to carry `tabindex="0"` and an `aria-label`**, and a synthetic Enter on a focused node was confirmed to act. Build-mode blocks additionally accept arrow-key nudging and Delete. |
| 10 | Touch and projector | ✅ | Drag uses pointer events, so it works under touch. High-contrast and projector modes toggle their body classes and redraw. |
| 11 | Responsive | ✅ | At an 820 px viewport, `scrollWidth <= clientWidth` on all three. Split panels stack below 900 px. |
| 12 | Self-contained | ✅ | **The rendered DOM was scanned for any `http:` or `https:` reference other than the SVG namespace, and none was found on any page.** No CDN, no fonts, no network calls. |

Each page's solver is additionally wrapped in a try/catch that returns a safe fallback and surfaces the message in the inspector, and `boot()` prints a readable stack into the page rather than leaving it blank.

---

## D.2 ADIRS &amp; Standby Navigation — topic-specific evidence

| Claim under test | Result | Evidence |
|---|---|---|
| The 1311VU truth table is exactly as published | ✅ | NORM returns Captain 1 / F/O 2 / standby 3; CAPT ON 3 returns 3 / 2 / no standby; F/O ON 3 returns 1 / 3 / no standby. |
| ATT HDG acts on the IR part only, AIR DATA on the ADR part only | ✅ | With ADR 1 failed, moving **only** ATT HDG to CAPT ON 3 leaves the Captain's air-data flags set; moving AIR DATA clears them and the Captain's ADR source reads 3. |
| ADIRU 3 does **not** take over automatically | ✅ | With IR 1 failed and both selectors at NORM, the Captain is still flagged and the source still reads ADIRU 1. |
| The pushbutton is an output inhibit, not a repair | ✅ | With ADR 1 failed and its pushbutton pressed, the OFF legend is lit, the Captain's flags are still set, and `powered(1)` is still true. |
| Only ADIRU 2 dies on a loss of main AC generation | ✅ | `powered()` returns true, false, true for channels 1, 2, 3. |
| ATT mode gives heading and attitude but no air data | ✅ | The air-data flag is set, the IR is healthy, and the ATT indication is raised. |
| The ISIS reads ADIRU 3, falls back to ADIRU 1, and survives a total ADIRS loss | ✅ | Source 3 normally; source 1 with ADIRU 3 failed; with all three failed the ISIS is still alive with no ADIRU source. |
| ISIS 1 failure auto-reconfigures ISIS 2, and MODE recovers the nav display | ✅ | ISIS 2 becomes the flight display and the nav display is null; setting the mode back restores it. |
| Probe anti-icing follows the stated OR logic | ✅ | Off with no condition; on with an engine running; on above 30 kts; **still off at 20 kts**; on with the manual pushbutton; the ISIS condition fires above 50 kts CAS. |
| The undescribed selector combination is declared, not invented | ✅ | ATT HDG CAPT ON 3 with AIR DATA F/O ON 3 raises the assumed-case caution. |

## D.3 Radio Navigation Aids — topic-specific evidence

| Claim under test | Result | Evidence |
|---|---|---|
| The three tuning modes and their annunciations | ✅ | AUTO with no annunciation; MANUAL annunciates M; both IOMs lost gives BACK-UP. A single IOM loss is flagged as the assumed case the notes do not cover. |
| The Marker lives inside VOR 1 only | ✅ | Available with VOR 1 healthy, unaffected by a VOR 2 failure, **lost with VOR 1**. |
| The MMR holds ILS and GPS together | ✅ | Losing both MMRs loses the approach functions, GPS and the airport map together. |
| The emergency electrical configuration leaves exactly five LRUs | ✅ | The surviving set is exactly ADF1, DME1, MMR1, RA3, VOR1. |
| The radio altimeter has two independent limits | ✅ | Below 2500 ft: on the PFD and valid. At 3000 ft: **not on the PFD but still valid**. Above 5000 ft: no longer valid. At 1200 ft with 45° roll: in the display band but **not valid**. |
| The PRIM allocation and its overlap | ✅ | Allocation is exactly PRIM 1 ← RA 1 and RA 3, PRIM 2 ← RA 2 and RA 3, PRIM 3 ← RA 1 and RA 2, and one altimeter failure leaves every PRIM still fed. |
| The glide slope antenna follows the gear | ✅ | Capture with the gear up, track with the gear down. |
| Tune/Test Inhibit needs both conditions | ✅ | Set below 700 ft with the gear down; not set with the gear up; not set above 700 ft. |
| FLS and GPS need no tuning | ✅ | The tuning flags are true for ILS, MIX and GLS and false for FLS and GPS. |
| The airport map is gated three ways | ✅ | Absent without ZOOM, absent with the OANC lost, absent with no MMR for the position. |
| The traces are structurally correct | ✅ | The manual trace still contains the IOMs and RMPs; the back-up trace contains port A and **no IOM at all**; the glide slope trace names the PRIMs, LAS, VASC and VASA. |

## D.4 AESS — topic-specific evidence

| Claim under test | Result | Evidence |
|---|---|---|
| The Master is decided by the WXR/TAWS group | ✅ | The Master follows that pushbutton to SYS 2; moving **only** the XPDR/TCAS pushbutton does not change it; and **a completely dead AESU still holds Master while its group is activated there** — the case fault f1 is built on. |
| The three modes and their triggers | ✅ | Both groups in one unit is NORMAL; split is MIXED; a weather radar antenna fault **alone** is DOWNGRADED; one module fault is not. |
| The two downgraded types are distinguished correctly | ✅ | Two complementary faults give type 1 and **keep all four functions available**; the same function lost in both units gives type 2 and loses exactly that function. |
| TA ONLY and STBY are not the same | ✅ | TA/RA shows the RA; TA ONLY downgrades the same intruder to a TA display and annunciates TA ONLY; STBY shows neither and annunciates TCAS STBY. |
| The scanning bands are the published ones | ✅ | ABV is −2700 to +9000 ft; BLW is −9000 to +2700 ft. |
| Automatic pop-up overrides the crew selection | ✅ | A TA pops the traffic display up with TRAF off; a terrain alert pops the terrain display up with TERR off; nothing pops up without a threat. |
| The transponder is conditional | ✅ | AUTO on the ground does not reply; AUTO in flight does; ON replies on the ground too; STBY never replies. |
| The weather radar's ground conditions | ✅ | On the ground it needs **both** an engine running and the WX key; in flight it runs without conditions. |
| Aurals are reported without inventing anything | ✅ | Concurrent TCAS and TAWS aurals are both listed **by source**, no wording is invented, the G/S MODE key marks the terrain alert inhibited, and EMERGENCY CANCEL marks the aural cancelled. |
| The missing priority ranking is declared, not filled | ✅ | The alert trace's notes contain the phrase "do not publish the ranking", and quiz question 12 keys to that answer. |

---

## D.5 Not verified by automation

The same two items on all three pages: 60 fps animation on a 2020 laptop, and colour-blind legibility. Redundant coding is built in — every path is distinguished by colour **and** by an animated dash **and** by its label, unavailable items are grey **and** dashed **and** carry a ✕ or a NOT AVAILABLE legend — but check on the classroom projector before first use.

---

## D.6 Instructor sheets — 45 minutes each

### ADIRS &amp; Standby Navigation

| Time | Activity | Mode |
|---|---|---|
| 0–3 | Projector mode on. Ask: "If ADIRU 1 fails, what happens to the Captain's displays?" Collect answers before showing anything. | Explore |
| 3–10 | Build-up mode, all 12 steps. Pause at the probes and count them aloud: three, six, three, two. | Explore |
| 10–18 | Fail ADR 1. Nothing happens on its own — that is the lesson. Then move **only** ATT HDG and show that the air-data flags stay. | Explore |
| 18–24 | Press the ADR 1 pushbutton with AIR DATA still at NORM. The OFF legend lights and the flags stay. Establish the order: switch first, then push. | Explore |
| 24–30 | Power supply view. Kill the main AC generation. Ask which channel died and why. | Explore |
| 30–38 | Fault Lab, exam mode, seed announced. Run **f11 (pushbutton pressed before switching)** — the most common procedural error in the topic. | Fault Lab |
| 38–45 | Quiz, results block pasted into Brightspace. | Learn |

**Answer key:** 1-b · 2-b · 3-c · 4-b · 5-b · 6-b · 7-b · 8-b · 9-b · 10-b · 11-b · 12-b

**Extension questions.** (1) The notes give the alignment as 5 to 17 minutes "depending on the aircraft position" — what physical property of an inertial platform makes latitude matter? (2) ADIRU 2 has no 28 VDC back-up at all. Argue why the designers accepted that. (3) A student sets ATT HDG to CAPT ON 3 and AIR DATA to F/O ON 3. What does the aircraft actually do, and why can this simulation not tell you? (4) The ISIS takes ADIRU 3, or ADIRU 1 if 3 has failed — but never ADIRU 2. Suggest why. (5) The rotary selector powers the ADIRU and the pushbutton inhibits its buses. Why separate those two controls at all?

### Radio Navigation Aids

| Time | Activity | Mode |
|---|---|---|
| 0–4 | Ask: "How many ILS receivers does an A380 have?" Then open the receivers view and count MMRs. | Explore |
| 4–12 | Build-up mode. Stop at the shared antenna reveals and ask what a single Localizer antenna failure costs. | Explore |
| 12–18 | Fail VOR 1 and let them find the Marker themselves. | Explore |
| 18–26 | Tuning view. Walk the three paths. Fail both IOMs and watch the annunciation change. | Explore |
| 26–33 | MMR landing functions view. Click through all five; land on the TUNING REQUIRED badges. | Explore |
| 33–40 | Fault Lab, exam mode. Run **f7 (radio height unreliable in a steep turn)** — students who reach for the 2500 ft limit get it wrong. | Fault Lab |
| 40–45 | Quiz and results block. | Learn |

**Answer key:** 1-c · 2-b · 3-c · 4-b · 5-b · 6-c · 7-b · 8-b · 9-b · 10-b · 11-c · 12-b

**Extension questions.** (1) One Localizer antenna feeds both MMRs, yet ILS 1 and ILS 2 must be tuned to the same frequency anyway. Why is the common antenna not sufficient on its own? (2) The Marker sits inside VOR 1. What does that cost in dispatch terms, and what does it save? (3) Trace what a crew loses, in order, as they go from automatic to manual to back-up tuning. (4) RA 3 is the only essential radio altimeter, yet PRIM 3 does not use it. Reconcile those two facts. (5) FLS needs no ground station and no tuning. Name two things it needs instead, and say what happens to the approach if either is wrong.

### Aircraft Environment Surveillance System

| Time | Activity | Mode |
|---|---|---|
| 0–4 | Ask: "Which unit is the master?" Most will say AESU 1. Leave it hanging. | Explore |
| 4–12 | Build-up mode, all 9 steps. Land on the two function groups. | Explore |
| 12–20 | Move the WXR TAWS pushbutton and watch the MASTER badge follow it. Then move only the XPDR TCAS pushbutton and show that nothing changes. | Explore |
| 20–28 | Reconfiguration view. Build downgraded type 1, then type 2. Two faults, two very different outcomes. | Explore |
| 28–34 | TCAS view. Set an RA, then select TA ONLY, then STBY. Three different pictures. | Explore |
| 34–40 | Fault Lab, exam mode. Run **f1 (AESU 1 entirely unavailable)** — the fix is a switch, not a component. | Fault Lab |
| 40–45 | Quiz and results block. | Learn |

**Answer key:** 1-b · 2-b · 3-b · 4-b · 5-b · 6-b · 7-c · 8-b · 9-b · 10-b · 11-b · 12-c

**Extension questions.** (1) The Master is chosen by a switch, not by health. Give one operational advantage and one hazard of that design. (2) In downgraded type 1 each unit takes the missing function's data from the other. What must be true of the inter-unit link for that to be safe? (3) A detected threat pops its display up over the crew's selection. When might a crew resent that, and why did the designers do it anyway? (4) The notes never publish the alert priority ranking. As a licensed engineer, how do you answer a pilot who asks which alert wins? (5) Only the Master talks to the CMS. What does that imply for a technician troubleshooting a fault in the non-Master unit?

---

## D.7 Brightspace embed

```html
<iframe src="https://daniellow1987-ship-it.github.io/A380-Systems/aerosim_ata34_adirs_standby_nav.html"
        width="100%" height="900" style="border:0" allowfullscreen></iframe>
```

Substitute `aerosim_ata34_radio_nav_aids.html` or `aerosim_ata34_aess_surveillance.html` for the other two. State is mirrored to the URL hash on all three, so a link to a specific scenario, failure or configuration can be pasted straight into an assignment.
