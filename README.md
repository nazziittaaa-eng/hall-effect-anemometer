# Hall Effect Anemometer

A 3D-printed four-cup anemometer that measures wind speed using a digital
Hall effect sensor (KY-003) and an Arduino Uno R4 WiFi. Developed for the
Laboratory of Sensors course (Prof. Alexandro Catini).



## How it works

Wind drives four cups spaced 90° apart. Two neodymium magnets (180° apart)
on the rotating assembly pass 3 mm from the Hall sensor. Each pass pulls the
open-collector output from HIGH (5 V, via 10 kΩ pull-up) to LOW, generating
a pulse that the Arduino counts with a hardware interrupt.

Pulses → revolutions → rps → tip speed (2πr × rps) → wind speed (× CAL_FACTOR)

## Hardware

- Arduino Uno R4 WiFi
- KY-003 digital Hall effect sensor
- 2× neodymium magnets
- 3D-printed parts: shaft, top cover, separator, cups, balls,
  inner bearings, direction indicator, main rotor
- Ball bearings for low friction

## Mechanical design

All parts were modelled in SolidWorks and 3D printed. Source files are in
`cad/solidworks/` and printable STLs in `cad/stl/`.

## Firmware

`firmware/anemometer.ino` features:
- Interrupt-driven pulse counting on pin 2
- 3 ms debounce
- 1 s sampling window
- Zero-timeout (reports 0 after 3 s with no pulses)
- Serial output: pulses, rpm, tip speed, wind speed (m/s and km/h)

## Results

| Test | Result |
|---|---|
| Light sensitivity | None (same readings with and without light) |
| Resolution | 0.346 m/s tip speed per pulse |
| Noise (std dev) | ±0.251 m/s |
| Calibration fit | y = 0.864x − 1.23, R² = 0.969 |
| Tested range | ~8–13 km/h |

Calibrated against a Viterbo weather station (Weather Underground).

## Limitations and future work

- CAL_FACTOR (2.5) is a placeholder, not derived from rotor geometry
- Only three calibration points over a narrow range
- Mounted at 2 m instead of the 10 m standard

## Full report

See (docs/hall_effect_anemometer_9.pdf).

## Author

Nazanin Taherpoursomeh

## License

MIT
