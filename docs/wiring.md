# Wiring (Raspberry Pi Pico W + SSD1306 I2C)

## Components (from `diagram.json`)

1. `wokwi-pi-pico` (used as Pico board in diagram; target remains Pico W)
2. `board-ssd1306` (I2C OLED display)
3. `wokwi-breadboard-mini`

## GPIO / Signal Mapping

Firmware uses:
- `I2C(1, scl=Pin(27), sda=Pin(26), freq=200000)`

| Function | OLED Pin | Pico W GPIO | Physical Pico Pin (signal pin name) | Notes |
|---|---|---:|---|---|
| Ground | GND | — | GND (`GND.8` in diagram) | Common ground |
| Power | VCC | — | 3.3V rail (`3V3_EN` wired in diagram) | SSD1306 is typically 3.3V-safe |
| I2C Clock | SCL | GP27 | `GP27` | Used as SCL in code |
| I2C Data | SDA | GP26 | `GP26` | Used as SDA in code |

## Diagram Interpretation Notes

- The provided Wokwi file includes both generic pin references (`pico:8`, `pico:9`) and explicit net connections (`pico:GP26`, `pico:GP27`) to the same breadboard rows.
- For firmware correctness, the authoritative mapping is GP27=SCL and GP26=SDA, matching `main.py`.
- The power net in the diagram is tied via `3V3_EN`; on real hardware, connect OLED VCC to a valid 3V3 supply pin.

## Real-World Wiring Checklist

- [ ] Pico GND ↔ OLED GND
- [ ] Pico 3V3 ↔ OLED VCC
- [ ] Pico GP27 ↔ OLED SCL
- [ ] Pico GP26 ↔ OLED SDA
- [ ] Keep wires short for cleaner I2C signal integrity
