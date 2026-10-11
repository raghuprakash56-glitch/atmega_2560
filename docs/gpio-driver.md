# GPIO Driver Notes

The GPIO driver abstracts direction and pin state operations.

Typical operations:
- Configure a pin as input or output.
- Write HIGH/LOW to an output.
- Read the current digital input.
- Toggle an output where supported.

On AVR, each port commonly has DDRx (direction), PORTx (output/pull-up control), and PINx (input state) registers. A set bit in DDRx selects output; a cleared bit selects input. For an input, setting the corresponding PORTx bit enables the internal pull-up.

## Review checklist
- Use `volatile` for memory-mapped hardware registers.
- Use bit masks such as `(1U << pin)` and preserve unrelated bits with read-modify-write operations.
- Validate the port/pin range.
- Do not assume Arduino digital pin numbers are identical to port bit numbers.
- Keep register addresses and definitions consistent with the ATmega2560 datasheet and compiler headers.
