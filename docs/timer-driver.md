# Timer Driver Notes

The timer driver provides repeatable timing using an AVR hardware timer.

For a compare-match timer in CTC mode, the timer counts from zero until the compare value, then resets. A common timing relationship is:

`compare interval = (OCRnA + 1) × prescaler / F_CPU`

For example, with a 16 MHz clock, prescaler 64, and `OCR1A = 249`:

- Timer clock = 16,000,000 / 64 = 250,000 Hz
- Compare interval = (249 + 1) / 250,000 = 0.001 s = 1 ms

This result assumes the timer is configured correctly for CTC mode and the selected clock/prescaler bits match the calculation. A delay routine that waits for compare flags must clear/check flags correctly and must not accidentally reuse a timer configured for PWM.
