# PCB placement constraints — pre-layout

- Outline: **220.0 × 110.0 mm**; four copper layers; components on top only.
- Top edge, left to right within the instrument/power zone: the XIAO USB-C must face the top edge, adjacent to J7 barrel input; J5 and the six DMM banana jacks are also top-edge parts near the XIAO.
- Field connectors J1, J2, J3, J4 must be aligned from left to right on one row. Their relay groups must be directly above them.
- Reserve sufficient edge clearance for USB plug, barrel plug and safety-banana mating bodies before routing.
- Use an uninterrupted internal GND reference plane; keep relay coil returns away from DMM measurement returns and relay-contact paths.
- Do not start routing or generate manufacturing outputs until `BOM_AUDIT.md` open items 1–6 are resolved and the schematic has passed ERC after conversion to the installed KiCad version.
