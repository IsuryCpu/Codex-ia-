# Raspberry Pi Pico W Keypad-to-LED Controller

This project targets the **Raspberry Pi Pico W (RP2040)** and maps a **4x4 membrane keypad** to **12 LEDs**.
Each key press turns on/off specific LEDs according to fixed logic in the firmware.

> Note: The provided source uses Arduino-style APIs (`setup()`, `loop()`, `pinMode()`, `digitalWrite()`) and the `Keypad.h` library. The logic was preserved exactly and moved into a clean Pico-oriented repository layout.

## Features

- 4x4 keypad scanning (16 keys)
- 12 individually addressable LEDs
- Group LED control for keys `9`, `0`, `*`, and `#`
- Wiring and architecture documentation for Wokwi + real hardware

## Repository Structure

- `src/main.cpp` — original firmware logic (preserved)
- `include/` — reserved for headers
- `docs/wiring.md` — full connection and GPIO mapping
- `docs/architecture.md` — firmware structure and behavior
- `CMakeLists.txt` — Pico SDK project entry point

## Hardware Components

From the provided `diagram.json`:

- 1x Raspberry Pi Pico / Pico W compatible board
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8 blue LEDs (numeric mapping 1..8)
  - 4 red LEDs (A..D mapping)
- 12x 220Ω resistors (LED current limiting)
- 4x 1kΩ resistors (keypad row pull-ups to 3V3)
- Jump wires / breadboard equivalent

## Pin Overview

See `docs/wiring.md` for the complete table.

## Build and Flash (Pico SDK)

1. Install toolchain and SDK.
2. Set `PICO_SDK_PATH`.
3. Configure and build:

```bash
mkdir -p build
cd build
cmake ..
make -j
```

4. Hold **BOOTSEL**, plug Pico W over USB, copy generated `.uf2` to the mounted drive.

## Wokwi Simulation

1. Create a new Pico project in Wokwi.
2. Paste your provided `diagram.json` into the Wokwi diagram editor.
3. Use `src/main.cpp` logic in the simulation source file.
4. Start simulation and press keypad keys.

## Real Hardware Notes

- Keep LED polarity correct: GPIO -> resistor -> LED anode, LED cathode -> GND.
- Ensure all grounds are common.
- The keypad row pull-up network in the diagram ties rows to 3V3 through 1kΩ resistors.

## Wi-Fi Note

This firmware does **not** use Wi-Fi despite targeting Pico W. No credentials are required.
If Wi-Fi is added later, keep SSID/password in a separate untracked config file.
