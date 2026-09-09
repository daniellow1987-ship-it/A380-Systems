# A380 Systems Simulator

Interactive, browser-based simulations of aircraft systems and electronics for aerospace maintenance and diploma teaching — one simulation per ATA chapter/topic. Each simulation is a **single self-contained HTML file** (vanilla JS + inline SVG, no CDN, no build step, no login) with four modes:

| Mode | What the student does |
|---|---|
| **Explore** | Live ECAM-style schematic with animated power flow, clickable overhead-panel pushbuttons, scenario selector, signal tracing, component inspector, build-up stepper |
| **Build** | Drag-and-drop constructor with wiring, run/pause, meters, starter circuits, "check my circuit", JSON export/import |
| **Fault Lab** | Instructor injects faults; student isolates with multimeter, C/Bs and ECAM; efficiency score and debrief |
| **Learn** | Guided lesson rail with predict-observe-explain checkpoints and an auto-graded quiz mapped to learning outcomes |

**Live site:** https://daniellow1987-ship-it.github.io/A380-Systems/

## Simulations

| ATA | Topic | Aircraft | Level | File |
|---|---|---|---|---|
| 24 | Electrical Power System — Introduction & AC/DC Generation | A380 (RR Trent 900) | SAR-66 B2, Level 2 | [`aerosim_ata24_electrical_power.html`](aerosim_ata24_electrical_power.html) |
| 31 | Control & Display System — EFIS, ECAM, DU reconfiguration | A380 (RR Trent 900) | SAR-66 B2, Level 2 | [`aerosim_ata31_control_display_system.html`](aerosim_ata31_control_display_system.html) |
| 31 | Flight Warning System — alert levels, flight phases, inhibition | A380 (RR Trent 900) | SAR-66 B2, Level 2 | [`aerosim_ata31_flight_warning_system.html`](aerosim_ata31_flight_warning_system.html) |

| 34 | ADIRS &amp; Standby Navigation | A380 (RR Trent 900) | SAR-66 B2, Level 2 | [`aerosim_ata34_adirs_standby_nav.html`](aerosim_ata34_adirs_standby_nav.html) |
| 34 | Radio Navigation Aids — MMR, VOR/Marker, DME, ADF, radio altimeter, OANS | A380 (RR Trent 900) | SAR-66 B2, Level 2 | [`aerosim_ata34_radio_nav_aids.html`](aerosim_ata34_radio_nav_aids.html) |
| 34 | Aircraft Environment Surveillance System | A380 (RR Trent 900) | SAR-66 B2, Level 2 | [`aerosim_ata34_aess_surveillance.html`](aerosim_ata34_aess_surveillance.html) |

Both ATA 31 and ATA 34 are split across several pages because each chapter covers far more than the master prompt's one-page limit of roughly 14 sources/buses/conversion units or three distinct sub-systems. ATA 34 follows the manual's own three-part division — the ADIRS and standby group, the radio navigation aids, and the surveillance system. Still to be built: the ATA 31 Flight Data Recording System, Electrical Clock, Tail Strike Indication and Interface for Video.

## Adding a new simulation

1. Open Claude and paste Section 2 of [`AeroSim_Master_Prompt.md`](AeroSim_Master_Prompt.md).
2. Fill the INPUT BLOCK and paste one topic of course notes into `{{COURSE_NOTES}}`.
3. Review PART A (system model) and PART B (design brief) before accepting PART C (the HTML).
4. Save the HTML as `ataNN-topic.html` in the repo root, add a card to `index.html` and a row to the table above, commit and push. GitHub Pages redeploys automatically.

The `ata*-part-*.md` files hold the PART A/B and PART D outputs from each generation run so the model, assumptions and self-test evidence are traceable:

- `ata24-part-a-b-system-model.md`, `ata24-part-d-selftest-instructor-sheet.md`
- `ata31-cds-part-a-b-system-model.md`, `ata31-cds-part-d-selftest-instructor-sheet.md`
- `ata31-fws-part-a-b-system-model.md`, `ata31-fws-part-d-selftest-instructor-sheet.md`
- `ata34-adirs-part-a-b-system-model.md`, `ata34-radionav-part-a-b-system-model.md`, `ata34-aess-part-a-b-system-model.md`, and one combined `ata34-part-d-selftest-instructor-sheet.md`

Each PART A lists every component, connection, control, rule, state and number extracted from the notes, plus a **GAPS** table naming everything the notes do not state and the conservative assumption used in its place. Every one of those assumptions is tagged "(assumed)" where it appears in the simulation. Each PART D carries the headless-browser self-test log and a one-page instructor run of show with the answer key and extension questions.

## Embedding in an LMS (Brightspace)

Either link to the live page, or embed it:

```html
<iframe src="https://daniellow1987-ship-it.github.io/A380-Systems/aerosim_ata24_electrical_power.html"
        width="100%" height="900" style="border:0" allowfullscreen></iframe>
```

State is mirrored to the URL hash, so a link to a specific scenario or fault can be shared.

## Licence and attribution

Teaching material is paraphrased from training documentation; no manual pages or logos are reproduced. Any value not present in the source notes is tagged "(assumed)" in the UI. © Daniel Low, Temasek Polytechnic — training use.
