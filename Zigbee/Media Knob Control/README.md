# MQTT Knob Media Controller Blueprint

Controls a media player using an MQTT-connected rotary encoder/knob.

## Features

- Play/Pause toggle (button press)
- Volume up/down (rotation)
- Mute toggle (optional)
- Next/Previous track (optional)

## Volume Step Behavior

- If your device sends `action_step_size` in the MQTT payload, it will be used
- Otherwise, the configured default step size is applied

## Configuration

Action IDs can be customized to match your specific MQTT device.

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
