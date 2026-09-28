# SIGLENT SC1016 reference - DS60030-E02B

This document is a design reference, not a claim that BenchScan DMMX16 already meets the same ratings.

## Functional reference

- 12 multipurpose channels, CH1-CH12: DCV, ACV, 2-wire and 4-wire resistance, capacitance, frequency, diode, continuity, thermocouple and RTD.
- 4 current-only channels, CH13-CH16: DCI and ACI.
- Six 4-wire pairs: CH1 input + CH7 sense, CH2 + CH8, CH3 + CH9, CH4 + CH10, CH5 + CH11, CH6 + CH12.
- Current range in the SC1016 documentation: 2 A range only; continuous current below 2.2 A.

## Published SC1016 reference ratings

| Parameter | SC1016 value |
| --- | --- |
| Maximum AC input | 125 Vrms or 175 Vpeak, 100 kHz |
| AC switched load | 0.3 A, 125 VA resistive |
| Maximum DC input | 110 V |
| DC switched load | 1 A at 30 VDC resistive |
| Maximum switching voltage | 250 VAC / 220 VDC |
| Maximum switching power | 62.5 VA / 30 W |
| Contact resistance | 75 milliohm maximum at 6 VDC, 1 A |
| Actuation | 5 ms maximum on/off |
| Insulation resistance | 1 gigaohm minimum at 500 VDC |

## BenchScan implications

- The functional channel grouping and 4-wire pairing are adopted.
- The electrical ratings are design targets only until verified against the actual UD2-5NE relays, connectors, fuses, PCB clearances, copper geometry and enclosure.
- The selected design retains four Littelfuse 0451.500MRL fast fuses. CH13-CH16 therefore remain provisionally limited to 500 mA and BenchScan must not be labeled as a 2 A scanner.
