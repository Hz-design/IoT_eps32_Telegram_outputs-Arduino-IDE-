# IoT_eps32_Telegram_outputs-Arduino-IDE-
This guide shows how to control the ESP32 or ESP8266 NodeMCU GPIOs from anywhere in the world using Telegram. As an example, we’ll control an LED, but you can control any other output. You just need to send a message to your Telegram Bot to set your outputs HIGH or LOW. The ESP boards will be programmed using Arduino IDE.

## Project overview
In this tutorial we’ll build a simple project that allows you to control ESP32 or ESP8266 NodeMCU GPIOs using Telegram. You can also control a relay module.
![image](https://user-images.githubusercontent.com/70894669/195111155-cd0ed6da-7d0e-4b40-b6ab-e886bf384acb.png)
- You’ll create a Telegram bot for your ESP32/ESP8266 board;
- You can start a conversation with the bot;
- When you send the message /led_on to the bot, the ESP board receives the message and turns GPIO 2 on;
- Similarly, when you send the message /led_off, it turns GPIO 2 off;
- Additionally, you can also send the message /state to request the current GPIO state. When the ESP receives that message, the bot responds with the -   current GPIO state;
- You can send the /start message to receive a welcome message with the commands to control the board.
- This is a simple project, but shows how you can use Telegram in your IoT and Home Automation projects. The idea is to apply the concepts learned in your own projects.

## Introducing telegram
Telegram Messenger is a cloud-based instant messaging and voice over IP service. You can easily install it in your smartphone (Android and iPhone) or computer (PC, Mac and Linux). It is free and without any ads. Telegram allows you to create bots that you can interact with.

“Bots are third-party applications that run inside Telegram. Users can interact with bots by sending them messages, commands and inline requests. You control your bots using HTTPS requests to Telegram Bot API“.

The ESP32/ESP8266 will interact with the Telegram bot to receive and handle the messages, and send responses. In this tutorial you’ll learn how to use Telegram to send messages to your bot to control the ESP outputs from anywhere (you just need Telegram and access to the internet).

### Creating a Telegram Bot for IOs
1. Go to App store, download and install Telegram.
![image](https://user-images.githubusercontent.com/70894669/195111740-63426a14-85b2-4582-b572-eeacee22e2b4.png)

2. Open Telegram and follow the next steps to create a Telegram Bot. First, search for "botfather" and click the BotFather as shown below. Or open this link: t.me/botfather in your smartphone. 

3. Click on "start" button.

Problem: BotFather doesn't react on messages.
<img src="https://user-images.githubusercontent.com/70894669/195118891-36d0c92d-92e2-4cbc-b910-9d7faf74fdee.PNG" width="150">
When I frist started Botfather i Got this message, after that I deleted the application, installed it again and "deleted chat" after that I started a new chat with BotFather and it gave me a different respond which does work.
<img src="https://user-images.githubusercontent.com/70894669/195118807-b6f02536-9c46-41d5-adb3-e2452d692096.PNG" width="150">

4. Type /newbot and follow the instructions to create your bot. Give it a name and username.
<img src="(https://user-images.githubusercontent.com/70894669/195122810-767a3d2a-6925-448e-a953-510b6505cb36.jpg" width="300">
