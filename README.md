# Medibox

**Medibox** is an ESP32-based IoT system for monitoring and maintaining optimal environmental conditions for medication storage. It includes sensors for temperature, humidity, and light, and features servo-controlled environmental adjustments, an OLED display for feedback, and a medication reminder system. MQTT integration enables remote configuration and monitoring.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Installation](#installation)
- [Usage](#usage)
- [MQTT Topics](#mqtt-topics)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 📖 Overview

Medibox ensures medications are stored under optimal conditions by:

- Monitoring temperature, humidity, and light levels.
- Automatically adjusting a servo-controlled window or vent.
- Displaying real-time data on an OLED screen.
- Providing configurable medication reminder alarms.
- Supporting MQTT communication for data reporting and remote updates.
- Synchronizing time via NTP with customizable timezones.

---

## ✨ Features

- **Environmental Monitoring**:
  - Temperature and humidity via DHT22 sensor.
  - Light intensity via LDR sensor.

- **Servo Control**:
  - Window/vent adjustment based on environmental data.

- **Medication Reminders**:
  - Two alarms with buzzer and LED.
  - Snooze functionality.

- **OLED Display**:
  - Shows time, sensor data, alarm status, and menu options.

- **MQTT Integration**:
  - Publishes light data.
  - Subscribes to parameter and interval updates.

- **User Interface**:
  - 4 push buttons: OK, Cancel, Up, Down.

---

## 🧰 Hardware Requirements

- ESP32 Development Board
- DHT22 Sensor
- LDR Sensor (Analog pin)
- Servo Motor
- OLED Display (SSD1306, I2C, 128x64)
- Buzzer
- LED
- 4 Push Buttons:
  - OK: Pin 32
  - Cancel: Pin 34
  - Up: Pin 33
  - Down: Pin 35
- Breadboard/PCB and Resistors
- WiFi Connection

---

## 🖥️ Software Requirements

- Arduino IDE (v2.0+)
- ESP32 Board Support (Install via Boards Manager):
