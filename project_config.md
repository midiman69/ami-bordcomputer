# Project Configuration
MQTT Broker: mqtt://broker.example.com
Raspberry Pi: Hostname ami-pi, statische IP 192.168.1.50
ESP32: ESP32-A (Wächter 1), ESP32-B (Wächter 2)
Pinout:
- ESP32-A: D5 -> Trigger, D18 -> Echo
- Pi Camera: CSI Port
Libraries: esp-idf v5.x; paho-mqtt; Flask 2.x
