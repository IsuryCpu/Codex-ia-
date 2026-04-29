# Wiring and GPIO Mapping (Raspberry Pi Pico W)

This mapping is derived from the provided Wokwi `diagram.json` and source arrays.

## Keypad Connections

| Keypad Pin | Pico W GPIO | Firmware Array |
|---|---:|---|
| C1 | GP19 | `colPins[0]` |
| C2 | GP18 | `colPins[1]` |
| C3 | GP17 | `colPins[2]` |
| C4 | GP16 | `colPins[3]` |
| R1 | GP26 | `rowPins[0]` |
| R2 | GP22 | `rowPins[1]` |
| R3 | GP21 | `rowPins[2]` |
| R4 | GP20 | `rowPins[3]` |

### Pull-up Network

Rows R1..R4 are also connected through four 1kΩ resistors that are bussed together to **3V3**.
This creates external pull-ups for row lines.

## LED Connections

All LED cathodes connect to GND. Each anode connects to a GPIO through a 220Ω resistor.

| LED Label | Pico W GPIO | `ledPins[]` Index | LED Color (diagram) |
|---|---:|---:|---|
| 1 | GP11 | 0 | Blue |
| 2 | GP10 | 1 | Blue |
| 3 | GP9  | 2 | Blue |
| 4 | GP8  | 3 | Blue |
| 5 | GP7  | 4 | Blue |
| 6 | GP6  | 5 | Blue |
| 7 | GP5  | 6 | Blue |
| 8 | GP4  | 7 | Blue |
| A | GP3  | 8 | Red |
| B | GP2  | 9 | Red |
| C | GP28 | 10 | Red |
| D | GP27 | 11 | Red |

## Serial Monitor (Wokwi)

- GP0 -> Serial RX
- GP1 -> Serial TX

(Used by the simulator wiring; firmware currently does not print serial output.)

## Behavior Mapping Summary

- `1..8`: turn on matching blue LED
- `9`: turn on blue LEDs 1..8
- `0`: turn off blue LEDs 1..8
- `A..D`: turn on matching red LED
- `*`: turn on red LEDs A..D
- `#`: turn off red LEDs A..D
