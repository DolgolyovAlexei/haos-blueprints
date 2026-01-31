# Climate Device Controller Blueprint

This blueprint controls climate devices (heaters, AC, humidifiers, etc.) based on environmental sensors, window/door states, and schedules.

## Supported Device Types

Supports any controllable device type through custom actions:

- Switches (traditional on/off control)
- Climate entities (HVAC, air conditioners)
- Smart remotes (IR/RF commands for AC units)
- Scripts and scenes
- Any other controllable entity

## Features

- Automatic on/off based on target value (temperature, humidity, etc.)
- Hysteresis window to prevent rapid on/off cycling
- Force ON override (manual override to keep device always on)
- Window/door sensor integration (turns off when open for efficiency)
- Decay duration (waits before reacting to door/window changes)
- Emergency threshold (forces device ON below critical value)
- Schedule support (only runs during scheduled times)
- Power monitoring (detects device malfunction)
- House-wide and room-specific window/door sensors

## Control Logic (Priority Order)

1. If Force ON switch is ON → FORCE ON (manual override)
2. If value is below emergency threshold → FORCE ON (safety override)
3. If control switch is OFF → FORCE OFF
4. If environment not sealed OR schedule not active → OFF
5. If value at or above target → OFF (target reached)
6. If value below turn-on threshold (target - hysteresis) → ON
7. Otherwise → maintain current state (in hysteresis zone)

## Hysteresis Example

Prevents rapid cycling:

- Target humidity: 30%, Hysteresis window: 5%
- Device turns OFF when humidity reaches 30%
- Device turns ON when humidity drops to 25% (30% - 5%)
- Between 25-30%: device maintains its current state

## Window/Door Logic

- "House closed" = ALL house windows are closed (for decay duration)
- "Room closed" = ALL room windows AND doors are closed (for decay duration)
- Device can run if EITHER house OR room is fully closed

## Power Monitoring

If device is ON but power consumption is below threshold for decay duration, it's flagged as problematic (possible malfunction).

## Requirements

- Device entity to monitor state (switch, climate, etc.)
- Custom actions for turning device on/off
- Control switch (master enable/disable)
- Environment sensor(s) for current value
- Target value entity (input_number)

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
