# Home Presence Controller Blueprint

This blueprint determines home presence/occupancy based on multiple signals:

- Activity sensors (presence assumed if any sensor changed state recently)
- Person/presence entities (tracking if someone is home)
- Wi-Fi connection (devices connected to home network)
- Bluetooth/BLE devices (device trackers reporting home/away)

The result is stored in an input_boolean helper that other automations can use to determine if someone is likely home.

## Features

- Multiple signal sources for robust presence detection
- Activity sensors with configurable threshold (door, motion, etc.)
- Guest mode override for manual presence control
- Bluetooth device tracker support
- Debug notifications for troubleshooting
- Graceful handling of unavailable sensors
- Automatic evaluation on Home Assistant startup

## Signal Priority

1. Guest mode (forces presence ON when enabled)
2. Stable signals (person entities, Wi-Fi, Bluetooth)
3. Activity sensors (temporary presence based on recent state changes)

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
