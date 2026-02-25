# 🤖 ESP32-DeepSeek Portable Voice Assistant (MVP Prototype)

![Platform](https://img.shields.io/badge/Platform-ESP32--S3-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-orange)
![LLM](https://img.shields.io/badge/AI_Brain-DeepSeek-deepblue)
![License](https://img.shields.io/badge/License-MIT-green)

> **An Ultra-Low-Cost, Portable AI Voice Assistant MVP Powered by ESP32-S3 and DeepSeek.**
> 
> 基于 ESP32-S3 与 DeepSeek 大模型的超低成本便携式 AI 语音交互终端（MVP原型）。

## 💡 Project Overview | 项目简介

This project demonstrates how to build a fully functional, offline-capable, and portable AI voice assistant using a microcontroller for under $10 (approx. 50 RMB). It integrates Baidu's STT (Speech-to-Text), DeepSeek's LLM API for logical thinking, and Youdao's TTS (Text-to-Speech) into a seamless closed-loop hardware pipeline.

本项目旨在通过低于 50 元人民币的硬件成本，打造一个完全脱离电源线束缚、具备大模型逻辑思考能力的实体 AI 语音助手。

### ✨ Key Features | 核心特性
- **Ultimate Portability (极致便携)**: Powered by a 3.7V Li-Po battery with a TP4056 charging module.
- **Pure Digital Audio (纯数字音频)**: Utilizes INMP441 (Mic) and MAX98357A (Amp) via I2S digital bus to eliminate analog noise.
- **High-IQ Brain (高智商大脑)**: Integrated with the DeepSeek API, breaking the limits of traditional "smart" speakers.
- **Crash-Proof Design (防崩溃工程设计)**: Optimized code to prevent Watchdog resets and hardware Brownout issues caused by audio power surges.

---

## 🛠️ Bill of Materials (BOM) | 硬件清单

| Item (器材) | Description / Spec (规格说明) |
| :--- | :--- |
| **MCU** | ESP32-S3 Development Board (**Must have PSRAM**, e.g., N8R8) |
| **Microphone** | INMP441 I2S Omnidirectional Digital Microphone |
| **Amplifier** | MAX98357A I2S Audio Amplifier Module |
| **Speaker** | 4Ω 3W (or 8Ω 2W) Passive Speaker |
| **Power** | 3.7V Li-Po Battery + TP4056 Charging/Protection Module |
| **Others** | Perfboard (洞洞板), jumper wires/solder |

---

## 🔌 Wiring Diagram | 接线指南

**⚠️ WARNING:** Do NOT connect the INMP441 VDD to 5V! It will burn the mic instantly.
**⚠️ 警告:** INMP441 麦克风切勿接 5V，必须接 3.3V！功放必须接 5V 保证功率。

| Peripheral (外设) | Pin | ESP32-S3 Pin | Note (备注) |
| :--- | :---: | :---: | :--- |
| **INMP441 (Mic)** | VDD | 3.3V | Strictly 3.3V |
| | GND | GND | Ground |
| | L/R | GND | Set to Left Channel |
| | WS | GPIO 15 | Word Select |
| | SCK | GPIO 14 | Serial Clock |
| | SD | GPIO 16 | Serial Data |
| **MAX98357A (Amp)** | VIN | 5V / VBUS | Needs 5V for high power output |
| | GND | GND | Ground |
| | LRC | GPIO 5 | Left/Right Clock |
| | BCLK | GPIO 4 | Bit Clock |
| | DIN | GPIO 6 | Data Input |

*Note: The system utilizes the onboard `BOOT` button (GPIO 0) as the Push-to-Talk (PTT) trigger.*

---

## 🚀 Quick Start | 快速上手

### 1. Software Dependencies (依赖库)
Please install the following libraries in Arduino IDE Library Manager:
- `ArduinoJson` (by Benoit Blanchon)
- `ESP32-audioI2S` (by schreibfaul1)

### 2. Arduino IDE Settings (编译设置)
Before compiling, navigate to `Tools` and ensure the following settings are strictly applied:
- **Board**: `ESP32S3 Dev Module`
- **PSRAM**: `OPI PSRAM` (CRITICAL! Fails to allocate recording buffer if disabled)
- **USB CDC On Boot**: `Enabled` (To view Serial Monitor output)

### 3. API Keys Configuration (配置密钥)
Open the `.ino` file and replace the placeholders with your actual credentials:
```cpp
const char* ssid             = "YOUR_WIFI_SSID";
const char* password         = "YOUR_WIFI_PASSWORD";
const char* baidu_api_key    = "YOUR_BAIDU_AK";
const char* baidu_secret_key = "YOUR_BAIDU_SK";
const char* deepseek_key     = "sk-YOUR_DEEPSEEK_KEY";
