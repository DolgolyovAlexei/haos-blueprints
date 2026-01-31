# MQTT Light Control Blueprint

Provides extended light control functionality via MQTT devices (typically Zigbee controllers through zigbee2mqtt).

## Features

- Control multiple lights via MQTT topics
- Sequential and "all at once" turn on/off actions
- Brightness control (increment, hold, list-based, min/max)
- Color temperature control (increment, hold, list-based)
- RGB/Hue control (increment, hold, list-based)
- Preset list support (JSON format) for quick scene switching
- Scene activation support (up to 4 scenes)
- Light group and area targeting
- Configurable transition duration for smooth changes
- Alternative light support (control secondary lights when primary are off)
- Persistent state storage via input_text entity
- Custom action callbacks for extending functionality

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
