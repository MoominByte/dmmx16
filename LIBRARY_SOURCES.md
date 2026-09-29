# Component library sources

The project keeps the exact footprints used by the design in local KiCad libraries so the design remains reproducible.

| Part | Project library | Source | Notes |
|---|---|---|---|
| Phoenix Contact 1190370 | `BenchScan_Connectors.pretty` | [Phoenix Contact product data](https://www.phoenixcontact.com/en-pc/products/pcb-terminal-block-lpta-25-8-50-1190370) | Project footprint based on the manufacturer dimensions: 8 positions, 5.00 mm pitch, 1.30 mm PCB holes, 41.5 × 21.35 mm body envelope. |
| Seeed Studio XIAO ESP32-C6 | `Seeed_XIAO.pretty` | [Seeed Studio OPL KiCad Library](https://github.com/Seeed-Studio/OPL_Kicad_Library) | Official `XIAO-ESP32-C6-SMD.kicad_mod` footprint. Pads 15–24 are optional underside module contacts and remain unconnected in this design. |
| Würth Elektronik 691137710006 | `Wurth_Connectors.pretty` | [Würth Elektronik KiCad Library](https://github.com/WurthElektronik/KiCad-Library) | Official footprint and STEP model; model path changed only to use the project-local copy. |
| KEMET/YAGEO UD2-5NE | `BenchScan_Custom.pretty` | [UC2/UD2 datasheet](https://content.kemet.com/datasheets/KEM_R7005_UC2_UD2.pdf) | Project footprint follows the UD2 NU/NE top-view land pattern: 8 SMD pads, 6.74 mm row spacing, 3.2/2.2/2.2 mm column spacing, 0.8 x 1.86 mm pads. |
| Pomona 73099 | `BenchScan_Custom.pretty` | [Pomona 73099 datasheet](https://www.pomonaelectronics.com/files/datasheets/d73099_101.pdf) | Project footprint follows the manufacturer panel/PCB drilling: four common 1.30 mm electrical holes on a 10.16 x 3.80 mm rectangle and one 2.20 mm mechanical hole. |
| Tensility 54-00129 | `BenchScan_Custom.pretty` | [Tensility 54-00129 specification](https://tensility.s3.us-west-2.amazonaws.com/imports/product_spec_sheets/54-00129.pdf) | Project footprint uses the manufacturer PCB layout for terminals A, C and switched terminal B. |
| Littelfuse 0451.500MRL | `BenchScan_Custom.pretty` | [Littelfuse 451/453 datasheet](https://www.littelfuse.com/assetdocs/fuse-451-and-453-datasheet?assetguid=533cd5cc-956c-4243-867f-6ab5a62f6ba1) | Project footprint follows the recommended NANO2 2410 pad layout. |

Imported vendor files should not be geometrically modified without checking the current manufacturer drawing and recording the change here.
