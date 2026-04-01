# zmk-skeletyl

Minimal ZMK shield/config repo for the [BastardKB Skeletyl](https://github.com/Bastardkb/Skeletyl/).

It includes:

- shield definitions in `boards/shields/skeletyl/`
- user config and keymap in `config/`
- build matrix in `build.yaml`
- keymap-drawer assets in `keymap-drawer/`

Current build targets cover:

- `skeletyl_left`
- `skeletyl_right`
- `skeletyl_dongle`
- `settings_reset`

Artifacts produced by the build matrix:

- `skeletyl_dongle` for `nice_nano/nrf52840/zmk`
- `skeletyl_dongle prospector_adapter` for `xiao_ble//zmk`
- `skeletyl_dongle` for `xiao_ble//zmk`
- `settings_reset` for `xiao_ble//zmk`
- `settings_reset` for `nice_nano/nrf52840/zmk`
- `skeletyl_left` for `nice_nano/nrf52840/zmk`
- `skeletyl_right` for `nice_nano/nrf52840/zmk`
- `skeletyl_right_usb_logging` artifact for `nice_nano/nrf52840/zmk`

Main files:

- `config/skeletyl.keymap`
- `config/skeletyl.conf`
- `config/skeletyl.json`

This repo is intended to be used as a ZMK config repository for local or CI builds.
