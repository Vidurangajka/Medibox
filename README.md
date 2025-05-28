Medibox
Medibox is an ESP32-based IoT system for monitoring and maintaining optimal environmental conditions for medication storage. It uses a DHT22 sensor for temperature and humidity, an LDR for light intensity, and a servo motor to adjust a window or vent based on environmental conditions. The system features an OLED display for real-time data and alarm management, with MQTT integration for remote configuration and data reporting. Medibox also includes a medication reminder system with configurable alarms.
Table of Contents

Overview
Features
Hardware Requirements
Software Requirements
Installation
Usage
MQTT Topics
Contributing
License
Contact

Overview
Medibox ensures medications are stored under optimal conditions by monitoring temperature, humidity, and light intensity. It adjusts a servo-controlled window to regulate the environment, displays real-time data and alerts on an OLED screen, and allows users to set medication reminder alarms via physical buttons. The system connects to WiFi for NTP-based time synchronization and uses MQTT to send light intensity data and receive configuration updates remotely.
Features

Environmental Monitoring: Measures temperature and humidity (DHT22 sensor) and light intensity (LDR).
Servo Control: Adjusts a window or vent based on light intensity and temperature to maintain optimal storage conditions.
Medication Reminders: Supports two configurable alarms with buzzer and LED alerts, including snooze functionality.
OLED Display: Shows time, environmental data, alarm status, and menu navigation.
MQTT Integration: Publishes average light intensity and subscribes to configuration updates (sampling/sending intervals, servo parameters).
Timezone Configuration: Allows setting UTC offset for accurate timekeeping using NTP.
User Interface: Four buttons (OK, Cancel, Up, Down) for navigating menus and configuring alarms/timezone.

Hardware Requirements

ESP32 Development Board (e.g., ESP32-WROOM-32)
DHT22 Sensor: For temperature and humidity measurement
LDR (Light Dependent Resistor): Connected to analog pin for light intensity
Servo Motor: For window/vent control (compatible with ESP32Servo library)
128x64 OLED Display (SSD1306, I2C interface)
Buzzer: For alarm audio feedback
LED: For visual alerts
Push Buttons: Four buttons (OK, Cancel, Up, Down) for user input
Resistors and Breadboard/PCB: For circuit assembly
WiFi Network: For internet connectivity (NTP and MQTT)

Software Requirements

Arduino IDE (2.0 or later recommended)
ESP32 Board Support: Install via Arduino Boards Manager (URL: https://raw.githubusercontent.com/espressif/arduino-esp32/master/package_esp32_index.json)
Libraries:
Adafruit_GFX (v1.10.0 or higher)
Adafruit_SSD1306 (v2.5.0 or higher)
DHTesp (v1.0.0 or higher)
WiFi (included with ESP32 core)
PubSubClient (v2.8.0 or higher)
ESP32Servo (v1.0.0 or higher)


WiFi Credentials: Update ssid and password in sketch.ino for your network
MQTT Broker: Uses broker.hivemq.com (public broker) by default

Installation

Set Up Arduino IDE:

Install the Arduino IDE and add ESP32 board support.
Install the required libraries via the Library Manager or manually.


Clone or Download the Repository:
git clone https://github.com/yourusername/medibox.git

Alternatively, download the sketch.ino file and place it in a folder named medibox.

Configure WiFi Credentials:

Open sketch.ino in the Arduino IDE.
Update the ssid and password variables:const char* ssid = "YourWiFiSSID";
const char* password = "YourWiFiPassword";




Connect Hardware:

Wire the components as per the pin definitions:
DHT22: Pin 12
LDR: Pin 36 (analog)
Servo: Pin 13
Buzzer: Pin 5
LED: Pin 15
Buttons: Pins 32 (OK), 34 (Cancel), 33 (Up), 35 (Down)
OLED: I2C pins (SDA, SCL) with address 0x3C




Upload the Sketch:

Connect the ESP32 to your computer.
Select the appropriate board (e.g., "ESP32 Dev Module") and port in the Arduino IDE.
Upload sketch.ino to the ESP32.



Usage

Power On:

The system initializes the OLED, connects to WiFi, and synchronizes time via NTP.
A welcome message ("Welcome to MediBox") is displayed.


Main Display:

Shows the current time (HH:MM:SS).
Alerts for out-of-range temperature (24–32°C) or humidity (65–80%) appear at the bottom.


Menu Navigation:

Press the OK button to enter the menu.
Use Up and Down buttons to navigate through:
Set Timezone
Set Alarm 1
Set Alarm 2
View/Delete Alarms


Press OK to select an option, Cancel to exit.


Set Timezone:

Adjust UTC offset (hours and minutes) using Up/Down buttons.
Confirm with OK to save and synchronize time.


Set Alarms:

Configure Alarm 1 or Alarm 2 (hour and minute) using Up/Down buttons.
Alarms trigger a buzzer and flashing LED; press OK to snooze (5 minutes) or Cancel to stop.


Environmental Control:

The system monitors temperature, humidity, and light intensity.
The servo adjusts the window angle based on light intensity and temperature, using the formula:[w = w_{\text{offset}} + (180 - w_{\text{offset}}) \cdot \text{intensity} \cdot \epsilon \cdot \log\left(\frac{\text{sampling_interval}}{\text{sending_interval}}\right) \cdot \frac{\text{temperature}}{T_{\text{med}}}]
Alerts are displayed and the LED blinks if conditions are out of range.


MQTT Communication:

Publishes average light intensity to medibox74B/light every 2 minutes (default).
Subscribes to configuration topics (see below).



MQTT Topics

Publish:
medibox74B/light: Average light intensity (0.0–1.0) every sending_interval (default: 120s).


Subscribe:
medibox74B/sampling: Set sampling interval (seconds, min 1.0).
medibox74B/sending: Set sending interval (seconds, min 10.0).
medibox74B/params/offset: Set servo offset angle (w_offset, 0–120°).
medibox74B/params/epsilon: Set control factor (epsilon, 0–1).
medibox74B/params/tmed: Set ideal temperature (T_med, 10–40°C).



Example MQTT command (using a tool like mosquitto_pub):
mosquitto_pub -h broker.hivemq.com -t medibox74B/sampling -m "5.0"

Contributing
Contributions are welcome! To contribute:


