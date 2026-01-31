# Telegram Commands Blueprint

This blueprint responds to Telegram bot commands (e.g., /start, /help, /status). Each command can trigger a different callback action and send an optional reply.

## How It Works

1. User sends a command to the Telegram bot (e.g., `/lights_on`)
2. Home Assistant receives `telegram_command` event
3. Blueprint matches command to the configured list
4. Executes the corresponding callback action
5. Optionally sends a reply message

## Command Format

Commands should start with "/" (e.g., `/status`, `/lights_on`, `/arm_alarm`). The bot must be configured to receive these commands.

## Example Configuration

| Commands | Answers |
|----------|---------|
| `/status` | "Status checked" |
| `/lights_on` | "Lights turned on" |
| `/lights_off` | "Lights turned off" |
| `/arm` | "Alarm armed" |

Each command has its own callback action that executes when received.

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
