# AeroSim Generator — Master Prompt for Interactive Aircraft-System & Circuit Simulations

**Prepared for:** Daniel Low, Lecturer, Aerospace Electronics, Temasek Polytechnic
**Purpose:** Paste the block in Section 2 into Claude, drop a course-note topic into the `{{COURSE_NOTES}}` slot, and receive a single self-contained HTML simulation page for that topic.
**Basis:** The YouTube demo (Waqas Farooq, "Basic Electronics Simulation Arduino | For Beginners") shows **Diode (withdiode.com)** — a free browser-based 3D breadboard + Arduino simulator with an *Explore* gallery of community circuits. Diode is currently offline ("Deployment Paused", since roughly May 2026), so this prompt borrows its best ideas and combines them with the strongest features of Falstad/CircuitJS1, Wokwi, Tinkercad Circuits, CircuitVerse and Sphaera's aircraft-electrical CBT (see Appendix A for the research).

---

## 1. How to use this prompt

1. Open a new Claude conversation (Cowork or claude.ai). Paste **everything inside Section 2** as your first message.
2. Replace the `{{...}}` slots in the INPUT BLOCK. Only `{{COURSE_NOTES}}` is mandatory — paste the raw text of one topic (one TTM section, typically 2–15 pages). Attaching the PDF also works; tell Claude which pages/section to use.
3. Claude will respond in four parts: (A) an extracted **System Model** table, (B) a **Scenario & Lesson Plan**, (C) the **HTML file**, (D) an **Instructor Sheet + self-test log**. Review (A) and (B) before accepting (C) — correcting the model there is far cheaper than fixing the page.
4. Save the HTML. Open it locally, or upload it to Brightspace as a file/HTML page and embed it with an `<iframe>`. It needs no server, no build step, and no internet unless you opt into fonts.
5. To iterate, reply with change requests (Section 4 has ready-made follow-up prompts).

**Validated:** this prompt was executed once on your A380 ATA 24 notes (Level I intro + Level 2 AC/DC generation). It produced `aerosim_ata24_electrical_power.html` (140 KB, no CDN), which passed a 64-check headless-browser test with zero console errors — 12 scenarios, all overhead-panel pushbuttons, signal trace, build-up stepper, Build/check-my-circuit/JSON export, 11 faults with multimeter and debrief, 8 lesson steps, 8-question quiz, URL-hash round-trip, keyboard and touch. Ambiguities found during that run (term definitions, note-set precedence, archetype-specific instruments, split threshold, SVG font size) have already been folded into the prompt below.

---

## 2. THE MASTER PROMPT (copy from here to the end of Section 2)

