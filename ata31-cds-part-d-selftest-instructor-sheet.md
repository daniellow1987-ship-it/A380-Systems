# ATA 31 — Control & Display System · PART D
## Self-test log and instructor sheet

File under test: `aerosim_ata31_control_display_system.html`

---

## D.1 Self-test log

The page was executed in a headless Chromium browser (Playwright) and driven through every mode. Each item below is ticked with the evidence that confirmed it. **52 automated checks, 52 passed, zero console errors and zero page errors.**

| # | Checklist item | Result | Evidence |
|---|---|---|---|
| 1 | Page opens with no console errors; all four tabs render | ✅ | Console and `pageerror` listeners attached before navigation; zero messages captured across the whole run, including after every tab switch, every scenario and every fault. Each of the four panels confirmed `.active` with a rendered height above 50 px. |
| 2 | Every named state in 0.5 can be reached and shows the correct displays | ✅ | All 14 scenarios selected in turn; each redrew the schematic with more than 40 SVG nodes. Specific assertions: **S1** — `solve().dark.L1` true and `solve().A.L2 === "PFD"`, so the Captain's PFD transferred automatically to L2. **S3** — `solve().A.C2 === "EWD"`. **S7** — `solve().hosts.capt === "L1"`, the list migrated L3 → L2 → L1. **S15 (BAT)** — C1 and L3 lit, L1 and R1 dark, matching "only EWD and CAPT MFD are supplied". |
| 3 | Every control in 0.3 changes system state per 0.4; legends match the notes | ✅ | PFD/ND transfer, DU RECONF (both sides), the ND mode and range selectors, all 14 ECP page keys, the warning/advisory/phase injectors and the five network switches were each exercised through the inspector. RECONF asserted: with L3 failed, advancing `reconfStep.capt` changed the format shown on the host DU (`L2` before ≠ after). With no DU out, `solve().anyOut` is false and `cand.capt` is empty, so the button is disabled and the notes' sentence is surfaced instead. |
| 4 | Signal trace from a display reaches the correct source in each scenario | ✅ | `tracePath("PFD")` returns an ADCN chain when the network is healthy and an ADIRS-first chain with `bk === true` when it is not. `tracePath("EWD")` returns FWS-first on backup. `tracePath("VIDEO SD")` never flips to backup, matching the CMV direct connection. |
| 5 | Build mode: place, wire, run, meter, undo/redo, export/import, check-my-build | ✅ | Nodes placed and wired programmatically and by pointer drag; canvas redrew with more than 20 SVG nodes. `checkBuild(TARGETS[0])` returns `ok:true` for the correct wiring and `ok:false` for a deliberately wrong one, listing the missing link. `reachSources()` correctly reports ADIRS reaching the DU through the ADCN. Undo reduced the node count and redo restored it. JSON export/import round-trips through the textarea. |
| 6 | Fault lab: each fault produces its indications; the debrief shows the correct path | ✅ | All 11 faults injected in turn. For each: the state after injection differed from the healthy state, and after submitting the correct isolation and rectifying, the verification predicate (`!anyOut && adcn && ecp && cool && !bat`) returned true. All six diagnostic tests returned non-trivial strings for each fault. |
| 7 | Learn mode: every step's completion condition fires; every quiz question grades | ✅ | Each of the 12 lesson steps was put into the state its instruction describes and its `check()` returned true. The quiz was submitted with all-correct answers (12 `.ok` marks) and with all-wrong answers (12 `.bad` marks), so no question is mis-keyed in either direction. |
| 8 | URL-hash state round-trips; Reset restores defaults | ✅ | State set to C1 failed + ADCN off + F/O PFD/ND transferred, the resulting hash opened in a **second browser page**, and `STATE` there read back `C1:"fail"`, `adcn:false`, `xfer.fo:true` with zero errors on that page. Reset returned `anyOut:false, adcn:true, ecp:true`. |
| 9 | Keyboard-only walkthrough possible; touch works; high-contrast legible | ✅ | Every DU, panel and architecture block carries `tabindex="0"`, `role="button"` and an `aria-label`, and responds to Enter and Space — asserted by dispatching a synthetic Enter on a focused DU and reading back `STATE.sel`. Build-mode blocks additionally accept arrow-key nudging and Delete. Drag uses pointer events, so it works under touch. High-contrast and projector modes toggle their body classes and redraw. |
| 10 | No number shown that is not in 0.7 or tagged "(assumed)" | ✅ | Every specified figure on screen comes from the 0.7 whitelist. Items outside it carry the tag: ETACS, VIDEO SD, the OIT knob, the second monitoring loop and the phase→page mapping are each labelled "(assumed)" or "not defined in these notes" in the model, the inspector or the gaps table. The sample screen values from the manual (FLEX 83.9 %, N1 84.7 …) are deliberately **not** reproduced as ratings. |
| 11 | Responsive — no horizontal page overflow | ✅ | At an 820 px viewport, `scrollWidth <= clientWidth`. The split panels stack vertically below 900 px. |
| 12 | Solver never freezes the page | ✅ | `solve()` is wrapped in a try/catch that returns an all-dark fallback state and surfaces the message in the inspector; `boot()` is wrapped to print a readable stack into the page rather than leaving it blank. |

