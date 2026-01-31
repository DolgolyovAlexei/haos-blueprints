# Power Overconsumption Monitor Blueprint

This blueprint monitors power sensors for sustained overconsumption that might indicate device malfunction, overload, or safety concerns.

## How It Works

- Triggers when power EXCEEDS a maximum threshold
- Requires power to stay high for a configurable duration (filters startup spikes)
- Optionally ignores readings below an idle threshold (device "off")
- Can automatically turn off the switch for safety

## Use Cases

- Space heater drawing more than rated wattage (fire risk)
- Motor consuming excessive power (mechanical binding/failure)
- Appliance exceeding safe operating limits
- Extension cord/circuit overload protection

## Naming Convention

The blueprint assumes sensors follow the pattern: `sensor.<name>_power` and the corresponding switch is: `switch.<name>`

**Example**: `sensor.coffee_maker_power` → `switch.coffee_maker`

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
