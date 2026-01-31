# Day Scene Controller Blueprint

This blueprint automatically activates scenes based on time-of-day state and a control switch. It bridges the Time of Day State Machine with scene activation.

## How It Works

- Monitors a time-of-day input_select (from Time of Day State Machine)
- When control switch is ON: activates the scene matching current time slot
- When control switch is OFF: activates the default scene
- Optionally applies default scene as transition before switching scenes

## Index Mapping

Scenes are mapped to time-of-day states by index:

| Time State Index | Scene |
|-----------------|-------|
| option[0] | scenes[0] |
| option[1] | scenes[1] |
| option[2] | scenes[2] |
| etc. | etc. |

## Example Configuration

- **Time of Day options**: `["Night", "Morning", "Afternoon", "Evening"]`
- **Scenes**: `[scene.night, scene.morning, scene.afternoon, scene.evening]`
- When time is "Morning" and control is ON → `scene.morning` activates

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
