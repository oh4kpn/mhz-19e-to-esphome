# MH-Z19E CO2 Sensor with ESPHome

This repository contains an example ESPHome configuration for using an **MH-Z19E CO₂ sensor** via UART, including **manual calibration** and a **fixed ppm offset** based on outdoor reference measurements.

## Features

- UART-based MH-Z19E CO₂ sensor support  
- CO₂ concentration and temperature reporting  
- Fixed CO₂ offset compensation  
- Manual zero-point calibration via Home Assistant button  
- Automatic Baseline Calibration (ABC) disabled for improved long-term accuracy  

## Hardware

- ESP32 or ESP8266 (with available UART)
- MH-Z19E CO₂ sensor

## UART Configuration

The sensor communicates over UART at **9600 baud**:

```yaml
uart:
  tx_pin: GPIO1
  rx_pin: GPIO3
  baud_rate: 9600
