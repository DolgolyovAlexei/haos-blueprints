# Washing Machine / Dryer Notifications Blueprint

This blueprint monitors washing machine or dryer appliances and sends notifications for various events throughout the wash/dry cycle.

## Features

- Start notification with cycle duration, estimated end time, and mode details
- Completion notification (reminder to unload clothes) with energy report
- "Almost done" notification (configurable minutes before end)
- Pause/Resume notifications (detect when cycle is paused or resumed)
- Error message notifications
- Preparation mode notification (e.g., for dryer prep)
- Tub/drum cleaning reminder based on wash counter
- Power consumption monitoring with energy tracking per cycle
- Fully customizable notification messages (i18n support)
- Debug notifications for troubleshooting

## State Machine

The automation tracks the appliance through these states:

| State | Description |
|-------|-------------|
| IDLE | Waiting for cycle to start |
| RUNNING | Cycle in progress (start notification sent) |
| PAUSED | Cycle temporarily paused (pause notification sent) |
| FINISHING | Near completion (time-to-end notification sent) |
| COMPLETED | Cycle done (completion notification sent, state reset) |

## Persistent State Keys

| Key | Description |
|-----|-------------|
| `nass` | Notification About Start Sent |
| `nart` | Notification About Remaining Time Sent |
| `naps` | Notification About Preparation Sent |
| `napas` | Notification About Pause Sent |
| `wasp` | Was Paused flag |
| `cst` | Cycle Start Time (ISO timestamp) |
| `esmp` | Energy Samples accumulator (Wh) |
| `lst` | Last Sample Time (ISO timestamp) |

## Message Template Variables

All message templates support these placeholder variables (use single braces):

| Variable | Description |
|----------|-------------|
| `{appliance_name}` | Device name (e.g., "Washing Machine") |
| `{remaining}` | Remaining time as string (e.g., "01:30:00") |
| `{estimated_end}` | Estimated completion time (e.g., "14:30") |
| `{minutes}` | Remaining minutes as number (e.g., 90) |
| `{error}` | Error message text (only in error notification) |
| `{tub_count}` | Tub clean counter value (only in tub clean notification) |
| `{tub_threshold}` | Tub clean threshold (only in tub clean notification) |
| `{details}` | Startup details from sensors (only in start notification) |
| `{energy_kwh}` | Energy consumed in kWh (only in completion notification) |
| `{energy_cost}` | Estimated cost (only in completion notification) |

## Requirements

- Sensors for: remaining time, run state, error messages
- `input_text` entity for persistent state storage
- Notification service entity
- (Optional) Power sensor for energy tracking

## Note

Default messages are in Russian for LG ThinQ integration. Customize messages in the "Messages" section for your language.

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
