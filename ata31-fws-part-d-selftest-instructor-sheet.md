# ATA 31 — Flight Warning System · PART D
## Self-test log and instructor sheet

File under test: `aerosim_ata31_flight_warning_system.html`

---

## D.1 Self-test log

The page was executed in a headless Chromium browser (Playwright) and driven through every mode. Each item below is ticked with the evidence that confirmed it. **62 automated checks, 62 passed, zero console errors and zero page errors.**

| # | Checklist item | Result | Evidence |
|---|---|---|---|
| 1 | Page opens with no console errors; all four tabs render | ✅ | Console and `pageerror` listeners attached before navigation; zero messages captured across the whole run — including a pass that presses **every** ECP key in sequence. All four panels confirmed `.active` and rendered. |
| 2 | Every named state in 0.5 can be reached and shows the correct indications | ✅ | All 14 scenarios selected in turn, each redrawing more than 40 SVG nodes. |
| 3 | Alert levels produce exactly the aural and visual outputs the notes specify | ✅ | **Level 1** → `aural:"none"`, `mw:false`, `mc:false` — no chime and no attention getter. **Level 2** → `aural:"single chime"`, `mc:true`, `mw:false`. **Level 3** → `aural:"CRC"`, `mw:true`. Concurrent L3 + L2 → both `mw` and `mc` true, confirming the notes' "the MASTER WARN and MASTER CAUT lights can come on simultaneously". |
| 4 | Priority is fixed, not chronological | ✅ | With the Level 2 injected **first** and the Level 3 second, `evaluate().shown[0].lvl === 3`. The display order is unchanged by the order of occurrence. |
| 5 | EMER CANC behaves differently for Level 3 than for Levels 1 and 2 | ✅ | On a Level 3: after `emerCanc()`, `shown.length` is still 1 (the red message remains) and `aural` begins "none" (the audio and MASTER WARN are gone). On a Level 2: `shown.length` drops to 0 and the alert id appears in `STATE.cancelled`, which the SD renders under **CANCELLED CAUTION** on the Status More Info page. |
| 6 | CLEAR and RCL work as described | ✅ | `clearTop()` takes the displayed alert count to 0; `recall()` restores it to 1. |
| 7 | Failure categories render with their EWD characteristics | ✅ | The primary + secondary case returns both `"primary"` and `"secondary"`; the EWD renderer boxes the primary, underlines the independent system indication and prefixes the secondary with an asterisk. |
| 8 | The 12 flight phases are verbatim, with the correct default | ✅ | `MODEL.phases.length === 12`; spot-checked `3:TAKE OFF STEP 1`, `8:CRUISE`, `12:POSTFLIGHT`. With `phaseData` false, `effPhase()` returns **8**, matching "if the data are not available to compute the flight phases, the FWS selects by default the cruise phase". |
| 9 | Inhibition works, and is reversible for the right reason | ✅ | In phase 4 the Level 1 caution is inhibited (`inhib.length === 1`, `shown.length === 0`) and the EWD shows magenta **T.O INHIB**. Removing the phase data drops the system to the default cruise phase and the same caution reappears — the exercise that breaks the "phase comes from a switch" misconception. The Time Limited Item caution is hidden in cruise and shown in phase 12. |
| 10 | Signal trace reaches the correct source on every path, normal and degraded | ✅ | Acquisition traces through the ADCN normally and through ARINC 429 when it is lost; the ECP traces through CAN/IOM/ADCN normally and through discretes when it is lost. Asserted explicitly: **neither the aural chain nor the attention-getter chain ever contains the string "ADCN"**, in either configuration. |
| 11 | Degraded configurations degrade only what the notes say they degrade | ✅ | **ADCN lost** with a Level 3 active → `aural:"CRC"`, `mw:true`, message still shown. **Both AMUs lost** → aural silenced, MASTER WARN still on. **Both attention getters lost** → lights off, message and chime unaffected. **Both FWS applications lost** → a single error string that explicitly carries the word "assumed", because the notes do not describe this case. **RMP RST** → aural only; the visual indications are unchanged. |
| 12 | Every control in 0.3 is handled; the ECP failure case is correct | ✅ | Every key in `MODEL.ecp.top`, `sysL`, `sysR` and the management block was pressed programmatically with no error. With the ECP failed, `ENG` is blocked (`sdPage` stays null) while `STS` still works — matching the discrete key list CLR, RCL, STS, EMER CANC, VALID, scroll and ALL. |
| 13 | Build mode: place, wire, run, meter, undo/redo, export/import, check-my-build | ✅ | **All eight** check-my-build targets were wired from their own `need` list and each returned `ok:true`. All three starter architectures loaded with a non-zero wire count. Undo reduced the node count and redo restored it. The continuity tester reports which sources reach each sink. |
| 14 | Fault lab: each case produces its indications and can be resolved | ✅ | All 12 cases injected in turn; each changed the state from healthy, all seven diagnostic tests returned substantive strings for each, and after the correct isolation and rectification the verification predicate returned true. |
| 15 | Learn mode: every step's completion condition fires; every quiz question grades | ✅ | Each of the 13 lesson steps was placed in the state its instruction describes and its `check()` returned true (zero failures). The quiz was submitted all-correct (12 `.ok`) and all-wrong (12 `.bad`). |
| 16 | URL-hash state round-trips; Reset restores defaults | ✅ | Primary+secondary alerts, ADCN off and phase 10 were encoded, the hash opened in a **second browser page**, and that page read back two active alerts, `adcn:false`, `phase:10`, with zero errors. Reset returned `adcn:true`, no active alerts, phase 8. |
| 17 | Keyboard-only walkthrough possible; touch works; high-contrast legible | ✅ | Architecture nodes and phase boxes carry `tabindex`, `role="button"` and `aria-label` and respond to Enter/Space (asserted with a synthetic Enter). Build blocks accept arrow-key nudging and Delete. Drag uses pointer events. High-contrast and projector modes toggle and redraw. |
| 18 | No number shown that is not in 0.7 or tagged "(assumed)" | ✅ | Every specified figure comes from the 0.7 whitelist. The specific inhibition mapping, the within-level ordering, the arrow-key function, the T.O CONFIG / ALL / VIDEO / RCL LAST key functions and the both-applications-lost case are each tagged "(assumed)" where they appear. The manual's sample screen values are reproduced only as illustrative display content, never as FWS ratings. |
| 19 | Responsive — no horizontal page overflow | ✅ | At an 820 px viewport, `scrollWidth <= clientWidth`. |
| 20 | Engine never freezes the page | ✅ | `evaluate()` is wrapped in a try/catch returning a safe empty result with the message surfaced in the inspector; `boot()` prints a readable stack into the page rather than leaving it blank. |

