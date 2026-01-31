# MQTT Button Control Blueprint

Controls lights and switches using Zigbee2MQTT button devices with multiple action mappings.

## Features

- Map multiple action IDs to different lights/switches
- Supports light, switch, and input_boolean entities
- Visual feedback via blink indication when pressing already-active light
- Tracks last interacted entity in an input_text helper
- Supports multiple MQTT topics (multiple buttons)

## How It Works

1. Receives MQTT messages with action IDs from Zigbee buttons
2. Maps action ID to corresponding entity by index position
3. Toggles the matched entity (light/switch/input_boolean)
4. Optionally blinks light if it's already on (idle timeout feature)

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
