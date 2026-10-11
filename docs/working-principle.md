# Working Principle

1. Initialize the required GPIO directions and peripheral registers.
2. Trigger an ultrasonic measurement and measure the ECHO pulse duration, using a timeout so the program cannot wait forever.
3. Read the IR/analog sensor through the ADC driver when applicable.
4. Apply calibrated decision logic to classify the slot or proximity state.
5. Update the seven-segment display and activate the buzzer when the selected condition requires it.
6. Repeat at a controlled rate so display refresh and sensor sampling remain stable.

## Important distinction
An ADC result is a digital representation of the input voltage, not a distance by itself. For example, `512` is a threshold in the 10-bit ADC range (0–1023) only when using the ATmega2560's 10-bit ADC configuration. Whether values below or above the threshold mean “occupied” depends on the sensor output and wiring.
