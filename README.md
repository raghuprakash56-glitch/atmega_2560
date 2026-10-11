# Smart Parking Assist and Slot Monitoring System

> **🥈 2nd Prize — Smart Parking Assist Hackathon 2026**

A microcontroller-based parking assistance prototype built around the **Arduino Mega 2560 (ATmega2560)**. The project combines sensor inputs, embedded decision logic, and visual/audio feedback. A major engineering focus was implementing and understanding low-level drivers rather than depending entirely on high-level Arduino libraries.

> **Repository note:** This package contains project documentation and a repository structure. Copy your final, tested source files and actual event photos/results into the marked folders before publishing. Hardware details marked *verify* should be checked against your final wiring.

## Contents

- [Project overview](#project-overview)
- [Features](#features)
- [Hardware and software](#hardware-and-software)
- [System architecture](#system-architecture)
- [Driver architecture](#driver-architecture)
- [Known pin plan](#known-pin-plan)
- [Build and run](#build-and-run)
- [Validation](#validation)
- [Achievement](#achievement)
- [Repository layout](#repository-layout)
- [Future improvements](#future-improvements)

## Project overview

Finding an available parking space and judging the distance to an obstacle can be difficult in crowded parking areas. This prototype explores sensor-based parking assistance using an ATmega2560 microcontroller. Sensor readings are processed by embedded C logic, then communicated through a seven-segment display and buzzer.

## Features

- Ultrasonic distance measurement for proximity feedback.
- IR/ADC-based slot sensing (threshold and sensor polarity must be validated on the actual hardware).
- Two-digit seven-segment display interface.
- Buzzer feedback for alerts.
- Modular drivers for GPIO, timer, sensors, display, and PWM where used.
- Register-level/bare-metal learning on the ATmega2560.
- Test and demo evidence can be added under `results/`.

## Hardware and software

| Item | Purpose |
|---|---|
| Arduino Mega 2560 / ATmega2560 | Main controller |
| HC-SR04 ultrasonic sensor | Distance measurement |
| IR sensor / analog output sensor | Parking-slot detection, depending on the final module |
| Two-digit seven-segment display | Numeric/status output |
| Buzzer | Audible alert |
| LEDs and resistors, if used | Status indication |
| Embedded C/C++ and AVR register access | Firmware |
| Arduino IDE or AVR toolchain | Build and upload |

Update this table to match the exact hardware used in the final demonstration.

## System architecture

```text
Ultrasonic sensor ─┐
IR / ADC sensor ───┼──> ATmega2560 application logic ──> 7-segment display
User/control input ┘                 │                  └─> Buzzer / status output
                                     └──> GPIO, Timer, ADC and PWM drivers
```

## Driver architecture

| Module | Responsibility |
|---|---|
| GPIO | Configure pins and read/write digital I/O |
| Timer | Provide timing/delay functions using AVR timer registers |
| Ultrasonic | Generate TRIG pulse and measure ECHO duration |
| ADC | Convert analog sensor voltage into a digital reading |
| IR / slot sensing | Read sensor values and classify a slot using a validated threshold |
| Seven-segment | Map digits to segments and refresh the two display digits |
| PWM | Generate a hardware timer waveform / control duty cycle if used by the final build |
| Main application | Combine sensor readings and determine output/alerts |

Keep each driver’s `.h` and `.c`/`.cpp` implementation together. Document register choices, prescaler, timer mode, and CPU clock assumptions in the relevant source comments.

## Known pin plan

The following assignments appeared in the development notes. **Confirm them against the final circuit before treating them as authoritative.**

| Signal | Arduino Mega pin | ATmega2560 mapping | Status |
|---|---:|---|---|
| HC-SR04 TRIG | D52 | PB1 | Previously discussed; verify final wiring |
| HC-SR04 ECHO | D51 | PB2 | Previously discussed; verify final wiring |
| IR digital output | D53 | PB0 | Previously discussed; verify final wiring |
| Buzzer | D12 or D13 was discussed | Depends on selected pin | Confirm final code/wiring |
| Seven-segment segments A–DP | D22–D29 proposed | PA0–PA7 | Proposed mapping; not confirmed wired |
| Seven-segment digit selects | D30–D31 proposed | PC7/PC6 | Proposed mapping; confirm display type and driver circuit |

Do not connect a seven-segment display directly without suitable current-limiting resistors and, where required, digit-driver transistors. Confirm common-anode/common-cathode type before choosing segment polarity.

## Build and run

1. Open the project in Arduino IDE or your configured AVR build environment.
2. Copy your **final tested** application and driver files into `src/` and `drivers/`.
3. Check that filenames and `#include` statements match exactly.
4. Verify `F_CPU` and the clock frequency assumed by the timer calculations. The common Mega 2560 board runs at 16 MHz, but confirm the selected board/build configuration.
5. Check pin mappings, sensor polarity, display type, and buzzer wiring.
6. Compile, upload, and test each driver independently before testing the integrated application.

This documentation package intentionally does not claim a verified build because the final source tree and circuit were not supplied with this request.

## Validation

Record actual measured outcomes; do not fill this section with assumed results.

- [ ] GPIO input/output tests passed
- [ ] Timer timing checked against a known reference or logic analyzer
- [ ] Ultrasonic distance compared against a ruler at several distances
- [ ] IR/ADC threshold tested for both occupied and free conditions
- [ ] Seven-segment digit mapping and refresh tested
- [ ] Buzzer alert conditions tested
- [ ] Integrated system tested under realistic conditions
- [ ] Photographs, demo video, and test evidence added to `results/`

See [`docs/test-plan.md`](docs/test-plan.md).

## Achievement

**🥈 Second Prize — Smart Parking Assist Hackathon 2026**

Add the official event name, organizer, date, team members, and a genuine certificate/prize photograph if available. Avoid publishing other participants’ faces or personal details without permission.

## Repository layout

```text
smart-parking-assist/
├── README.md
├── src/                 # Application entry point and integration
├── drivers/             # GPIO, timer, ADC, IR, ultrasonic, display, PWM
├── docs/                # Architecture, design notes, test plan, viva
├── hardware/            # Pin map and circuit/block diagrams
├── results/
│   ├── photos/
│   └── demo-video-link.md
├── presentation/        # Final PPT
├── poster/              # Final poster
├── LICENSE
└── .gitignore
```

## Future improvements

- Add robust filtering and timeout handling for ultrasonic measurements.
- Calibrate and document sensor thresholds from recorded data.
- Use a non-blocking periodic timer for display refresh and sensor sampling.
- Add more parking slots and a clear occupied/free indicator.
- Add a serial diagnostics mode and automated test checklist.
- Add a verified circuit diagram and measured timing screenshots.

## Credits

Developed as a team project for the Smart Parking Assist hackathon. Update this section with team member names, roles, and acknowledgements before publishing.

# atmega_2560