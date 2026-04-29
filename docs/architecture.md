# Firmware Architecture

## Overview

The firmware is implemented as a single translation unit (`src/main.cpp`) using Arduino-style structure:

- `setup()` for one-time initialization
- `loop()` for periodic keypad polling and LED updates

No dynamic allocation, interrupts, RTOS tasks, or networking are used.

## Static Configuration

- `LEDS = 12`
- `ROWS = 4`, `COLS = 4`
- `keys[4][4]` defines keypad character map
- `ledPins[12]` maps LED channels to Pico GPIOs
- `rowPins[4]`, `colPins[4]` map keypad matrix lines

## Initialization Flow (`setup`)

1. Iterate over all 12 LED pins.
2. Configure each as output.
3. Drive all LEDs LOW (off).

## Runtime Flow (`loop`)

1. Read one key event via `keypad.getKey()`.
2. If a key is pressed (`key != NO_KEY`), execute `switch` action.
3. Apply direct GPIO writes for individual or grouped LEDs.
4. Delay 10 ms.

## Key Action Groups

- **Individual blue LED ON**: `1`..`8`
- **Blue bank ON/OFF**: `9` (ON), `0` (OFF)
- **Individual red LED ON**: `A`..`D`
- **Red bank ON/OFF**: `*` (ON), `#` (OFF)

## Assumptions and Portability Note

The logic is preserved verbatim from provided code and depends on `Keypad.h` plus Arduino GPIO APIs.
For strict Pico SDK builds, an adapter layer or equivalent keypad scan implementation would be required, but that is intentionally out of scope to avoid behavior changes.
