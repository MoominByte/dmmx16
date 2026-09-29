# BenchScan DMMX16

BenchScan DMMX16 is a digital multimeter switching card inspired by the functional architecture of the SIGLENT SC1016. It provides 16 measurement channels: 12 multipurpose channels and 4 fuse-protected current channels.

## Project status

- Schematic revision: **DRAFT-1**
- File format: **KiCad 10**
- Hierarchical schematic converted and saved
- ERC: **0 errors and 18 off-grid warnings** from the custom MOSFET symbols
- PCB: **220 × 110 mm**, four copper layers, with all 113 footprints placed on the top side
- Preliminary placement completed; routing and manufacturing files have not started

This project is not ready for manufacturing.

## Opening the project

Open `BenchScan_DMMX16.kicad_pro` with KiCad 10. The modern root schematic is `BenchScan_DMMX16.kicad_sch`.

The legacy `.sch` files are retained as conversion sources. The earlier architecture-only draft is preserved under `archive/architecture-notes-draft0/`.

## Architecture

### Control

- Main module: Seeed Studio XIAO ESP32-C6, U1
- D0 / GPIO0: serial data `SER`
- D1 / GPIO1: shift clock `SRCLK`
- D2 / GPIO2: register clock `RCLK`
- D3 / GPIO21: active-low output enable `/OE`
- D4 / GPIO22: direct K17 control
- U2 and U3: two SN74HC595 shift registers powered by the XIAO 3.3 V output
- U2 controls K1-K8 and U3 controls K9-K16

Each relay is driven by a 2N7002K MOSFET with a 100 ohm series gate resistor, a 47 kohm gate pull-down, and a 1N4148W flyback diode. K17 uses the same driver circuit but receives its control signal directly from the XIAO.

### Measurement channels

| Connector | Channels | Purpose |
| --- | --- | --- |
| J1 | CH1-CH4 | Voltage, resistance, frequency, capacitance, diode, continuity, and temperature |
| J2 | CH5-CH8 | Multipurpose measurement and associated SENSE channels |
| J3 | CH9-CH12 | Multipurpose measurement and associated SENSE channels |
| J4 | CH13-CH16 | Current measurement, provisional 500 mA maximum |

Each J1-J4 connector has eight positions at 5.00 mm pitch: one `HI` and one `LO` terminal for each of its four channels.

### Switching

- K1-K16 use normally open contacts.
- K1-K6 route directly to `INPUT_HI` and `COM`.
- K7-K12 are routed through K17.
- With K17 de-energized, K7-K12 are routed to `INPUT_HI` and `COM`.
- With K17 energized, K7-K12 are routed to `SENSE_HI` and `SENSE_LO`.
- The four-wire pairs are CH1+CH7, CH2+CH8, CH3+CH9, CH4+CH10, CH5+CH11, and CH6+CH12.
- K13-K16 route the current channels to `CURRENT_HI` and `CURRENT_LO`.

Firmware must prevent multiple channels from being connected to the same destination bus at the same time, except for one valid four-wire pair.

### Current-channel protection

F1-F4 are Littelfuse `0451.500MRL` fast-acting 500 mA, 125 V fuses. They must not be replaced by 0.1 ohm resistors without a new circuit and safety analysis.

### DMM interface

J5 and the six banana jacks expose:

- `INPUT_HI`
- `COM`
- `SENSE_HI`
- `SENSE_LO`
- `CURRENT_HI`
- `CURRENT_LO`

R50 is a default-fitted 0 ohm link between `CURRENT_LO` and `COM`, with accessible test points planned on both sides.

### Power

- The XIAO is powered through its USB-C connector.
- The barrel jack supplies only the `+5V_RELAY` rail through F6 and Q19.
- USB, logic, and relay grounds are common.
- The external 5 V supply is not connected directly to the XIAO VBUS pin, preventing backfeed into USB.

## Schematic structure

- `01_power_control.kicad_sch`: XIAO, shift registers, and power supply
- `02_relay_drivers.kicad_sch`: 17 relay-coil drivers
- `03_voltage_channels.kicad_sch`: CH1-CH12 and normal/sense selection
- `04_current_dmm_interface.kicad_sch`: CH13-CH16, fuses, and DMM interface

Supporting documents:

- `BOM_AUDIT.md`: bill-of-materials review
- `CONNECTOR_PINOUT.csv`: J1-J4 pin assignments
- `SWITCHING_TRUTH_TABLE.md`: switching truth table
- `PLACEMENT_CONSTRAINTS.md`: mechanical and placement constraints
- `SC1016_REFERENCE.md`: SC1016 reference specifications
- `erc-placement.json`: latest automated ERC report
- `drc-placement.json`: preliminary placement DRC report (routing intentionally incomplete)
- `LIBRARY_SOURCES.md`: footprint provenance and manufacturer references

## Required before routing

1. Align the custom MOSFET symbol pins to eliminate the 18 ERC off-grid warnings.
2. Verify the gate, source, and drain pin mapping of Q1-Q19 against the selected SOT-23 footprint.
3. Mechanically verify the four project-created footprints against physical samples or manufacturer drawings before ordering boards.
4. Confirm voltage limits, creepage and clearance requirements, trace-width rules, and internal plane strategy.
5. Review and refine the preliminary placement, especially edge access and measurement-signal return paths.
6. Complete a manual schematic and PCB review before routing and manufacturing-output generation.

## Warning

The SC1016 ratings are used only as a functional reference. They do not certify the electrical limits of this board. A complete safety and manufacturability review is required before ordering PCBs.
