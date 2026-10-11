# Pin Configuration

These are development notes, not a substitute for the final schematic. Verify each assignment against the final build.

| Signal | Proposed/previous pin | MCU mapping | Verification |
|---|---|---|---|
| Ultrasonic TRIG | D52 | PB1 | Verify |
| Ultrasonic ECHO | D51 | PB2 | Verify |
| IR digital output | D53 | PB0 | Verify |
| Seven-segment A–DP | D22–D29 | PA0–PA7 | Proposed; verify |
| Seven-segment digit select | D30–D31 | PC7/PC6 | Proposed; verify |
| Buzzer | D12 or D13 discussed | Depends on selected pin | Confirm final source |

Document sensor model, display type, active polarity, resistor/transistor circuit, and supply voltage once confirmed.
