# Component library sources

The project keeps the exact footprints used by the design in local KiCad libraries so the design remains reproducible.

| Part | Project library | Source | Notes |
|---|---|---|---|
| Phoenix Contact 1190370 | `BenchScan_Connectors.pretty` | [Phoenix Contact product data](https://www.phoenixcontact.com/en-pc/products/pcb-terminal-block-lpta-25-8-50-1190370) | Project footprint based on the manufacturer dimensions: 8 positions, 5.00 mm pitch, 1.30 mm PCB holes, 41.5 × 21.35 mm body envelope. |
| Seeed Studio XIAO ESP32-C6 | `Seeed_XIAO.pretty` | [Seeed Studio OPL KiCad Library](https://github.com/Seeed-Studio/OPL_Kicad_Library) | Official `XIAO-ESP32-C6-SMD.kicad_mod` footprint. Pads 15–24 are optional underside module contacts and remain unconnected in this design. |
| Würth Elektronik 691137710006 | `Wurth_Connectors.pretty` | [Würth Elektronik KiCad Library](https://github.com/WurthElektronik/KiCad-Library) | Official footprint and STEP model; model path changed only to use the project-local copy. |

Imported vendor files should not be geometrically modified without checking the current manufacturer drawing and recording the change here.
