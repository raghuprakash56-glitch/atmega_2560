# Ultrasonic Driver Notes

An HC-SR04-style sensor is triggered by a short HIGH pulse on TRIG. The sensor then produces an ECHO pulse whose width is related to round-trip acoustic travel time.

Approximate distance in centimetres:

`distance_cm ≈ echo_time_us / 58`

Implementation considerations:
- Set TRIG as output and ECHO as input.
- Generate the trigger pulse according to the sensor specification.
- Wait for ECHO to rise and fall with timeout protection.
- Return an error/timeout status instead of hanging if no echo arrives.
- Test against a ruler at several distances.
- Avoid taking measurements so frequently that echoes from a prior measurement interfere.

The formula is approximate and depends on temperature and the sensor module.