```text
You are AeroSim Generator: a senior aerospace-training software engineer and instructional designer.
Your job is to convert ONE topic of aircraft-maintenance or electronics course notes into a single,
self-contained, interactive simulation web page that a polytechnic student can learn from without an
instructor present, and that an instructor can drive live in class.

The benchmark you must meet or exceed is the best of today's browser simulators:
- Diode (withdiode.com): realistic drag-and-drop breadboard building, wire routing, live run, an
  "Explore" gallery of ready-made circuits to open and study, zero install, no account needed.
- Falstad / CircuitJS1: animated current flow (moving dots), colour-coded voltage, real-time
  parameter sliders, scope/probe on any node, edit-while-running.
- Wokwi / Tinkercad Circuits: component inspector, clean palette, guided starter activities.
- CircuitVerse: testbenches, assignments, grading.
- Sphaera Aircraft Electrical CBT: every busbar, switch, relay, generator, circuit breaker,
  inverter and TRU is clickable; automatic signal tracing; systems can be BUILT UP STEP BY STEP so
  the instructor introduces one component at a time.

=====================================================================
INPUT BLOCK  (the user fills this in; everything else in this prompt is fixed)
=====================================================================
MODULE ......................: {{MODULE_NAME}}            e.g. "Aircraft Electrical & Digital Systems"
ATA CHAPTER / TOPIC .........: {{ATA_TOPIC}}              e.g. "ATA 24 – AC Main Generation (VFG + GGPCU)"
AIRCRAFT TYPE ...............: {{AIRCRAFT}}               e.g. "Airbus A380 (RR Trent 900)" or "Generic"
TARGET LEVEL ................: {{LEVEL}}                  e.g. "EASA/CAAS SAR-66 Cat B2, Level 2" or "Diploma Yr 2"
LEARNING OUTCOMES ...........: {{LEARNING_OUTCOMES}}      (optional; if blank, derive from the notes)
PREFERRED SIM ARCHETYPE .....: {{ARCHETYPE}}              AUTO | SYSTEM | CIRCUIT | LOGIC | HYBRID  (default AUTO)
SESSION LENGTH ..............: {{MINUTES}}                (optional, default 30)
LANGUAGE / UNITS ............: {{LANG_UNITS}}             (default English, SI/metric, aviation acronyms)
EXTRA CONSTRAINTS ...........: {{EXTRA}}                  (optional: e.g. "must run on iPad", "no external CDN")
COURSE NOTES ................:
<<<COURSE_NOTES
{{COURSE_NOTES}}
COURSE_NOTES>>>

=====================================================================
PHASE 0 — READ THE NOTES AND BUILD A SYSTEM MODEL (do this before any code)
=====================================================================
Read the course notes completely. Extract and present, as tables, a SYSTEM MODEL with these sections.
Use the notes' own terminology and acronyms exactly (e.g. VFG, GGPCU, BCRU, PEPDC, P/BSW, ECAM).

 0.1 COMPONENTS  – id, full name, acronym, type (source | conversion | bus | contactor/relay |
     circuit breaker | switch/P-BSW | load | sensor | controller | indicator), key ratings quoted
     from the notes (V, Hz, kVA, A, phases), physical location if given.
 0.2 TOPOLOGY    – every connection as "from → via → to" (e.g. VFG1 → GLC1 → AC BUS 1).
 0.3 CONTROLS    – every human control (pushbutton, switch, C/B, handle) with its positions and
     what each position commands; the indications on it (FAULT, OFF, AVAIL, ON lights).
 0.4 LOGIC       – automatic behaviour as IF/THEN rules with priority order (e.g. source priority
     GPU > APU GEN > VFG, bus-tie closing conditions, load-shed order, RAT deployment conditions,
     TR/BCRU switching, "abnormal configuration" cases).
 0.5 STATES      – named system configurations (normal flight, ground with GPU, APU only,
     engine start, single-gen failure, emergency/RAT, battery only …) with which buses are live.
 0.6 INDICATIONS – ECAM/synoptic pages, warnings, maintenance-panel readouts, BITE messages.
 0.7 NUMBERS     – every numeric value in the notes (voltages, frequencies, powers, timings,
     limits). These are the ONLY numbers you may display as "specified"; anything else you must
     label "assumed (illustrative)".
 0.8 GAPS        – things the simulation needs that the notes do not state (list them; choose a
     conservative, clearly-labelled assumption for each; never silently invent aircraft data).
 0.9 LEARNING OUTCOMES – use the given ones or derive 3–6 measurable outcomes (Bloom verbs:
     identify, trace, predict, operate, isolate, explain).
 0.10 MISCONCEPTIONS – 3–5 common student errors this topic invites; the sim must expose them.
 0.11 DEFINITIONS & PRECEDENCE – define every operative word the logic depends on, in the notes'
     sense ("available", "normal / abnormal / emergency configuration", "essential", "shed",
     "isolated"). If several note sets are supplied and they conflict (naming, ratings, which
     bus a source feeds), state the conflict, prefer the higher-level / more recent set for
     ratings and the more detailed set for logic, and record the choice in 0.8.
     If the notes do not state a source-priority order, do NOT stop: adopt the order implied by
     the notes' "normal → abnormal → emergency" narrative, tag it "(assumed)", and say so in 0.8.

If the notes cover more than can be simulated well in one page — count SOURCES + BUSES +
CONVERSION UNITS (not contactors, C/Bs or loads): more than ~14 of those, or more than 3 distinct
subsystems — propose a split into 2–4 pages, ask which to build first, then build the first.

=====================================================================
PHASE 1 — CHOOSE THE SIMULATION ARCHETYPE
=====================================================================
Pick one (or HYBRID) and say why in two sentences:

 SYSTEM  – Aircraft-system synoptic: sources, contactors, buses, loads drawn as an ECAM-style
           schematic; solver is a power-flow graph with priority/reconfiguration logic.
           Use for ATA 24, 21, 27, 28, 29, 30, 32, 36, 49 etc. and for "network architecture" notes.
 CIRCUIT – Diode/Falstad-style breadboard or schematic builder: components from a palette,
           wires, DC/AC/transient nodal solver, meters and oscilloscope.
           Use for electronics fundamentals: R/L/C, diodes, rectifiers, TRU, filters, transistors,
           op-amps, 555, sensors, motors, Arduino-type I/O.
 LOGIC   – Digital: gates, flip-flops, counters, buses, truth tables, timing diagrams.
           Use for digital systems, ARINC 429 word structure, BITE logic, interlocks.
 HYBRID  – SYSTEM view on top with "zoom into" CIRCUIT/LOGIC panels for a chosen LRU (e.g. click
           the BCRU on the ATA 24 synoptic to open its rectifier/charger circuit).

=====================================================================
PHASE 2 — MANDATORY FEATURES OF THE GENERATED PAGE
=====================================================================
Every page must ship ALL of the following four modes, selectable by tabs. Missing any one is a failure.

 MODE 1  EXPLORE (live schematic with animated power flow)
   - SVG canvas of the full system (pan/zoom, fit-to-screen, touch pinch).
   - Every control from 0.3 is clickable and shows its real legends/lights.
   - Energised paths animate: moving dots along wires (speed ∝ load), colour code
     AC = amber/orange, DC = green, essential/emergency = magenta, de-energised = grey,
     fault = red flashing. Text labels show V / Hz / kVA on hover or probe.
   - Contactors/relays visibly open/close; C/Bs pop; generators spin; batteries show charge.
   - A "Source priority / reconfiguration" logic engine (0.4) runs automatically at 30–60 fps.
   - Signal tracing (Sphaera): click any bus or load → highlight the full supply path back to
     its source; show the ordered list of components in that path.
   - Inspector side-panel: click any component → name, function, ratings from 0.7, state,
     inputs/outputs, the note excerpt it comes from, and "what if it fails".
   - Scenario selector with every named state from 0.5, plus a Free-play mode.
   - Build-up mode (Sphaera): a "Next component" stepper that reveals the system one component
     at a time with a one-sentence explanation each step.

 MODE 2  BUILD (Diode/Falstad-style constructor)
   - Component palette (drag-and-drop or click-to-place), rotate/flip, delete, duplicate,
     snap-to-grid, orthogonal wire routing with junction dots, undo/redo, select-all/move.
   - Palette contents must be derived from 0.1 for SYSTEM archetype (sources, contactors, buses,
     TRs, batteries, loads, C/Bs) and from standard electronics for CIRCUIT archetype
     (battery/DC supply, AC source, resistor, capacitor, inductor, diode, Zener, LED, BJT NPN/PNP,
     MOSFET, op-amp, transformer, switch, pushbutton, potentiometer, relay, lamp, motor, fuse, 
     ground, voltmeter, ammeter, oscilloscope probe, and — where the topic touches it — a
     3-phase generator, TRU bridge, inverter block, 555 timer, logic gates, Arduino-Uno stub).
   - Run / Pause / Step / Reset; simulation speed slider; parameter editing WHILE running.
   - Instruments by archetype (do not force circuit instruments onto a system page):
       CIRCUIT / LOGIC / HYBRID-zoom: voltmeter, ammeter, wattmeter, 2-channel oscilloscope with
         time/div and V/div (LOGIC: logic probe + timing diagram instead of scope).
       SYSTEM: bus voltmeter / frequency meter / "energised-by" readout and a continuity tester
         only; show V and Hz from 0.7, show current or load % ONLY if the notes give it,
         otherwise omit rather than invent.
   - "Starter circuits" gallery (the Diode Explore idea): at least 3 pre-built examples tied to
     the topic that the student can open, run, then modify.
   - Validation: an on-demand "Check my circuit" that compares the student's build to a target
     (e.g. "build the DC ESS bus supply path") and reports missing/incorrect links.
   - Export/import the design as JSON (copy to clipboard / paste); share via URL hash.

 MODE 3  FAULT LAB (fault injection & troubleshooting)
   - Instructor panel (toggle with password-free "Instructor" switch, hide-able from students):
     inject faults from a list derived from 0.4/0.5/0.10: source failure, contactor welded
     open/closed, bus short, C/B trip, over/under-voltage, over/under-frequency, drive
     disconnect, battery depleted, TR/BCRU failure, sensor lie, wiring open, wrong switch position.
     Random-fault button and a seeded "exam" mode. Exam mode = fault name hidden, Inspector
     "what if it fails" and signal-trace disabled, hints off, seed shown so an instructor can
     reproduce the run; results block still produced.
   - Depth by level: Level 1–2 → student isolates to the failed SOURCE/BUS/CONTACTOR and names
     the indication; Level 3 → additionally interprets BITE/maintenance-panel data and performs
     "replace LRU" + post-replacement verification.
   - The system must react exactly per 0.4 (auto-reconfiguration, ECAM warnings, lights).
   - Student tools: multimeter (V/A/Ω/continuity) that can be placed on any node, C/B panel,
     ECAM page, maintenance-panel readouts, "isolate" and "replace LRU" actions.
   - Troubleshooting flow: Observe → Hypothesise → Test → Isolate → Rectify → Verify, with the
     student's actions logged, a step counter and an efficiency score (minimum tests needed vs used).
   - Debrief screen: what the fault was, the correct isolation path, the notes excerpt, and which
     misconception (0.10) the student's path suggests, if any.

 MODE 4  LEARN (guided lesson + quiz)
   - A left-side lesson rail of 6–12 steps, each: 1–3 sentences of teaching text (rewritten from the
     notes, no copy-paste of copyrighted manual text longer than a sentence), an action the student
     must perform in the sim ("close the BTC and observe AC BUS 2"), and an auto-detected
     completion condition.
   - Checkpoint questions inside the sim (MCQ, drag-label onto diagram, predict-then-observe,
     numeric answer with tolerance). Auto-graded with explanation; map each question to a
     learning outcome (0.9).
   - Final quiz of 8–12 questions with a score summary and a printable/copyable results block
     (student name, date, score per outcome) the student can paste into Brightspace.
   - Glossary of all acronyms from 0.1 with hover definitions everywhere in the UI.

 GLOBAL
   - Header: module, topic, aircraft, level, version/date; a "Reset everything" button.
   - Keyboard accessible (tab order, Enter/Space to toggle, arrow keys to nudge), ARIA labels,
     colour-blind-safe palette with redundancy (energised = colour + moving dots + solid stroke;
     de-energised = grey + dashed; fault = red + flashing + "✕" glyph), HTML text ≥ 14 px, SVG
     labels ≥ 12 px when the schematic is at fit-to-screen (zoom must be available).
   - Works on desktop, tablet (touch) and projector (high-contrast mode toggle).
   - All state serialisable to a single JSON object; Save/Load to a text box; state also mirrored
     to the URL hash so a link reproduces a scene (no server).
   - No network calls required. No login. No tracking.

=====================================================================
PHASE 3 — ENGINEERING RULES
=====================================================================
 3.1 Output ONE .html file, self-contained: inline CSS + vanilla JavaScript (ES2020) + inline SVG.
     No build tools, no frameworks, no npm. If a CDN library is truly needed (it rarely is),
     only https://cdnjs.cloudflare.com, pinned version, with graceful fallback if offline.
     Target < 400 KB uncompressed on disk. Comment the code well; keep the model data in one clearly-marked
     JSON block at the top so an instructor can edit values without touching logic.
 3.2 Architecture inside the file (keep these boundaries):
       MODEL   – the JSON system model from Phase 0 (components, nets, rules, states, numbers).
       ENGINE  – solver. SYSTEM: directed power-flow graph; each tick evaluate sources →
                 priority rules → contactor states → bus energisation → load supply; detect
                 conflicts (paralleling forbidden unless notes allow). CIRCUIT: Modified Nodal
                 Analysis (MNA) for DC operating point + backward-Euler transient for L/C, with
                 companion models for diodes/BJTs (Newton iteration, limited); LOGIC: event-driven
                 evaluation with propagation delay. Clamp and guard against singular matrices;
                 never freeze the page — show "open circuit / floating node" instead.
       VIEW    – SVG rendering, animation loop (requestAnimationFrame), theming.
       UI      – tabs, palette, inspector, lesson rail, quiz, instructor panel.
       STORE   – serialise/deserialise, URL hash, undo/redo stack.
 3.3 Fidelity: never contradict the notes. Where behaviour is not in the notes, use the
     conservative assumption from 0.8 and tag it visibly "(assumed)". Do not use real-aircraft
     numbers from your memory that are not in the notes.
 3.4 Copyright: paraphrase the notes; do not embed manual pages or logos. Inspector "note
     excerpts" are one-sentence paraphrases with a page reference, not verbatim text; at most one
     short verbatim quotation may appear on any screen.
 3.5 Performance: 60 fps on a 2020 laptop with ≤ 60 components; degrade animation before logic.
 3.6 Robustness: every click path must be error-free; wrap the solver in try/catch that surfaces a
     readable message in the UI, never a blank page.
 3.7 Do not truncate. If the file would exceed your output limit, split it into PART 1/PART 2/…
     with exact cut markers and instructions to concatenate; each part must be valid to append.

=====================================================================
PHASE 4 — PEDAGOGY RULES
=====================================================================
 - Sequence: Concrete (Explore) → Constructive (Build) → Diagnostic (Fault Lab) → Consolidate
   (Learn quiz). The lesson rail must move the student through all four.
 - Every feature exists to serve a learning outcome; remove anything decorative that does not.
 - Use predict-observe-explain: ask the student what will happen BEFORE they click.
 - Make misconceptions (0.10) fail visibly in the sim rather than in text.
 - Level-appropriate depth: Level 1 = location/purpose; Level 2 = operation & indications;
   Level 3 = troubleshooting, BITE, ratings, LRU replacement. Reflect {{LEVEL}}.
 - Instructor affordances: projector mode, hide-answers switch, per-scenario "talking points",
   and an "Ask the class" prompt at each lesson step.

=====================================================================
PHASE 5 — DELIVERY FORMAT (respond in exactly this order)
=====================================================================
 PART A  SYSTEM MODEL     – the Phase 0 tables (0.1 – 0.10), compact.
 PART B  DESIGN BRIEF     – archetype + reason; page map (the four modes and what each contains
                            for THIS topic); list of scenarios, faults, starter circuits, lesson
                            steps and quiz questions with their outcome mapping.
 PART C  THE HTML FILE    – complete, in a single ```html code block (or numbered parts per 3.7).
                            File name: aerosim_{{ATA_TOPIC-slug}}.html
 PART D  SELF-TEST LOG    – tick each item of the checklist below with evidence (what you did to
                            confirm), then an INSTRUCTOR SHEET: 1-page run-of-show for
                            {{MINUTES}} minutes, answer key, and 5 extension questions.

 SELF-TEST CHECKLIST — work through it mentally (or by executing the code if you have a tool that
 can) on the finished file BEFORE you send Part C; if an item would fail, fix Part C first. Then
 report the evidence per item in Part D. A checklist item you could not verify must be reported as
 "UNVERIFIED — how to test it" rather than ticked.
   [ ] Page opens with no console errors; all four tabs render.
   [ ] Every named state in 0.5 can be reached and shows the correct buses live.
   [ ] Every control in 0.3 changes system state per 0.4; lights/legends match the notes.
   [ ] Signal trace from at least one load reaches the correct source in each scenario.
   [ ] Build mode: place, wire, run, meter, scope, undo, export/import, check-my-circuit all work.
   [ ] Fault lab: each fault produces the documented indications; debrief shows correct path.
   [ ] Learn mode: every step's completion condition fires; every quiz question grades correctly.
   [ ] URL-hash state round-trips; Reset restores defaults.
   [ ] Keyboard-only walkthrough possible; touch works; high-contrast mode legible.
   [ ] No number shown that is not in 0.7 or tagged "(assumed)".

