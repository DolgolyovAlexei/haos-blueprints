# Motion Light Automation Blueprint

This blueprint creates a smart motion-activated light control system. It handles motion detection, luminance-based triggering, and manual override detection to provide intelligent lighting automation.

## Features

- Multiple motion sensor support (triggers on ANY sensor)
- Condition switches (ALL must be ON for automation to work)
- Multiple lights and/or switches control
- Light groups and area-based targeting
- Configurable timeout delay before turning off
- Minimum on duration (prevents rapid on/off cycling)
- Motion sensor debounce (filter false triggers)
- Smooth light transitions with configurable duration
- Luminance sensor support (only trigger in dark conditions)
- Time-based conditions (only active during specified hours)
- Day/Night mode (different light settings based on time)
- Scene support (activate scenes instead of light parameters)
- Dim before off (visual warning before turning off)
- Manual override detection (stops automation if user changes light)
- Brightness threshold (only trigger if light is dim)
- Custom light parameters (brightness, color, etc.)
- Callback actions for enable/disable/manual events
- Debug notifications for troubleshooting

## State Machine

The automation tracks these states via persistent storage:

| State | Value | Description |
|-------|-------|-------------|
| NONE | 0 | Idle, waiting for motion |
| ENABLING | 2 | Light turn-on command sent, waiting for state change |
| ENABLED | 1 | Light is ON and controlled by automation |
| MANUAL | 3 | User took control, automation paused until light turns off |

## Behavior Notes

- Will NOT turn on light if it's already ON (prevents hijacking user control)
- If user changes light while automation is active, enters MANUAL mode
- MANUAL mode exits when light is turned OFF (by any means)
- Timeout delay only applies when turning OFF (motion cleared)
- Time conditions support overnight windows (e.g., 22:00 to 06:00)
- Day/Night mode uses separate time window from time conditions

## Requirements

- At least one motion sensor
- `input_text` entity for persistent state storage
- Target light(s), switch(es), group, or area to control

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
