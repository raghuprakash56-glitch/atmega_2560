# PWM Notes

Pulse-width modulation (PWM) controls the average power delivered to a load by switching a digital output on and off.

`duty_cycle (%) = (ON time / total period) × 100`

At 25% duty cycle, the signal is HIGH for one quarter of each period and LOW for the remaining three quarters (for a non-inverting output). Frequency determines how often the cycle repeats; duty cycle determines the fraction of time spent active.

On the ATmega2560, hardware PWM is produced by timer/counter peripherals and their output-compare pins. Correct setup generally requires:
1. Configure the output pin direction.
2. Select the waveform generation mode.
3. Select the clock source/prescaler.
4. Set the output compare value and output mode.
5. Enable the timer clock and verify the output.

The exact register bits and formula depend on the chosen timer mode and whether TOP is fixed, `ICRn`, or `OCRnA`. Document the specific timer/channel used by the final firmware; do not claim PWM is used in the final prototype unless it is actually integrated.
