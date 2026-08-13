# zmk-skeletyl

Minimal ZMK shield/config repo for the [BastardKB Skeletyl](https://github.com/Bastardkb/Skeletyl/).

It includes:

- shield definitions in `boards/shields/skeletyl/`
- the dongle OLED add-on shield in `boards/shields/dongle_oled/`
- user config and keymap in `config/`
- build matrix in `build.yaml`
- keymap-drawer assets in `keymap-drawer/`

Current build targets cover:

- `skeletyl_left`
- `skeletyl_right`
- `skeletyl_dongle`
- `dongle_oled`
- `settings_reset`

Artifacts produced by the build matrix:

- `skeletyl_dongle` for `nice_nano/nrf52840/zmk`
- `skeletyl_dongle prospector_adapter` for `xiao_ble//zmk`
- `skeletyl_dongle` for `xiao_ble//zmk`
- `skeletyl_dongle_oled_nice_nano` artifact for `nice_nano/nrf52840/zmk`
- `skeletyl_dongle_oled_xiao_ble` artifact for `xiao_ble//zmk`
- `settings_reset` for `xiao_ble//zmk`
- `settings_reset` for `nice_nano/nrf52840/zmk`
- `skeletyl_left` for `nice_nano/nrf52840/zmk`
- `skeletyl_right` for `nice_nano/nrf52840/zmk`
- `skeletyl_right_usb_logging` artifact for `nice_nano/nrf52840/zmk`

## Dongle display

The dongle can drive an I2C OLED using
[englmaxi/zmk-dongle-display](https://github.com/englmaxi/zmk-dongle-display),
which replaces ZMK's built-in status screen with a screen showing the active
layer, modifiers, HID indicators, output status, peripheral battery levels, a
bongo cat and an optional WPM meter.

The module is pulled in via `config/west.yml`. It only supplies the screen, not
the panel wiring, so this repo adds a small `dongle_oled` shield that declares
the display itself:

- `boards/shields/dongle_oled/dongle_oled.dtsi` — the panel node, defaulting to
  a 1.3" 128x64 SH1106 at address `0x3c`
- `boards/shields/dongle_oled/boards/nice_nano.overlay` — wires it to
  `pro_micro_i2c`: D2 = SDA (P0.17), D3 = SCL (P0.20)
- `boards/shields/dongle_oled/boards/xiao_ble.overlay` — wires it to `xiao_i2c`:
  D4 = SDA (P0.04), D5 = SCL (P0.05)
- `boards/shields/dongle_oled/dongle_oled.conf` — idle timeout plus commented
  widget options

Build it by combining all three shields, as the matrix entries do:

```yaml
- board: nice_nano/nrf52840/zmk
  shield: skeletyl_dongle dongle_oled dongle_display
```

Keeping the OLED in its own shield leaves the plain `skeletyl_dongle` and the
`skeletyl_dongle prospector_adapter` builds untouched — only the targets that
list `dongle_oled` get an OLED.

For a different panel, edit `dongle_oled.dtsi`: a 0.96" SSD1306 needs
`compatible = "solomon,ssd1306fb"` and `segment-offset = <0>`, and a 0.91"
128x32 needs `height = <32>`, `multiplex-ratio = <31>`, `com-sequential`, plus
the 128x32 config block in `dongle_oled.conf`.

Main files:

- `config/skeletyl.keymap`
- `config/skeletyl.conf`
- `config/skeletyl.json`

This repo is intended to be used as a ZMK config repository for local or CI builds.
