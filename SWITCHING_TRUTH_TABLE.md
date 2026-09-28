# Switching truth table - DRAFT-1

All K1-K16 signal contacts are normally open. Only the selected relay is energized, except for a deliberate 4-wire pair.

| Mode | Energized channel relay(s) | K17 | DMM destination |
| --- | --- | --- | --- |
| Normal CH1-CH6 | One of K1-K6 | OFF | INPUT_HI / COM |
| Normal CH7-CH12 | One of K7-K12 | OFF | INPUT_HI / COM |
| 4-wire CH1 | K1 + K7 | ON | K1 -> INPUT_HI/COM; K7 -> SENSE_HI/SENSE_LO |
| 4-wire CH2 | K2 + K8 | ON | K2 -> INPUT_HI/COM; K8 -> SENSE_HI/SENSE_LO |
| 4-wire CH3 | K3 + K9 | ON | K3 -> INPUT_HI/COM; K9 -> SENSE_HI/SENSE_LO |
| 4-wire CH4 | K4 + K10 | ON | K4 -> INPUT_HI/COM; K10 -> SENSE_HI/SENSE_LO |
| 4-wire CH5 | K5 + K11 | ON | K5 -> INPUT_HI/COM; K11 -> SENSE_HI/SENSE_LO |
| 4-wire CH6 | K6 + K12 | ON | K6 -> INPUT_HI/COM; K12 -> SENSE_HI/SENSE_LO |
| Current CH13-CH16 | One of K13-K16 | OFF | CURRENT_HI / CURRENT_LO |

Interlock rules: never energize more than one relay on a shared destination bus, except the valid 4-wire pair shown above. Never switch a current channel while a voltage/sense channel is active unless the DMM interface is explicitly designed and verified for that state.
