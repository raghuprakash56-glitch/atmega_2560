# System Architecture

```text
Sensors
  ├── Ultrasonic TRIG/ECHO
  └── IR / analog sensor
          │
          ▼
   Sensor driver layer
  ├── ultrasonic driver
  ├── ADC driver
  └── IR/slot driver
          │
          ▼
   Application decision logic
          │
          ├── Seven-segment driver
          ├── Buzzer / GPIO driver
          └── PWM driver (if used)
```

## Layer responsibilities
- **Hardware layer:** ATmega2560 registers and physical pins.
- **Driver layer:** reusable GPIO, timer, ADC, ultrasonic, display, and PWM routines.
- **Application layer:** interprets sensor values and chooses the output state.
- **Evidence layer:** test results, photos, circuit diagram, and demo link.

Keep hardware-specific register definitions in one place and avoid defining the same register or function in multiple source files.
