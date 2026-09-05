# 555 Servo Controller

A compact KiCad PCB design that generates servo control pulses using a 555 timer; includes schematic, PCB layout, 3D views, ERC/DRC reports, BOM, and fabrication files.

> Project status: PCB design completed — not yet manufactured or physically tested.

[![License: CERN-OHL-S-2.0](https://img.shields.io/badge/License-CERN--OHL--S--2.0-blue.svg)](LICENSE) [![KiCad version](https://img.shields.io/badge/KiCad-10.0-brightgreen.svg)](https://kicad.org) [![repo size](https://img.shields.io/github/repo-size/shlok-ac/Servo-Controller-555)](https://github.com/shlok-ac/Servo-Controller-555) [![issues](https://img.shields.io/github/issues/shlok-ac/Servo-Controller-555)](https://github.com/shlok-ac/Servo-Controller-555/issues)

## TL;DR
- Designed in KiCad 10.0; 555-timer generates servo PWM controlled via potentiometer.
- Repo includes KiCad project, 3D model, gerbers, BOM, ERC/DRC reports.
- Design has passed KiCad ERC/DRC but has not been manufactured or bench-tested.

## Table of contents
- [Quick links](#quick-links)
- [Quick start](#quick-start)
- [Open in KiCad](#open-in-kicad)
- [Files included](#files-included)
- [Features](#features)
- [PCB & Circuit overview](#pcb--circuit-overview)
- [Design verification](#design-verification)
- [Fabrication & manufacturing notes](#fabrication--manufacturing-notes)
- [BOM & sourcing](#bom--sourcing)
- [How to test / Validation plan](#how-to-test--validation-plan)
- [Important notes](#important-notes)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [License](#license)
- [Author](#author)

## Quick links
- Schematic PDF — documentation/schematic.pdf
- PCB layout PDF — documentation/pcb-layout.pdf
- 3D front — assets/pcb-3d-front.png
- 3D back — assets/pcb-3d-back.png
- Gerbers — fabrication/gerbers/
- Drill files — fabrication/drills/
- BOM — fabrication/BOM.csv
- Position (Pick-and-Place) — fabrication/position.csv
- ERC report — documentation/verification/ERC.rpt
- DRC report — documentation/verification/DRC.rpt

## Quick start
If you just want to inspect or share the design quickly:
1. Browse the PDFs in `documentation/` (schematic & PCB layout).
2. Preview 3D renders in `assets/` or open KiCad's 3D viewer for the full model.
3. Review `fabrication/BOM.csv` and `fabrication/position.csv` to prepare for ordering.
4. Inspect gerbers in `fabrication/gerbers/` with your preferred Gerber viewer and confirm vendor settings.

## Open in KiCad
(Recommended KiCad version: 10.0)
1. Clone or download the repository:
   git clone https://github.com/shlok-ac/Servo-Controller-555.git
2. Open KiCad, then open the project file:
   - `Servo Controller 555.kicad_pro`
3. From the KiCad Project Manager you can open:
   - Schematic Editor (view/edit schematic)
   - PCB Editor (view/edit layout and 3D with STEP models)
4. If 3D models are missing, point footprint 3D model paths to the `external-cad/` folder in footprint properties.

## Files included
<details>
<summary>Repository structure</summary>

```text
Servo-Controller-555/
│
├── .gitattributes
├── .gitignore
├── LICENSE
├── README.md
├── Servo Controller 555.kicad_pcb
├── Servo Controller 555.kicad_pro
├── Servo Controller 555.kicad_sch
├── assets/
│   ├── pcb-3d-front.png
│   ├── pcb-3d-back.png
│   ├── schematic.png
│   └── pcb-layout.png
├── documentation/
│   ├── schematic.pdf
│   ├── pcb-layout.pdf
│   └── verification/
│       ├── ERC.rpt
│       └── DRC.rpt
├── fabrication/
│   ├── gerbers/
│   ├── drills/
│   ├── BOM.csv
│   └── position.csv
└── external-cad/
    └── Potentiometer_Bourns_PTV09A-1_Single_Vertical.step
```

</details>

## Features
- 555 timer based servo controller
- Adjustable servo control using a potentiometer
- Through-hole and SMD components
- Custom footprints and external STEP model for 3D viewer
- ERC and DRC verification reports
- Fabrication files, BOM, and pick-and-place

## PCB & Circuit overview
The circuit uses a 555 timer to generate servo PWM; a potentiometer changes the pulse width to vary servo position. See `assets/schematic.png` or `documentation/schematic.pdf` for details.

![pcb-3d-front](assets/pcb-3d-front.png "Front 3D view of the PCB")

### Footprints & libraries
- Footprints use the standard KiCad 10.0 libraries where possible.
- Custom footprints and any third-party footprints are included in the KiCad project files or documented in the BOM/footprint fields. If you depend on external library packages, note them in this README or add a `CONTRIBUTING.md` with exact library versions.

## Design verification
- ERC: Errors 0, Warnings 0 — documentation/verification/ERC.rpt
- DRC: Violations 0 — documentation/verification/DRC.rpt

> Note: KiCad checks validate the CAD rules; they are not a replacement for physical testing after fabrication.

## Fabrication & manufacturing notes
- Recommended: 2-layer FR-4, 1.6 mm, 1 oz copper.
- Typical fab settings: 6/6 mil track/space (confirm with your board house).
- Soldermask and silkscreen enabled.
- Recommended finish: HASL or ENIG (confirm with your assembler/soldering needs).
- Verify gerbers in a viewer (e.g., Gerbv or KiCad's Gerber viewer) and check with your manufacturer for edge clearance and drill tolerances.
- For tighter tolerances, consult your fab's capabilities and adjust design rules before ordering.

## BOM & sourcing
- See `fabrication/BOM.csv` for references, values, and footprints.
- BOM column notes (recommended):
  - Reference (designator)
  - Value/Description
  - Footprint
  - Quantity
  - Suggested part number / Supplier (add Digi-Key / Mouser PN if available)
  - Notes (e.g., alternate parts, tolerance)

Consider updating BOM with supplier part numbers to make ordering reproducible.

## How to test / Validation plan
These are the planned checks to validate a manufactured board. Perform these after you have a physical PCB and components:

1. Visual inspection
   - Check silkscreen, component orientation, missing or misaligned parts, soldermask issues.
2. Power smoke test
   - Assemble power section only (no microcontrollers/servos) and apply regulated supply. Verify no excessive current draw or overheating.
3. Basic signal check
   - Probe the 555 output with an oscilloscope or logic probe. Verify pulse width range and frequency when adjusting the potentiometer.
   - Confirm pulse amplitude is 0–Vcc as expected and duty cycle falls within servo PWM range.
4. Servo functional test
   - Connect a standard hobby servo to the output and confirm it moves across expected range when potentiometer is adjusted.
   - Measure current drawn by the servo under no-load and typical-load conditions; ensure power traces and regulators (if any) are adequate.
5. Full system test
   - Test connectors, mechanical fit, mounting holes, and any connectors intended for integration.
6. Report
   - Document results and update `documentation/` with photos, measurements, and any design changes. If issues are found, open an issue in the repo with steps to reproduce and suggested fixes.

## Important notes
(Please paste any additional important notes you added here; you can paste them in a follow-up message and I'll insert them verbatim.)
- [PLACEHOLDER — paste your "important notes" text here]

## Contributing
Contributions welcome — open issues or PRs. For larger changes:
- Create a branch: `feature/xxx` or `fix/xxx`
- Update documentation and BOM
- Add verification notes and updated PDFs

If you'd like, I can add a `CONTRIBUTING.md` file and basic issue/PR templates.

## Changelog
- v0.1 — Initial PCB design and documentation (KiCad 10.0). (Add future entries here as you iterate.)

## License
Copyright © 2026 Shlok Chorge

This project is licensed under the CERN Open Hardware Licence Version 2 – Strongly Reciprocal (CERN‑OHL‑S‑2.0). See `LICENSE` for full text.

## Author
Shlok Chorge — https://github.com/shlok-ac