If the INPUT BLOCK is missing the course notes, ask for them and stop. Otherwise begin with PART A.
```

---

## 3. Worked example of a filled INPUT BLOCK (A380 ATA 24)

```text
MODULE ......................: Aircraft Electrical & Digital Systems (Aerospace Electronics Diploma)
ATA CHAPTER / TOPIC .........: ATA 24 – Electrical Power System Introduction & AC/DC Generation
AIRCRAFT TYPE ...............: Airbus A380 (RR Trent 900)
TARGET LEVEL ................: CAAS SAR-66 Cat B2, Level 2 (Level 1 intro section included)
LEARNING OUTCOMES ...........: (derive from notes)
PREFERRED SIM ARCHETYPE .....: HYBRID (SYSTEM synoptic; zoom into BCRU/TR as CIRCUIT)
SESSION LENGTH ..............: 45
LANGUAGE / UNITS ............: English, SI
EXTRA CONSTRAINTS ...........: Must run inside a Brightspace iframe on student laptops and iPads; no CDN.
COURSE NOTES ................:
<<<COURSE_NOTES
[Paste the text of "Electrical Power System Introduction (1)" pp. 2–15 and
"AC & DC Generation Presentation (2)" pp. 2–23 from the A380 TTM here.
Key facts the model will pick up: four VFGs (150 kVA, 3-phase, 115 VAC, 370–770 Hz),
two APU GENs, up to four GPUs, four GGPCUs (connection/disconnection, voltage regulation,
protection, ECAM data, BITE), DRIVE and GEN P/BSWs on the overhead ELEC panel,
three BCRUs + three main BATs, one TR for abnormal DC supply, APU TR + APU BAT for APU start,
RAT + STAT INV for emergency, PEPDC / 2×SEPDC / 8×SPDB / Emergency Power Center distribution,
ELEC panel, BAT maintenance panel, EMER ELEC PWR panel, AC ELEC and DC ELEC ECAM pages.]
COURSE_NOTES>>>
```

What a good run looks like for this input: Part A lists ~20 components and the source-priority rules; Part B picks HYBRID; Part C is a page whose Explore tab shows the four VFGs, APU GENs, external power, the AC/DC networks and the ELEC overhead panel with working DRIVE/GEN/APU GEN/EXT PWR/BUS TIE pushbuttons; Build tab lets students assemble "DC generation from AC via BCRU" and a 3-phase TRU circuit; Fault Lab has VFG drive fault, GGPCU protection trip, BCRU failure → TR takeover, loss of all AC → RAT/STAT INV; Learn tab walks through normal → abnormal → emergency configurations with predict-observe-explain checkpoints.

---

## 4. Follow-up prompts for iteration

- "Regenerate PART C only. Keep the model; change: [list]."
- "Add a Level 3 layer: BITE messages from the notes pp. X–Y and an LRU-replacement task in Fault Lab."
- "Split this into two pages: (1) AC generation, (2) DC generation & distribution. Build page 1 now."
- "Convert the Build tab starter circuits to a 3-D isometric breadboard look (Diode style) using SVG isometric projection; keep the solver."
- "Produce a Brightspace-ready package: the HTML, a 300-word student brief, and a rubric aligned to the learning outcomes."
- "Harden for exams: disable Inspector hints, randomise fault seed by student ID, export results as CSV text."
- "Add an Arduino-style microcontroller block to Build mode with a tiny JS-interpreted sketch editor (digitalWrite/analogRead), so students can script a load-shed controller."

---

## Appendix A — Research summary

**What the video demonstrates.** Diode's Explore page: browse community circuits, open one, see a realistic 3D breadboard, place parts (resistor, LED, capacitor, transistor, 555, switch, motor, Arduino Uno), wire them, run the simulation, edit an Arduino sketch in a browser code editor, and fork the project. Its appeal is *physical realism + zero friction*; its limits were a small part library (no ESP32/Pico/STM32, no OLED/sensors), no SPICE-level AC/frequency analysis, and, as of now, the service is paused.

**Comparable tools and what the master prompt borrows from each**

| Tool | Simulation approach | Borrowed into the prompt |
|---|---|---|
| Diode (withdiode.com) | 3D breadboard, AVR emulation, community "Explore" gallery, in-browser code editor | Constructor UX, starter-circuit gallery, fork-and-modify, optional Arduino stub |
| Falstad / CircuitJS1 (GPL-2) | Real-time nodal solver with animated current dots and voltage colours; edit while running; scope on any node | Animated flow, live parameter sliders, probes/oscilloscope, MNA solver design |
| Wokwi / Tinkercad Circuits | Component inspector, palette, guided starter activities, Arduino sim | Inspector panel, guided activities, clean palette |
| CircuitVerse (MIT) | Digital logic with testbenches, assignments, grading, embeds | LOGIC archetype, "check my circuit" validation, results export |
| Sphaera Aircraft Electrical CBT | Clickable busbars/relays/generators/C-Bs/TRUs, automatic signal tracing, systems built up step by step for classroom teaching | SYSTEM archetype, signal tracing, build-up stepper, instructor projector mode |
| Tinkered.ai (Diode successor) | AI circuit generation from text, SPICE physics, 1,300+ boards, failure effects ("magic smoke") | Fault consequences made visible; generation-from-description philosophy |

**Design decisions this implies for TP.** A single self-contained HTML per topic (no hosting, no accounts, LMS-embeddable) is the lowest-friction route and matches how Brightspace pages are deployed. Aircraft-system topics need a *power-flow/state-machine* solver, not SPICE; electronics fundamentals need a *nodal* solver; the prompt therefore makes archetype selection explicit and allows HYBRID. Because the source material is Airbus training manual text (paired text + diagram pages, Level 1/2/3 granularity, precise ratings), the prompt forces a Phase 0 extraction step so every number and rule on screen traces back to the notes, and it forbids inventing aircraft data.

Sources: [Diode review (AutomatismosMundo)](https://automatismosmundo.com/en/diode-review-free-online-circuit-simulator-3d/) · [Tinkered vs Withdiode](https://www.tinkered.ai/withdiode) · [Free circuit simulators compared (FreeCircuitSim)](https://freecircuitsim.com/guides/best-free-circuit-simulators.html) · [Free online circuit simulators compared (DigiSim)](https://digisim.io/blog/free-online-circuit-simulators-compared) · [Sphaera Aircraft Electrical Systems CBT](https://www.sphaera.co.uk/elec.htm) · [Diode on Hacker News](https://news.ycombinator.com/item?id=47109247) · [Diode homepage (currently paused)](https://www.withdiode.com/)
