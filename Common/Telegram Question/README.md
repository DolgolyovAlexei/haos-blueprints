# Telegram Keyboard Action Blueprint

This blueprint creates interactive Telegram messages with inline keyboard buttons. When a button is pressed, the corresponding callback action runs.

## How It Works

1. Manual trigger (service call) → Sends message with keyboard to chat(s)
2. Button press → Triggers `telegram_callback` event
3. Blueprint matches callback data to `keyboard_id`
4. Executes the corresponding button's callback action
5. Optionally sends answer and/or hides keyboard/message

## Chat ID Resolution

Chat IDs can be provided in two ways:

- Directly as text list (`chat_ids` input)
- From notify entities with friendly names like `"Alex (123456789)"` - the number in parentheses is extracted as the chat ID

## Multiple Telegram Bots

If you have multiple Telegram bots configured in Home Assistant, you must specify the `config_entry_id` to identify which bot to use.

Find it in: Settings → Devices & Services → Telegram Bot → your bot → URL

## Callback Data Format

Each button sends callback data: `/<keyboard_id>_<button_index>`

Example: `/my_keyboard_0` for first button of keyboard `"my_keyboard"`

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
