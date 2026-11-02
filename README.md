# Yale Access Bluetooth for Home Assistant, test build

[![Validate](https://github.com/Yale-Libs/ha-yalexs-ble/actions/workflows/validate.yml/badge.svg?branch=main)](https://github.com/Yale-Libs/ha-yalexs-ble/actions/workflows/validate.yml)
[![HACS Custom](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://hacs.xyz/docs/faq/custom_repositories)

A copy of Home Assistant's built-in `yalexs_ble` integration, taken from core 2026.10.4, that installs through HACS and replaces the built-in one while it is installed. It exists so the changes the [yalexs-ble activity log work](https://github.com/Yale-Libs/yalexs-ble/issues/421) asks of Home Assistant can be shown and tried end to end before they go to core.

This is a test build. It keeps the core domain `yalexs_ble`, so your existing Yale Access Bluetooth entries keep working, and the built-in integration comes back when you uninstall it.

## Installation

1. In HACS, open the menu, choose Custom repositories, and add `https://github.com/Yale-Libs/ha-yalexs-ble` as an Integration.
2. Install Yale Access Bluetooth and restart Home Assistant.
3. Existing Yale Access Bluetooth entries pick up the copy on restart; new ones are added the usual way under Settings, Devices & services.

## What changes here

- Moves to the yalexs-ble release that carries the activity log decoder (`parse_log_event_packet`, `Brand`, `register_log_record_callback`).
- Stores the `brand` the August or Yale Home integration passes in its discovery and hands it to `PushLock`.
- Reshapes the keypad attribution and lock operation event work (home-assistant/core#185596, home-assistant/core#151436) onto decoded records, dispatching on record class for both brands.

## Updating from core

`script/vendor <path to a home-assistant checkout> <tag>` checks out the tag there, builds the English translations with core's script, copies the integration in and sets the manifest's `version` to the tag. Commit the result before making changes on top, so the diff against core stays readable.

## License

The vendored code is Home Assistant's, under the Apache License 2.0 (see LICENSE).
