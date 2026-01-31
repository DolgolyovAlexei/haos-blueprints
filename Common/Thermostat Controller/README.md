# Thermostat Controller Blueprint

This blueprint controls a thermostat/climate entity based on schedules, presence, and various conditions.

## Features

- Schedule-based heating control (using HA schedule helper)
- Working and standby temperature modes
- Optional input_number overrides for temperatures
- External temperature sensor support
- Window/door sensor integration (disable when open)
- Force heating override
- Minimum on-time to prevent rapid cycling
- Configurable behavior when disabled (off vs standby)
- Debug notifications for troubleshooting

## Temperature Priority

1. Windows open → Turn off (or standby based on setting)
2. Force heating ON → Working temperature
3. Schedule active → Working temperature
4. Schedule inactive → Standby temperature (or off)

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
