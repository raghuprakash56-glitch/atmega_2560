# Two-Digit Seven-Segment Driver Notes

A seven-segment display has segments A–G and usually DP. A two-digit multiplexed display shares segment lines and enables one digit at a time quickly enough that both appear illuminated.

Before wiring:
1. Identify common-anode or common-cathode type from the part number or a multimeter test.
2. Use current-limiting resistors.
3. Confirm whether digit enables require transistor drivers.
4. Confirm active-HIGH/active-LOW logic in the driver.

A refresh routine should activate one digit, set the segment pattern, then switch to the other digit on a regular schedule. Avoid long blocking delays that cause flicker. The development notes proposed segment pins D22–D29 and digit enables D30–D31; verify these against the final wiring and code.
