<div align="center">
  <h1>S.H.I.E.L.D. Guardian</h1>

![ESP32](https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white)
![MicroPython](https://img.shields.io/badge/MicroPython-2B2728?style=for-the-badge&logo=micropython&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![MQTT](https://img.shields.io/badge/MQTT-660066?style=for-the-badge&logo=mqtt&logoColor=white)
![Kivy](https://img.shields.io/badge/Kivy-FF6900?style=for-the-badge&logo=kivy&logoColor=white)

*IoT smart caveau with ESP32, MicroPython, MQTT, and I2C for remote door control and burglar detection via a Kivy GUI application.*

[📚 Overview](#-overview) • [✨ Features](#-features) • [🔌 Hardware Components](#-hardware-components) • [🏗️ System Architecture](#️-system-architecture) • [🛠️ Setup & Installation](#️-setup--installation) • [🎥 Demo Video](#-demo-video) • [📁 Repository Structure](#-repository-structure) • [👨‍💻 Authors](#-authors)
</div>

---

## 📚 Overview

S.H.I.E.L.D. Guardian is an IoT-based smart caveau developed as part of the *Internet of Things* course at the University of Salerno. The system runs on an ESP32 microcontroller programmed in MicroPython and combines traditional vault security with digital and electronic components for enhanced functionality and protection.

The caveau is controlled remotely through a Python GUI application built with Kivy and KivyMD. The ESP32 communicates with the GUI over MQTT and drives a servo motor to open and close the door, an OLED display via I2C to show the lock state, a buzzer and LEDs for alarm feedback, and an infrared sensor for intrusion detection.

---

## ✨ Features

S.H.I.E.L.D. Guardian provides **remote door control** through the GUI application: the user can unlock the caveau by entering the correct PIN, which triggers the servo motor to open the door. The OLED display reflects the current state of the lock in real time, showing a closed lock, open lock, or broken lock icon depending on the system status.

The system includes a **two-level alarm system**. If the user enters the wrong PIN five times consecutively, a 10-second alarm is triggered — the buzzer sounds and the LEDs flash in sequence. Additionally, the user can activate the infrared sensor through the GUI: if someone attempts to open the door physically without entering the correct code, the alarm goes off continuously until the right PIN is entered remotely.

The **GUI application** allows the user to unlock the caveau, close it remotely, change the password, toggle the alarm on or off, and view a log of burglar attempts through a dedicated Notifications tab.

---

## 🔌 Hardware Components

| Component | Description |
|-----------|-------------|
| ESP32 | Main microcontroller running the application logic in MicroPython |
| Micro Servo Motor | Controls the physical opening and closing of the caveau door |
| SSD1306 OLED | Displays the current lock state via I2C protocol |
| Infrared Sensor (PIR) | Detects physical intrusion attempts when alarm is active |
| Buzzer Piezo | Sounds the alarm on unauthorized access attempts |
| LEDs × 4 | Flash in sequence to provide visual alarm feedback |

---

## 🏗️ System Architecture

The project is organized into two main layers. The first is the **embedded layer** running on the ESP32 in MicroPython. The main logic is implemented in `caveau.py`, which manages the door state, drives the servo motor, updates the OLED display via I2C, activates the buzzer alarm, handles the infrared interrupt, and communicates over MQTT. The `buzzer_class.py` module provides the buzzer driver.

The second is the **remote interaction layer** built with Python on desktop. The GUI application (`S.H.I.EL.D.Guardian.py`), developed with Kivy and KivyMD, allows the user to interact with the caveau remotely. It publishes and subscribes to MQTT messages to send commands (unlock, close, alarm toggle, password change) and receive intrusion notifications.

The two layers communicate through the **MQTT protocol** using a public broker (`test.mosquitto.org`). The I2C protocol is used internally on the ESP32 to drive the OLED display.

---

## 🛠️ Setup & Installation

### Prerequisites

- ESP32 with MicroPython firmware installed
- A MicroPython-compatible IDE such as Thonny
- Python 3 with `kivy` and `kivymd` installed
- A Wi-Fi connection

### ESP32 Deployment

Upload all files inside the `ESP32/` folder to the ESP32 filesystem. Then open `caveau.py` and replace the Wi-Fi credentials with your own network SSID and password:

```python
sta_if.connect('YOUR_SSID', 'YOUR_PASSWORD')
```

### GUI Application

Install the required Python dependencies:

```bash
pip install kivy kivymd
```

Then run the GUI application:

```bash
python "GUI Application/S.H.I.EL.D.Guardian.py"
```

---

## 🎥 Demo Video

The following video provides a practical demonstration of the project, including the system behavior, hardware components, and remote interaction through the GUI:

[📺 Watch the demo](caveau_video.mp4) 

---

## 📁 Repository Structure

```text
S.H.I.E.L.D.-Guardian-IOT-Smart-Caveau/
├── 📁 ESP32/
│ ├── buzzer_class.py # Buzzer driver
│ └── caveau.py # Main ESP32 logic
├── 📁 GUI Application/
│ └── S.H.I.EL.D.Guardian.py # Kivy desktop application
└── LICENSE
```

---

## 👨‍💻 Authors

Chiara Ferraioli\
Davide Gigante\
Francesco Ferraù
