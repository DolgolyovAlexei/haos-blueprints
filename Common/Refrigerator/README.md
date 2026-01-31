# Refrigerator Express Mode Control Blueprint

This blueprint monitors refrigerator temperature and automatically enables express/turbo cooling mode when the temperature drifts too far from target.

## How It Works

- Monitors the temperature sensor and compares to target temperature
- If difference exceeds threshold (and door is closed), enables express mode
- Sends notification when express mode is activated
- Automatically disables express mode when temperature normalizes

## Requirements

- Door sensor (binary_sensor) to detect if door is open
- Temperature sensor reporting current fridge temperature
- Climate entity with target temperature attribute
- Switch entity to control express/turbo mode

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
