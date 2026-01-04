ESP32-S3-CAM AI Chatbot
Introduction

An MCP-based AI chatbot specifically designed for ESP32-S3-CAM development boards. This project combines camera functionality with voice interaction capabilities, creating a versatile AI assistant that can see and hear.
<img src="docs/esp32-s3-cam-setup.jpg" alt="ESP32-S3-CAM Setup" width="320">
Hardware Specifications
ESP32-S3-CAM Development Board Features

    Processor: ESP32-S3 dual-core Xtensa LX7 up to 240MHz

    Memory: 8MB PSRAM, 8MB Flash

    Camera: OV2640 sensor (2MP)

    Audio: Built-in microphone and speaker interfaces

    Connectivity: WiFi 4, Bluetooth 5, USB-C for programming

    GPIO: Multiple GPIO pins for peripherals

    Special Note: Camera uses pins 19 and 20 which are shared with USB functionality

Quick Start Guide
1. Development Environment Setup

Install ESP-IDF (Version 5.4 or above):
bash

# Clone ESP-IDF
git clone -b v5.4 --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
./install.sh all
source export.sh

2. Clone the Repository
bash

git clone --recursive https://github.com/
cd edubuddy

3. Configure for ESP32-S3-CAM

Set target:
bash

idf.py set-target esp32s3

Configure settings:
bash

idf.py menuconfig

Navigate to:
text

Edubuddy Assistant -> Board Type -> ESP32-S3-CAM (with Camera)

4. Camera Configuration

In menuconfig:

    Go to: Component config → Espressif Camera Sensors Configurations

    Select Camera Sensor Configuration → Select and Set Camera Sensor

    Choose OV2640 as the sensor

    Enable Auto detect

    Set default output format to YUV422 (recommended for memory efficiency)

5. Build and Flash
bash

idf.py build
idf.py -p PORT flash monitor

Replace PORT with your actual serial port (e.g., /dev/ttyUSB0 or COM3).
Pin Configuration for ESP32-S3-CAM
Camera Pins (OV2640)
c

#define CAMERA_PIN_D0    GPIO_NUM_11
#define CAMERA_PIN_D1    GPIO_NUM_9
#define CAMERA_PIN_D2    GPIO_NUM_8
#define CAMERA_PIN_D3    GPIO_NUM_10
#define CAMERA_PIN_D4    GPIO_NUM_12
#define CAMERA_PIN_D5    GPIO_NUM_18
#define CAMERA_PIN_D6    GPIO_NUM_17
#define CAMERA_PIN_D7    GPIO_NUM_16
#define CAMERA_PIN_XCLK  GPIO_NUM_15
#define CAMERA_PIN_PCLK  GPIO_NUM_13
#define CAMERA_PIN_VSYNC GPIO_NUM_6
#define CAMERA_PIN_HREF  GPIO_NUM_7
#define CAMERA_PIN_SIOC  GPIO_NUM_5
#define CAMERA_PIN_SIOD  GPIO_NUM_4
#define CAMERA_PIN_PWDN  GPIO_NUM_NC
#define CAMERA_PIN_RESET GPIO_NUM_NC

Audio Configuration (Optional External Codec)
c

// I2S Audio Pins
#define AUDIO_I2S_GPIO_WS    GPIO_NUM_4
#define AUDIO_I2S_GPIO_BCLK  GPIO_NUM_5
#define AUDIO_I2S_GPIO_DIN   GPIO_NUM_6
#define AUDIO_I2S_GPIO_DOUT  GPIO_NUM_7

Display Configuration (Optional External LCD)
c

// SPI Display Pins
#define DISPLAY_MOSI_PIN      GPIO_NUM_20
#define DISPLAY_CLK_PIN       GPIO_NUM_19
#define DISPLAY_DC_PIN        GPIO_NUM_47
#define DISPLAY_RST_PIN       GPIO_NUM_21
#define DISPLAY_CS_PIN        GPIO_NUM_45
#define DISPLAY_BACKLIGHT_PIN GPIO_NUM_38

Features Specific to ESP32-S3-CAM
1. Camera Integration

    Real-time video streaming via MCP protocol

    Object detection capabilities

    Face recognition support

    QR code scanning

    Environmental awareness (light detection, motion sensing)

2. Voice Interaction

    Offline wake words (ESP-SR)

    Streaming ASR for real-time speech recognition

    Multi-language TTS support

    Speaker identification using 3D-Speaker technology

3. MCP Protocol Support

    Device control through natural language

    Camera operations (take photo, record video, stream)

    IoT integration with home automation

    Multi-device coordination

Application Examples
1. Smart Home Monitor
bash

"Take a picture of the living room"
"Show me who's at the door"
"Monitor the pet while I'm away"

2. Visual Assistant
bash

"Read this text for me"
"Identify this object"
"What's in front of the camera?"

3. Security System
bash

"Detect motion in the room"
"Recognize faces of family members"
"Send alert when unknown person detected"

Advanced Configuration
Memory Optimization

Since ESP32-S3-CAM has limited RAM (8MB PSRAM), optimize settings:

    Use YUV422 instead of RGB565 for camera

    Reduce camera resolution if needed (QVGA instead of VGA)

    Enable PSRAM in menuconfig: Component config → ESP32S3-Specific → Support for external, SPI-connected RAM

Power Management
c

// Configure power saving modes
#define CONFIG_PM_ENABLE 1
#define CONFIG_PM_DFS_INIT_AUTO 1
#define CONFIG_PM_PROFILING 1

Troubleshooting
Common Issues and Solutions

    Camera Not Detected

        Check OV2640 connections

        Verify camera module is properly seated

        Ensure correct pin configuration in config.h

    Memory Allocation Errors

        Reduce camera resolution

        Use YUV422 format

        Enable PSRAM in configuration

    USB Communication Issues

        Pins 19 and 20 are shared between camera and USB

        Consider using external USB-to-serial adapter if conflicts occur

    Audio Quality Problems

        Check I2S connections

        Adjust sample rates in configuration

        Ensure proper grounding

Performance Benchmarks
Feature	Performance	Notes
Camera Capture	15-30 FPS @ VGA	Depends on lighting
Face Detection	5-10 FPS	With optimized model
Voice Recognition	< 200ms latency	Using ESP-SR
MCP Response Time	< 100ms	Local commands
Customization
Adding Custom Wake Words

Use the Custom Assets Generator to create:

    Custom wake words for ESP-SR

    Personalized voice responses

    Brand-specific interactions

Extending Camera Functions
cpp

// Add custom camera processing
void custom_camera_processing() {
    // Your custom image processing code
    // Object detection
    // Face recognition
    // Image filtering
}

Resources
Documentation

    ESP32-S3 Technical Reference

    OV2640 Datasheet

    ESP-IDF Programming Guide

Community Support

    GitHub Issues

    ESP32 Forum

    Project Documentation

License

This project is released under the MIT License. See the LICENSE file for details.
Contributing

Contributions are welcome! Please see our Contributing Guidelines for more information.
Acknowledgments

    Espressif Systems for ESP32-S3 hardware and ESP-IDF

    All contributors to the Edubuddy ESP32 project

    Open source community for various libraries and tools