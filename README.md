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

## Adding a new simulation

1. Open Claude and paste Section 2 of [`AeroSim_Master_Prompt.md`](AeroSim_Master_Prompt.md).
2. Fill the INPUT BLOCK and paste one topic of course notes into `{{COURSE_NOTES}}`.
3. Review PART A (system model) and PART B (design brief) before accepting PART C (the HTML).
4. Save the HTML as `ataNN-topic.html` in the repo root, add a card to `index.html` and a row to the table above, commit and push. GitHub Pages redeploys automatically.

The `ata24-part-*.md` files hold the PART A/B and PART D outputs from each generation run so the model, assumptions and self-test evidence are traceable.

## Embedding in an LMS (Brightspace)

Either link to the live page, or embed it:

```html
<iframe src="https://daniellow1987-ship-it.github.io/A380-Systems/aerosim_ata24_electrical_power.html"
        width="100%" height="900" style="border:0" allowfullscreen></iframe>
```

State is mirrored to the URL hash, so a link to a specific scenario or fault can be shared.

## Licence and attribution

Teaching material is paraphrased from training documentation; no manual pages or logos are reproduced. Any value not present in the source notes is tagged "(assumed)" in the UI. © Daniel Low, Temasek Polytechnic — training use.
