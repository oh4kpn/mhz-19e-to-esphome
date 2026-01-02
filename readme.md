# MH-Z19E CO2 Sensor with ESPHome

This repository contains an example ESPHome configuration for using an
**MH-Z19E CO₂ sensor** via UART, including **manual calibration** and a
**fixed ppm offset** based on outdoor reference measurements.

## Features

-   UART-based MH-Z19E CO₂ sensor support\
-   CO₂ concentration and temperature reporting\
-   Fixed CO₂ offset compensation\
-   Manual zero-point calibration via Home Assistant button\
-   Automatic Baseline Calibration (ABC) disabled for improved long-term
    accuracy

## Hardware

-   ESP32 or ESP8266 (with available UART)
-   MH-Z19E CO₂ sensor

## UART Configuration

The sensor communicates over UART at **9600 baud**:

``` yaml
uart:
  tx_pin: GPIO1
  rx_pin: GPIO3
  baud_rate: 9600
```

> ⚠️ Adjust TX/RX pins according to your board and wiring.

## CO₂ Offset Calibration

The MH-Z19E sensor internally considers **400 ppm** as its zero
reference. Outdoor measurements near the installation site indicated a
real CO₂ level of approximately **428 ppm**, so a fixed **+28 ppm
offset** is applied:

``` yaml
filters:
  - offset: 28.0
```

You should verify your local outdoor CO₂ reference before choosing an
offset.

Example public reference (Finland, FMI Uto station):\
https://swell.fmi.fi/Uto/graphs_pco2both_1d.html

## Manual Calibration

Automatic Baseline Calibration (ABC) is disabled:

``` yaml
automatic_baseline_calibration: false
```

Instead, calibration is performed manually using a Home Assistant
button.

### Calibration Procedure

1.  Place the sensor outdoors or in well-ventilated outdoor air\
2.  Let it stabilize for **at least 20 minutes**\
3.  Press the **"Calibrate CO2"** button in Home Assistant\
4.  The sensor is calibrated to **400 ppm**\
5.  ESPHome applies the configured offset automatically

## Home Assistant Integration

A template button is exposed to Home Assistant for easy calibration:

``` yaml
button:
  - platform: template
    name: "Calibrate Example CO2 (Outdoor ~428 ppm)"
```

## Notes

-   Manual calibration once per year is usually sufficient\
-   Disabling ABC prevents indoor CO₂ levels from shifting the baseline\
-   The temperature reading from the MH-Z19E is also exposed for
    monitoring

## License

MIT License -- free to use, modify, and distribute.
