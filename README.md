# Home Assistant Automation Blueprints

A collection of automation blueprints for Home Assistant.

## Blueprints

### Common

| Blueprint | Description |
|-----------|-------------|
| Alarm Notification | Triggers notifications when binary sensors activate |
| Climate Device Controller | Controls climate devices based on window/door sensors |
| Day Scene Controller | Activates scenes based on time-of-day state |
| Home Presence | Determines home presence from multiple signals |
| Immich Album Watcher | Sends notifications when photos are added to Immich albums |
| Motion Light | Smart motion sensor light control |
| Refrigerator | Monitors refrigerator temperature and triggers express mode |
| Telegram Commands | Responds to Telegram bot commands with callback actions |
| Telegram Question | Sends Telegram messages with inline keyboard buttons |
| Thermostat Controller | Controls thermostat based on schedules, presence, and window sensors |
| Time Of Day Controller | Sets input_select based on time-of-day thresholds |
| Track Abnormal Plug Activity | Monitors power sensors for sustained overconsumption |
| Washing Machine | Sends notifications for washing machine events |

### Zigbee (MQTT)

| Blueprint | Description |
|-----------|-------------|
| Media Knob Control | Control media player using rotary knob via MQTT |
| MQTT Button Control | Control devices with multiple button actions |
| MQTT Generic Control | Generic MQTT trigger with custom action callbacks |
| MQTT Light Control | Extended light control using MQTT devices |
| MQTT Light Selector | Cycle through lights using MQTT button events |

## Installation

1. Copy the desired `.yaml` file to your Home Assistant `config/blueprints/automation/` directory
2. Reload automations or restart Home Assistant
3. Create a new automation using the blueprint

## Author

Created by Alexei Dolgolyov (`dolgolyov.alexei@gmail.com`)

## Support

If you encounter any issues or have questions, please open an issue in this repository.
