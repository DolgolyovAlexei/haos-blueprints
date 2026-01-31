# MQTT Light Selector Blueprint

Cycles through a list of lights using MQTT button events (up/down/remind). The selected light flashes to provide visual feedback, then returns to its original state. Selection is persisted in an input_text helper.

## Features

- Navigate lights with up/down actions
- Remind action flashes the currently selected light
- Visual feedback via configurable flash pattern
- Persists selection in an input_text helper
- Optional state persistence across restarts (JSON storage)
- Optional "remind on idle" - up/down acts as remind if idle too long

## How It Works

1. Press up/down to cycle through the light list
2. Selected light flashes N times to confirm selection
3. Light returns to its original on/off state after flashing

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
