# MQTT Generic Control Blueprint

A flexible blueprint that triggers custom actions based on MQTT messages. Supports up to 8 different action IDs, each with its own callback.

## Features

- Listen to up to 4 MQTT topics simultaneously
- Map up to 8 action IDs to custom callback actions
- Works with any Zigbee2MQTT device that sends action payloads
- Fully customizable actions for each trigger

## How It Works

1. Listens for MQTT messages on configured topics
2. Extracts the `action` field from the JSON payload
3. Matches action against configured action IDs
4. Executes the corresponding callback action sequence

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