**Not verified by automation:** 60 fps animation on a 2020 laptop, and colour-blind legibility. Redundant coding is built in — each signal path is distinguished by colour *and* by an animated dash *and* by its label, and de-energised paths are grey *and* dashed — but check on the classroom projector before first use.

---

## D.2 Instructor sheet — 45-minute run of show

| Time | Activity | Mode |
|---|---|---|
| 0–3 | Open on the projector, **Projector** mode on. Ask: "What are the three alert levels, and what does each one sound like?" Collect answers before showing anything. | Explore |
| 3–10 | **Build-up mode**, all 13 steps. Pause at the AMU step and at the attention-getter step; ask which of the four output paths uses the ADCN. | Explore |
| 10–18 | Inject the Level 1, then Level 2, then Level 3 alerts. Predict-then-observe the chime and the lights each time. The Level 1 silence is the point of the whole segment. | Explore |
| 18–24 | With the Level 3 active, press **EMER CANC** in front of the class. Then repeat with a Level 2. This is the single most examinable difference in the topic. | Explore |
| 24–30 | Switch to the **Flight phases** view. Walk the 12 phases and their transitions. Then set phase 4 with the Level 1 active and show T.O INHIB; then remove the phase data and watch the alert come back. | Explore |
| 30–38 | **Fault Lab**, exam mode on, seed announced. Run fault **f8 (take-off phase inhibition)** — an inhibited alert is not a defect, and students who report an unserviceability fail the case. Debrief. | Fault Lab |
| 38–45 | Students take the 12-question quiz and paste the results block into Brightspace. | Learn |

### Answer key — final quiz

| Q | Answer | Q | Answer |
|---|---|---|---|
| 1 | Two, in CPIOM-C1 and CPIOM-C2 | 7 | 12 phases, default phase 8 (cruise) |
| 2 | None at all | 8 | Engine parameters, computed air speed, altitude and gear compressed information |
| 3 | Single chime | 9 | Magenta |
| 4 | Only the audio signal and the MASTER WARN light are cancelled | 10 | They continue — analog audio to the AMUs, which never used the ADCN |
| 5 | Secondary failure | 11 | Most of its functions, through discrete connections |
| 6 | Always in the same defined priority order | 12 | Phases 1 and 12 only |

### Five extension questions

1. The aural path is analog and the attention-getter path is discrete, while the display path is AFDX with an ARINC 429 backup. Explain, in terms of failure independence, why the designers deliberately used three different physical media for three outputs of the same computer.
2. A Level 1 caution gives no chime and no light. Argue both sides: what is gained by that choice, and what is the risk the design accepts?
3. The notes state that several messages "are always displayed in the same order, which is not dependent on the chronology". Give a concrete two-failure scenario in which a chronological display order would actively mislead the crew.
4. `MAINTENANCE TIME LIMITED ITEM` is shown only in flight phases 1 and 12. Explain how that restriction, the class 4 BITE message and a single MMEL entry point work together to let an aircraft dispatch.
5. The LEVEL I notes say the ECP backup keeps **all** its functions operational; the LEVEL 2&3 notes say **most**. Which would you write in an exam, and what general rule about note-set precedence does your answer illustrate?

### Brightspace embed

```html
<iframe src="https://daniellow1987-ship-it.github.io/A380-Systems/aerosim_ata31_flight_warning_system.html"
        width="100%" height="900" style="border:0" allowfullscreen></iframe>
```

State is mirrored to the URL hash, so a link to a specific alert configuration, flight phase or degraded architecture can be pasted straight into an assignment.
