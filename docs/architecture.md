# Firmware Architecture

## Runtime Flow

`main()` executes in this order:

1. `init_i2c(scl_pin=27, sda_pin=26)`
   - Initializes `I2C(1)` at 200 kHz.
   - Scans for devices.
   - Exits if no device is found.
2. `SSD1306_I2C(128, 64, i2c_dev)`
   - Binds display driver to the detected bus.
3. `display_logo(oled)`
   - Builds a `FrameBuffer` from a 32x32 byte array and blits it to `(96,0)`.
4. `display_text(oled)`
   - Writes static label text.
5. `display_anima(oled)`
   - Enters infinite loop updating elapsed seconds every 1 second.

## Module Responsibilities

- `machine.Pin`, `machine.I2C`: RP2040 GPIO and I2C peripheral control.
- `ssd1306.SSD1306_I2C`: Display transport + drawing primitives.
- `framebuf`: Bitmap buffer abstraction for logo rendering.
- `utime`: Tick/timing functions for second counter update.
- `sys`: Early exit when no I2C OLED is detected.

## Files

- `src/main.py`: Main firmware logic (preserved behavior).
- `diagram.json`: Wokwi hardware topology.
- `docs/wiring.md`: Electrical mapping and assumptions.
- `docs/architecture.md`: Firmware design notes.

## Error Handling Behavior

- If no I2C address is found, firmware prints `No I2C Display Found` and exits.
- If found, prints first I2C address and I2C configuration object to serial console.

## Timing Behavior

- Timer display updates nominally once per second using `utime.sleep_ms(1000)`.
- Elapsed seconds computed from `utime.ticks_ms()` and `utime.ticks_diff()`.
