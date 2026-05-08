# Telegram Bot Setup Guide

This guide explains how to create a Telegram bot and get the required values for the Wazuh to Telegram integration.

You need two values:

```python
TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"
CHAT_ID = "YOUR_TELEGRAM_CHAT_ID"
```

## 1. Create a Telegram Bot

1. Open Telegram.
2. Search for `@BotFather`.
3. Start a chat with BotFather.
4. Send the command:

```text
/newbot
```

5. Enter a display name for your bot.

Example:

```text
Wazuh Alerts Bot
```

6. Enter a username for your bot.

The username must end with `bot`.

Example:

```text
wazuh_alerts_example_bot
```

7. BotFather will generate a bot token.

It will look similar to this:

```text
1234567890:AAExampleTokenDoNotShareThisValue
```

Save this value. This is your Telegram bot token.

## 2. Get Your Chat ID

1. Open Telegram.
2. Search for `@userinfobot`.
3. Start the bot.
4. It will show your Telegram user ID.

Example:

```text
123456789
```

This value is your `CHAT_ID`.

## 3. Start Your Bot

Before Wazuh can send messages to your Telegram bot, you must start the bot manually.

1. Open your newly created bot in Telegram.
2. Press `Start`.
3. Send any test message to the bot.

Example:

```text
test
```

## 4. Add Telegram Values to the Script

Open the Wazuh integration script on your Wazuh Manager:

```bash
sudo nano /var/ossec/integrations/custom-telegram
```

Find these lines:

```python
TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"
CHAT_ID = "YOUR_TELEGRAM_CHAT_ID"
```

Replace them with your real values:

```python
TOKEN = "1234567890:AAExampleTokenDoNotShareThisValue"
CHAT_ID = "123456789"
```

Save the file.

## 5. Test Telegram API Manually

You can test whether your bot token and chat ID work before testing Wazuh.

Run this command:

```bash
curl -s -X POST "https://api.telegram.org/botYOUR_TELEGRAM_BOT_TOKEN/sendMessage" \
  -d chat_id="YOUR_TELEGRAM_CHAT_ID" \
  -d text="Test message from Wazuh server"
```

Replace:

```text
YOUR_TELEGRAM_BOT_TOKEN
YOUR_TELEGRAM_CHAT_ID
```

with your real values.

If everything is correct, you should receive a Telegram message.

## 6. Security Notes

Never upload your real Telegram bot token or chat ID to GitHub.

Do not commit files that contain real credentials.

Use placeholders in public repositories:

```python
TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"
CHAT_ID = "YOUR_TELEGRAM_CHAT_ID"
```

Use real values only on your Wazuh Manager server.

## 7. Troubleshooting

### Bot does not send messages

Check that:

- you pressed `Start` in the bot chat
- the bot token is correct
- the chat ID is correct
- the server has internet access
- Telegram API is reachable from the server

### Wrong chat ID

If the chat ID is wrong, Telegram will return an error similar to:

```json
{"ok":false,"error_code":400,"description":"Bad Request: chat not found"}
```

### Invalid bot token

If the token is wrong, Telegram will return an error similar to:

```json
{"ok":false,"error_code":404,"description":"Not Found"}
```

## Final Check

After completing Telegram setup, continue with the main Wazuh integration setup from `README.md`.