**Not verified by automation:** the visual quality of the animation at 60 fps on a 2020 laptop, and colour-blind legibility. Both were designed for — energised paths carry colour *plus* moving dots *plus* a solid stroke while de-energised carry grey *plus* dashes *plus* a "✕" glyph — but should be checked on the classroom projector before first use.

---

## D.2 Instructor sheet — 45-minute run of show

| Time | Activity | Mode |
|---|---|---|
| 0–3 | Open the page on the projector. Turn on **Projector** mode. Ask: "How many display units, and how many different kinds?" Let them answer wrong, then reveal: eight units, one kind. | Explore |
| 3–10 | **Build-up mode.** Step through all 14 components. Stop at the ADCN step and ask what happens if that box goes. | Explore |
| 10–16 | Fail L1 live. Predict-then-observe: what is lost, the PFD or the ND? Then fail C1 and repeat. | Explore |
| 16–24 | Load **S7 (L3 and L2 out)**. Walk the RECONF list: where does it live, what order does it offer, and what does it refuse? Try to put the SD on L1 in front of the class. | Explore |
| 24–30 | Switch to the **Architecture** view. Kill the ADCN. Trace the magenta paths. Ask which content is genuinely lost. | Explore |
| 30–38 | **Fault Lab**, exam mode on, seed announced. Run fault **f9 (R1 brightness knob at OFF)** — students who test before they observe will burn four tests on a knob position. Debrief the efficiency score. | Fault Lab |
| 38–45 | Students take the 12-question quiz on their own laptops and paste the results block into Brightspace. | Learn |

### Answer key — final quiz

| Q | Answer | Q | Answer |
|---|---|---|---|
| 1 | Pin programming according to the DU location | 7 | Failure related mode |
| 2 | The Captain's PFD transfers automatically to L2 | 8 | The ADIRS in ARINC 429 through a direct backup connection |
| 3 | MFD, EWD, SD, PFD, ND | 9 | The CMV |
| 4 | On L1 | 10 | The EMER CANC key |
| 5 | EWD and SD | 11 | Two loops of four |
| 6 | Nothing — there is no effect | 12 | The EWD and the Captain's MFD |

### Five extension questions

1. The EWD centralises the BITE data of all DUs and KCCUs over CAN bus 1.1 and 2.1. If the EWD is failed **and** the SD is displaying on the Captain's MFD after a reconfiguration, where does the BITE centralisation function live, and what does that tell you about the difference between a *format* and a *function*?
2. The Captain's PFD is supplied from the DC ESS BUS with no backup, while the Captain's ND has DC BUS 1 as a backup. Argue why the designers gave the backup to the less critical display.
3. A DU shows "Check CAPT PFD" and so does the F/O PFD, but the CAPT PFD itself looks perfectly normal. Which DU raised the message, and why do two displays carry it?
4. On a total loss of cooling air the DUs are specified to withstand thirty minutes. Relate that figure to a flight phase and explain the design intent.
5. The notes say manual mode "can override all other modes", and also that an incoming warning "automatically triggers the failure related mode". Write a single sentence that reconciles the two statements, and state which note set you would quote in an exam answer and why.

### Brightspace embed

```html
<iframe src="https://daniellow1987-ship-it.github.io/A380-Systems/aerosim_ata31_control_display_system.html"
        width="100%" height="900" style="border:0" allowfullscreen></iframe>
```

State is mirrored to the URL hash, so a link to a specific scenario or fault configuration can be pasted straight into an assignment.
