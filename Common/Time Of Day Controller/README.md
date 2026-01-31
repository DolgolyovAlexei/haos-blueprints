# Time of Day State Machine Blueprint

This blueprint automatically updates an input_select based on time-of-day thresholds. Useful for managing different modes throughout the day (morning, afternoon, evening, night, etc.).

## How It Works

- Define states (e.g., "Morning", "Afternoon", "Evening", "Night")
- Define corresponding time thresholds for each state
- The blueprint sets the input_select to the appropriate state based on current time

## Index Mapping

States and times are mapped by index position:

| Index | State | Time |
|-------|-------|------|
| 0 | states[0] | times[0] |
| 1 | states[1] | times[1] |
| 2 | states[2] | times[2] |
| etc. | etc. | etc. |

## Supported Time Formats

- `input_datetime` entities (time-only: HH:MM:SS)
- Sensor entities reporting time strings (e.g., `sun.sun` next_rising attribute)

## Example Configuration

- **States**: `["Night", "Morning", "Afternoon", "Evening"]`
- **Times**: `[00:00, 06:00, 12:00, 18:00]`
- At 14:30, the state would be "Afternoon" (last threshold passed)

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
