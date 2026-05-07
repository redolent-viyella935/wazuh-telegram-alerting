# Wazuh to Telegram Integration 🚀

A simple custom integration for sending Wazuh alerts directly to Telegram.

This project was created to solve common issues with Wazuh custom integrations, including incorrect script arguments, missing JSON alert format, and wrong file permissions.

## Features

- Sends Wazuh alerts to Telegram in real time
- Uses Telegram Markdown formatting
- Shows agent name, alert level, rule ID, description, and log location
- Uses `sys.argv[1]` to read the Wazuh alert JSON file
- Includes basic error handling
- Uses safe placeholders instead of real Telegram tokens

## Project Structure

```text
.
├── README.md
└── custom-telegram.py
```

## Installation & Setup

### 1. Copy the integration script

Clone this repository or download `custom-telegram.py`.

Copy the script to the Wazuh integrations directory:

```bash
sudo cp custom-telegram.py /var/ossec/integrations/custom-telegram
```

The file inside `/var/ossec/integrations/` should not have the `.py` extension because the integration name in `ossec.conf` must match the script name.

### 2. Configure Telegram credentials

Edit the integration script:

```bash
sudo nano /var/ossec/integrations/custom-telegram
```

Replace the placeholders with your real Telegram bot token and chat ID:

```python
TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"
CHAT_ID = "YOUR_TELEGRAM_CHAT_ID"
```

Important: do not upload real tokens or chat IDs to GitHub.

### 3. Set correct permissions

This step is critical. Wazuh will not execute the script correctly if ownership or permissions are wrong.

Run:

```bash
sudo chown root:wazuh /var/ossec/integrations/custom-telegram
sudo chmod 750 /var/ossec/integrations/custom-telegram
```

### 4. Configure Wazuh Manager

Open the Wazuh configuration file:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Add the following block inside `<ossec_config>`:

```xml
<integration>
  <name>custom-telegram</name>
  <level>3</level>
  <alert_format>json</alert_format>
</integration>
```

The `<alert_format>json</alert_format>` option is required because the Python script reads the alert as a JSON file.

## Restart Wazuh Manager

Apply the changes by restarting Wazuh Manager:

```bash
sudo /var/ossec/bin/wazuh-control restart
```

## Troubleshooting

If Telegram notifications are not arriving, check the Wazuh logs:

```bash
sudo tail -f /var/ossec/logs/ossec.log | grep -a -E "integratord|custom-telegram"
```

You can also check whether the script exists and has the correct permissions:

```bash
ls -l /var/ossec/integrations/custom-telegram
```

Expected result should look similar to this:

```text
-rwxr-x--- 1 root wazuh ... /var/ossec/integrations/custom-telegram
```

## Common Issues

### FileNotFoundError

If you see a `FileNotFoundError`, the script may be reading the wrong argument.

This integration uses:

```python
alert_file = sys.argv[1]
```

This is important because Wazuh passes the alert JSON file path as the first argument when using a minimal custom integration block.

### Permission denied

Make sure the script has the correct owner and permissions:

```bash
sudo chown root:wazuh /var/ossec/integrations/custom-telegram
sudo chmod 750 /var/ossec/integrations/custom-telegram
```

### No Telegram message

Check that:

- the bot token is correct
- the chat ID is correct
- the bot has permission to send messages
- Wazuh Manager was restarted
- the alert level is high enough to trigger the integration

