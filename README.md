# IoT_eps32_Telegram_outputs-Arduino-IDE-
This guide shows how to control the ESP32 or ESP8266 NodeMCU GPIOs from anywhere in the world using Telegram. As an example, we’ll control a LED, but you can control any other output. You just need to send a message to your Telegram Bot to set your outputs HIGH or LOW. The ESP boards will be programmed using Arduino IDE.

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

## Creating a Telegram Bot for IOs
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

## Preparin Arduino IDE
We'll program the ESP32 and ESP8266 boards using Arduino IDE, so make sure you have them installed in your Arduino IDE.

[Installing the ESP32 Board in Arduino IDE (Windows, Mac OS X, Linux)](https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/)

[Installing ESP8266 Board in Arduino IDE (Windows, Mac OS X, Linux)](https://randomnerdtutorials.com/how-to-install-esp8266-board-arduino-ide/)


### Installing ESP32 Add-on in Arduino IDE
1. In your Arduino IDE, got to **Arduino IDE> Preferences**<img width="724" alt="Schermafbeelding 2022-10-11 om 17 29 59" src="https://user-images.githubusercontent.com/70894669/195134710-8360271e-717c-44c6-a757-26df1c6bf013.png">

2. Enter the following into the "Additional Board Manager URLs" field: https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json Then click the Ok button.
**Note:** If you have already have the ESP8266 boards URL, you can seperate the URLs with a comma as follows: https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json, http://arduino.esp8266.com/stable/package_esp8266com_index.json

3. Open the Boards Manager. Go to **Tools> Board> Boards Manager...**<img width="858" alt="Schermafbeelding 2022-10-11 om 17 33 25" src="https://user-images.githubusercontent.com/70894669/195135474-cc7f4c07-49d6-4cf1-80ee-96655330b129.png">

4. Search for **ESP32** and press install button for the "**ESP32 by Espressif Systems**".
<img width="316" alt="Schermafbeelding 2022-10-11 om 17 34 28" src="https://user-images.githubusercontent.com/70894669/195135695-692d8878-b517-4ef0-b92f-05a5bd1ecd35.png">

5. That's it. It should be installed after a few seconds.

### Testing the installation

1. Select your Board in **Tools > Board** menu (in my case it's the DOIT ESP32 DEVKIT V1)
![IMG_0364](https://user-images.githubusercontent.com/70894669/195136952-f1ddf458-cae0-4bf2-baf7-6c032dc8db33.png)

2. Select the Port (if you don't see the Slab_USBtoArt Port in your Arduino IDE, you need to install the [CP210x USB to UART Bridge VCP Drivers](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers).<img width="833" alt="Schermafbeelding 2022-10-11 om 18 10 27" src="https://user-images.githubusercontent.com/70894669/195144172-79278049-7c97-4081-b359-616ba51d74be.png">

3. Open the following example under **File > Examples > WiFi (ESP32) > WiFiScan**<img width="775" alt="Schermafbeelding 2022-10-11 om 18 13 28" src="https://user-images.githubusercontent.com/70894669/195144798-f129ae08-fba4-43df-818b-276e3fb50f90.png">

4. A new sketch opens in your Arduino IDE:<img width="765" alt="Schermafbeelding 2022-10-11 om 18 13 59" src="https://user-images.githubusercontent.com/70894669/195144928-7fd4cfbc-9522-4443-a701-4466d10703b1.png">

5. Press the **Upload** button in your Arduino IDE. Wait a few seconds while the code complies and uploads to your board.

An error occured at my Arduino IDE: xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun.

How I fixed it: https://apple.stackexchange.com/questions/254380/why-am-i-getting-an-invalid-active-developer-path-when-attempting-to-use-git-a

Open **Terminal**, and run the following code: xcode-select --install
This will download and install the [Command line Tools package](https://developer.apple.com/library/archive/technotes/tn2339/_index.html) and fix the problem.

After this problem a different problem occured:
Wrong boot mode detected (0x13)! The chip needs to be in download mode. (ESPTOOL-455)
How i fixed it: https://pythontechworld.com/issue/espressif/esptool/741

While the code is uploading **press** the boot button on the ESP32.
![IMG_0365](https://user-images.githubusercontent.com/70894669/195146147-3f4eeaee-18e8-487c-a395-4b1113d5e9c9.png)

6. If everything went as expected, you should see a **"Done uploading"** message.
7. Open the Arduino IDE Serial Monitor at a baud rate of 115200:
<img width="186" alt="Schermafbeelding 2022-10-11 om 18 22 31" src="https://user-images.githubusercontent.com/70894669/195146651-b31b6acc-f9b4-4635-8361-12cbd775d6ac.png">
It's located at the Top right corner.

Result:
<img width="770" alt="Schermafbeelding 2022-10-11 om 18 23 34" src="https://user-images.githubusercontent.com/70894669/195147015-b304edb7-2e06-4839-9cb6-711dc5fd014a.png">
Change to 115200 baud and you'll get this:
<img width="598" alt="Schermafbeelding 2022-10-11 om 18 25 10" src="https://user-images.githubusercontent.com/70894669/195147353-9b68a6d1-38d8-4e32-a73d-b42d58c3ddd1.png">

And that's it.

#### Troubleshooting
If you have more problems check out this [page](https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/) and scroll down to **Troubleshooting**.

## Universal Telegram Bot Library
To interact with the Telegram bot, we'll use the Universal Telegram Bot Library created by Brian Lough that provides an easy interface for the Telegram Bot API.

Follow the next steps to install the latest release of the library.

1. [Click here to download the Universal Arduino Telegram Bot library](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/archive/master.zip)
2. Go to **Sketch > Include Library > Add.ZIP library..**<img width="741" alt="Schermafbeelding 2022-10-11 om 18 31 48" src="https://user-images.githubusercontent.com/70894669/195148685-eb199f78-8ec3-45e2-add9-d8e12ccaf506.png">

3. Add the library you've just downloaded.
<img width="228" alt="Schermafbeelding 2022-10-11 om 18 32 15" src="https://user-images.githubusercontent.com/70894669/195148776-6034d947-5f41-4167-9074-320c5d78e74a.png">


And that's it. The library is installed.

Important: Don't install the library through the Arduino Library manager because it might install a deprecated version.

For all the details about the library, take a look at the Universal Arduino Telegram Bot library [Github](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot) page.

## ArduinoJson Library.
You also have to install the [ArduinoJson](https://github.com/bblanchon) library. Follow the next steps to install the library.
1. Go to **Sketch > Include Library > Manage Libraries.**
2. Search for "ArduinoJson".
3. Install the Library.
<img width="189" alt="Schermafbeelding 2022-10-11 om 18 33 59" src="https://user-images.githubusercontent.com/70894669/195149096-842821a7-c291-4288-baeb-e059564c7957.png">

We're using ArduinoJson library version 6.19.3.

## Parts Required
For this example we'll control the ESP on-board LEDs:
• [ESP32 board](https://makeradvisor.com/tools/esp32-dev-board-wi-fi-bluetooth/) (read [Best ESP32 dev boards](https://makeradvisor.com/esp32-development-boards-review-comparison/))
• Alternative - [ESP8266](https://makeradvisor.com/tools/esp8266-esp-12e-nodemcu-wi-fi-development-board/) board (read [Best ESP8266 dev boards](https://makeradvisor.com/tools/esp32-dev-board-wi-fi-bluetooth/)

## Control outputs using Telegram - ESP32/ESP8266 Sketch
The following code allows you to control your ESP32 or ESP8266 NodeMCU GPIOs by sending messages to a Telegram Bot. To make it work for you, you need to insert your network credentials (SSID and password), the Telegram Bot Token and your Telegram User ID.

```
/*
  Rui Santos
  Complete project details at https://RandomNerdTutorials.com/telegram-control-esp32-esp8266-nodemcu-outputs/
  
  Project created using Brian Lough's Universal Telegram Bot Library: https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot
  Example based on the Universal Arduino Telegram Bot Library: https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/FlashLED/FlashLED.ino
*/

#ifdef ESP32
  #include <WiFi.h>
#else
  #include <ESP8266WiFi.h>
#endif
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>   // Universal Telegram Bot Library written by Brian Lough: https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot
#include <ArduinoJson.h>

// Replace with your network credentials
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";

// Initialize Telegram BOT
#define BOTtoken "XXXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"  // your Bot Token (Get from Botfather)

// Use @myidbot to find out the chat ID of an individual or a group
// Also note that you need to click "start" on a bot before it can
// message you
#define CHAT_ID "XXXXXXXXXX"

#ifdef ESP8266
  X509List cert(TELEGRAM_CERTIFICATE_ROOT);
#endif

WiFiClientSecure client;
UniversalTelegramBot bot(BOTtoken, client);

// Checks for new messages every 1 second.
int botRequestDelay = 1000;
unsigned long lastTimeBotRan;

const int ledPin = 2;
bool ledState = LOW;

// Handle what happens when you receive new messages
void handleNewMessages(int numNewMessages) {
  Serial.println("handleNewMessages");
  Serial.println(String(numNewMessages));

  for (int i=0; i<numNewMessages; i++) {
    // Chat id of the requester
    String chat_id = String(bot.messages[i].chat_id);
    if (chat_id != CHAT_ID){
      bot.sendMessage(chat_id, "Unauthorized user", "");
      continue;
    }
    
    // Print the received message
    String text = bot.messages[i].text;
    Serial.println(text);

    String from_name = bot.messages[i].from_name;

    if (text == "/start") {
      String welcome = "Welcome, " + from_name + ".\n";
      welcome += "Use the following commands to control your outputs.\n\n";
      welcome += "/led_on to turn GPIO ON \n";
      welcome += "/led_off to turn GPIO OFF \n";
      welcome += "/state to request current GPIO state \n";
      bot.sendMessage(chat_id, welcome, "");
    }

    if (text == "/led_on") {
      bot.sendMessage(chat_id, "LED state set to ON", "");
      ledState = HIGH;
      digitalWrite(ledPin, ledState);
    }
    
    if (text == "/led_off") {
      bot.sendMessage(chat_id, "LED state set to OFF", "");
      ledState = LOW;
      digitalWrite(ledPin, ledState);
    }
    
    if (text == "/state") {
      if (digitalRead(ledPin)){
        bot.sendMessage(chat_id, "LED is ON", "");
      }
      else{
        bot.sendMessage(chat_id, "LED is OFF", "");
      }
    }
  }
}

void setup() {
  Serial.begin(115200);

  #ifdef ESP8266
    configTime(0, 0, "pool.ntp.org");      // get UTC time via NTP
    client.setTrustAnchors(&cert); // Add root certificate for api.telegram.org
  #endif

  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, ledState);
  
  // Connect to Wi-Fi
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  #ifdef ESP32
    client.setCACert(TELEGRAM_CERTIFICATE_ROOT); // Add root certificate for api.telegram.org
  #endif
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi..");
  }
  // Print ESP32 Local IP Address
  Serial.println(WiFi.localIP());
}

void loop() {
  if (millis() > lastTimeBotRan + botRequestDelay)  {
    int numNewMessages = bot.getUpdates(bot.last_message_received + 1);

    while(numNewMessages) {
      Serial.println("got response");
      handleNewMessages(numNewMessages);
      numNewMessages = bot.getUpdates(bot.last_message_received + 1);
    }
    lastTimeBotRan = millis();
  }
}
```
The code is compatible with ESP32 and ESP8266 NodeMCU boards (it's based on the Universal Arduino Telegram Bot library [example](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/blob/master/examples/ESP8266/FlashLED/FlashLED.ino)).The code will load the right libraries accordingly to the selected board.

>**Problem**: After uploading the code I got this message:
<img width="1075" alt="Schermafbeelding 2022-10-11 om 21 57 32" src="https://user-images.githubusercontent.com/70894669/195186767-d75f5ec3-b883-45e8-a58a-c43fd39305f1.png">
Ways to [solve](https://pythontechworld.com/issue/espressif/esptool/741) it. 

Press the **Boot** button while you're uploading, and this is the desired result.
<img width="1072" alt="Schermafbeelding 2022-10-11 om 22 01 20" src="https://user-images.githubusercontent.com/70894669/195187364-cd9f69d9-6469-4603-a164-a475fac61d9f.png">


## How the Code Works
This sections explain how the code works. Contiune reading or skip to the demonstration section.

Start by importing the required libraries.
```
#ifdef ESP32
  #include <WiFi.h>
#else
  #include <ESP8266WiFi.h>
#endif
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>
#include <ArduinoJson.h>
```

## Network Credentials
Insert your network credentials in the following variables.
```
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";
```
## Define Output
Set the GPIO you want to control. In our case, we'll control GPIO 2 (built-in LED) and its state is ```LOW``` by default.
```
const int ledPin = 2;
bool ledState = LOW;
```
>**Note**: If you're using an ESP8266, the built-in LED works with inverted logic. So, you should send a `LOW` signal to turn the LED on and a `HIGH` signal to turn it off.

## Telegram Bot Token
Insert your Telegram Bot Token you've got from BotFather on the `BOTtoken` variable.
```
#define BOTtoken "XXXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"  // your Bot Token (Get from Botfather)
```
## Telegram User ID
Insert your chat ID. The one you've got from the IDBot.
```
#define CHAT_ID "XXXXXXXXXX"
```
Create a new WiFi client with `WiFiClientSecure`.
```
WiFiClientSecure client;
```
Create a `bot` with the token and client defined earlier.
```
UniversalTelegramBot bot(BOTtoken, client);
```
The `botRequestDelay` and `lastTimeBotRan` are used to check for new Telegram messages every x number of seconds. In this case, the code whill check for new messages every second (1000 milliseconds). You can change the delay time in the `botRequestDelay` variable.
```
int botRequestDelay = 1000;
unsigned long lastTimeBotRan;
```
## handleNewMessages()
The `handleNewMessages()` function handles what happens when new messages arrive.
```
void handleNewMessages(int numNewMessages) {
  Serial.printIn("handleMessages");
  Serial.printIn(String(numNewMessages));
```
It checks the available messages:
```
for (int i=0; i<numNewMessages; i++) {
```
Get the chad ID for that particular message and store it in the `chat_id` variable. The chat ID allows us to identify who sent the message.
```
String chat_id = String(bot.messages[i].chat_id);
```
If the `chat_id` is different from your chat ID (`CHAT_ID`), it means that someone (that is not you) has sent a message to your bot. If that's the case, ignore the message and wait for the next message.
```
if (chat_id != CHAT_ID) {
  bot.sendMessage(chat_id, "Unauthorized user", "");
  continue;
}
```
Otherwise, it means that the message was sent from a valid user, so we'll save it in the `text` variable and check its content.
```
String text = bot.messages[i].text;
Serial.printIn(text);
```
The `from_name` variables saves the name of the sender.
```
String from_name = bot.messages[i].from_name;
```
If it receives the /start message, we'll send the valid commands to control the ESP32/ESP8266. This is useful if you happen to forget what are the commands to control your board. 
```
if (text == "/start"){
  String welcome= "Welcome, " + from_name + ".\n";
  Welcome += "Use the following commands to control your outputs. \n\n";
  welcome += "/led_on to turn GPIO ON \n";
  welcome += "/led_off to turn GPIO OFF \n";
  welcome += "/state to request current GPIO state \n";
  bot.sendMessage(chat_id, welcome, "");
}
```
Sending the message to the bot is very simply. You just need to use the `sendMessage()` method on the `bot` object and pass as arguments the recipient's chat ID, the message, and the parse mode.
```
bool sendMessage(String chat_id, String text, String parse_mode = "")
```
In our particular example, we’ll send the message to the ID stored on the chat_id variable (that corresponds to the person who’ve sent the message) and send the message saved on the welcome variable.
```
bot.sendMessage(chat_id, welcome, "");
```
If it receives the /led_on message, turn the LED on and send a message confirming we’ve received the message. Also, update the ledState variable with the new state.

```
if (text == "/led_on") {
  bot.sendMessage(chat_id, "LED state set to ON", "");
  ledState = HIGH;
  digitalWrite(ledPin, ledState);
}
```
Do something similar for the /led_off message.
```
if (text == "/led_off") {
  bot.sendMessage(chat_id, "LED state set to OFF", "");
  ledState = LOW;
  digitalWrite(ledPin, ledState);
}
```
>***Note***: if you're using and ESP8266, the built-in LED work with inverted logic. So, you should send a `LOW` signal to turn the LED on and a `HIGH` signal to turn it off.

Finally, if the received message is /state, check the current GPIO state and send a message accordingly.
```
if (text == "/state") {
  if (digitalRead(ledPin)){
    bot.sendMessage(chat_id, "LED is ON", "");
  }
  else{
    bot.sendMessage(chat_id, "LED is OFF", "");
  }
}
```
## setup()
In the `setup()`, intialize the Serial Monitor.
```
Serial.begin(115200);
```
If you’re using the ESP8266, you need to use the following line:

```
#ifdef ESP8266
  client.setInsecure();
#endif
```
In the library examples for the ESP8266 they say: “This is the simplest way of getting this working. If you are passing sensitive information, or controlling something important, please either use certStore or at least client.setFingerPrint“.

Set the LED as an output and set it to LOW when the ESP first starts:

```
pinMode(ledPin, OUTPUT);
digitalWrite(ledPin, ledState);
```
### Init Wi-Fi
Initialize Wi-Fi and connect the ESP to your local network with the SSID and password defined earlier.
```
WiFi.mode(WIFI_STA);
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED) {
  delay(1000);
  Serial.println("Connecting to WiFi..");
}
```
## loop()
In the `loop()`, check for new messages every second.
```
void loop() {
  if (millis() > lastTimeBotRan + botRequestDelay)  {
    int numNewMessages = bot.getUpdates(bot.last_message_received + 1);

    while(numNewMessages) {
      Serial.println("got response");
      handleNewMessages(numNewMessages);
      numNewMessages = bot.getUpdates(bot.last_message_received + 1);
    }
    lastTimeBotRan = millis();
  }
}
```
When a new message arrives, call the `handleNewMessages` function.
```
while(numNewMessages) {
  Serial.println("got response");
  handleNewMessages(numNewMessages);
  numNewMessages = bot.getUpdates(bot.last_message_received + 1);
}
```
That's pretty much how the code works.

## Demonstration
Upload the code to your ESP32 or ESP8266 board. Don’t forget to go to **Tools > Board** and select the board you’re using. Go to **Tools > Port** and select the COM port your board is connected to.

After uploading the code, press the ESP32/ESP8266 on-board EN/RST button so that it starts running the code. Then, you can open the Serial Monitor to check what’s happening in the background.

Go to your Telegram account and open a conversation with your bot. Send the following commands and see the bot responding:

• **/start** shows the welcome message with the valid commands.
• **/led_on** turns the LED on.
• **/led_off** turns the LED off.
• **/state** requests the current LED state.

![IMG_0371](https://user-images.githubusercontent.com/70894669/195189542-bbbc3fa4-e763-4dd6-bd46-8a2ae34817c6.PNG)


The on-board LED should turn on and turn off accordingly (the ESP8266 on-board LED works in reverse, it’s off when you send /led_on and on when you send /led_off).

![IMG_0373](https://user-images.githubusercontent.com/70894669/195190065-ef8293bf-b15f-49eb-98f1-c14012c665e3.png)


At the same time, on the Serial Monitor you should see that the ESP is receiving the messages.

<img width="1069" alt="Schermafbeelding 2022-10-11 om 22 18 06" src="https://user-images.githubusercontent.com/70894669/195190123-ae51d311-f380-429c-886d-d6b28ff3888f.png">


If you try to interact with your bot from another account, you’ll get the the “Unauthorized user” message.


## Wrapping Up
In this tutorial you’ve learned how to create a Telegram Bot to interact with the ESP32 or ESP8266. With this bot, you can use your Telegram account to send messages to the ESP and control its outputs. The ESP can also interact with the bot to send responses.

We’ve shown you a simple example on how to control an output. The idea is to modify the project to add more commands to execute other tasks. For example, you can [request sensor readings](https://randomnerdtutorials.com/telegram-request-esp32-esp8266-nodemcu-sensor-readings/) or send a message when motion is detected.

The great thing about using Telegram to control your ESP boards, is that as long as you have an internet connection (and your boards too), you can control and monitor them from anywhere in the world.

We hope you’ve found this project interesting. Learn more about the ESP32 and ESP8266 with our resources:

- [Learn ESP32 with Arduino IDE (eBook + Video Course)](https://randomnerdtutorials.com/learn-esp32-with-arduino-ide/)
- [Home Automation using ESP8266](https://randomnerdtutorials.com/home-automation-using-esp8266/)
- [More ESP32 projects and tutorials…](https://randomnerdtutorials.com/projects-esp32/)
- [More ESP8266 projects and tutorials…](https://randomnerdtutorials.com/projects-esp32/)

Thanks for reading.

>**[Source](https://randomnerdtutorials.com/telegram-control-esp32-esp8266-nodemcu-outputs/)**
