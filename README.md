# Raspberry Pi Pico W + SSD1306 OLED Demo

MicroPython project for Raspberry Pi Pico W that:
- initializes an SSD1306 OLED over I2C,
- draws a Raspberry Pi logo,
- prints static text,
- runs a 1-second timer animation loop.

Core firmware behavior is preserved from the provided source.

## Repository Structure

```text
.
├── src/
│   └── main.py
├── lib/
├── docs/
│   ├── architecture.md
│   └── wiring.md
├── diagram.json
└── README.md
```

## Features

- I2C bus scan and display presence check.
- OLED init at 128x64.
- Monochrome framebuffer logo rendering.
- Text output (`Raspberry Pi`, `Pico`).
- Infinite timer update (`N sec`) every 1000 ms.

## Hardware

- Raspberry Pi Pico W (RP2040)
- SSD1306 OLED (I2C, 128x64)
- Breadboard + jumper wires

See full connection details in [`docs/wiring.md`](docs/wiring.md).

## Software Requirements

- MicroPython firmware for Pico/Pico W
- `ssd1306.py` driver available on-device (commonly from MicroPython examples or bundle)
- Thonny, `mpremote`, or similar upload tool

## Run on Real Hardware

1. Flash MicroPython UF2 to Pico W.
2. Wire components as documented in `docs/wiring.md`.
3. Copy `src/main.py` to device as `main.py`.
4. Ensure `ssd1306.py` exists on the board filesystem.
5. Reset the board.

Expected serial output includes detected I2C address and config; display shows logo/text and timer.

## Run in Wokwi

1. Create a new **Raspberry Pi Pico** MicroPython project in Wokwi.
2. Replace `diagram.json` with this repository's `diagram.json`.
3. Paste `src/main.py` into Wokwi `main.py`.
4. Start simulation.

## Wi-Fi Notes

This project does **not** currently use Wi-Fi. If Wi-Fi is added later:
- keep credentials in a separate local file (for example `secrets.py`) not committed to git,
- import at runtime, and
- provide a redacted template (for example `secrets.example.py`).

## Behavior Preservation

No algorithmic/logic changes were introduced to the provided firmware; only structure and documentation were added.
