# BOM audit — DRAFT-0

The imported BOM is the source of truth for references and manufacturer part numbers below. This starter schematic does not silently add unspecified parts.

## Items consistent with the intended architecture

| Function | BOM evidence |
| --- | --- |
| Main controller | U1 Seeed Studio XIAO ESP32-C6, 113991254 |
| Relay matrix | K1–K17 KEMET UD2-5NE, 5 V DPDT |
| Coil clamps/drivers | D1–D17 1N4148W-13-F; Q1–Q17 2N7002K; 100 R gate series R1–R17; 47 k pull-down R18–R34 |
| Current protection | F1–F4 Littelfuse 0451.500MRL, 500 mA fast 125 V |
| Universal DMM port | J5 six-position terminal, J6/J9/J11 red and J8/J10/J12 black Pomona banana jacks, R50 0 R CURRENT_LO–COM link |
| Power input | J7 5.5/2.1 mm barrel, F6 resettable fuse, Q19 AO3401A, D19 SMBJ5.0A, C7 47 uF |

## User-confirmed architecture

1. U2/U3 run from the XIAO 3V3 output and control K1-K16 through their individual MOSFET drivers.
2. K17 uses a dedicated XIAO GPIO and its existing MOSFET driver, so the two 74HC595 are sufficient.
3. K1-K16 contacts are normally open. K1-K12 are voltage/multipurpose channels; K13-K16 are current channels.
4. K17 selects whether the K7-K12 relay bus is sent to normal INPUT_HI/COM or SENSE_HI/SENSE_LO.
5. Four-wire resistance pairs are CH1+CH7 through CH6+CH12, matching the SC1016 functional reference.
6. F1-F4 remain Littelfuse 0451.500MRL fast-acting 500 mA fuses; they are not replaced by 0.1 ohm resistors.

## Still required before manufacturing release

1. **GPIO validation:** confirm the proposed XIAO pins D0-D4 against ESP32-C6 boot strapping, USB operation and firmware needs. K17 must remain off during reset/boot.
2. **Connector identity:** the user image shows 16 terminals per connector (four channels times four terminals). Confirm manufacturer part 1190370 and footprint pin numbering because the BOM role text also calls it an 8-position connector.
3. **Electrical ratings:** define the promised input limits and required creepage/clearance. The SC1016 reference states 125 Vrms/175 Vpeak AC, 110 VDC and 62.5 VA/30 W, but those values are not automatically valid for this PCB.
4. **Current rating:** the user selected the BOM's 500 mA F1-F4 protection. CH13-CH16 therefore have a provisional 500 mA maximum rating, even though the SC1016 reference permits continuous current below 2.2 A. Verify relay, connector, copper and fault ratings before release.
5. **Physical parts:** obtain verified KiCad symbols/footprints and dimensional drawings for U1, J1-J5, J7 and banana jacks; confirm edge and mating clearances.
6. **Safety switching policy:** firmware interlocks must enforce one active channel per destination bus, and paired closures only for valid 4-wire combinations.

## Explicit draft assumptions

- Relay de-energized is the safe, unselected state.
- R50 is fitted by default, with accessible pads to isolate CURRENT_LO from COM when a DMM requires it.
- J1–J4 are placed left-to-right. Relay banks sit immediately above their associated field connector.
- USB-C of U1, J7, J5, and six banana jacks share the top board edge zone; no components are planned on the bottom side.
