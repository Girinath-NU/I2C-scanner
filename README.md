# I2C Scanner

This repository contains an Arduino sketch to scan for I2C devices connected to your microcontroller. The code identifies the I2C addresses of connected devices and prints the results in the Serial Monitor.

## How It Works

- The sketch iterates through all possible I2C addresses (from 0x01 to 0x7F).
- For each address, it attempts to establish communication using the `Wire.beginTransmission()` function.
- If a device responds, the address is displayed in the Serial Monitor.

## Hardware Requirements

1. Arduino Board (e.g., Uno, Nano, Mega, ESP32, etc.)
2. I2C-compatible device (e.g., sensors, OLED displays, etc.)
3. Jumper wires and breadboard (for connections)

## Connections

| Arduino Pin | I2C Pin |
|-------------|---------|
| A4          | SDA     |
| A5          | SCL     |

For ESP32:
| ESP32 Pin | I2C Pin |
|-----------|---------|
| GPIO 21   | SDA     |
| GPIO 22   | SCL     |

Ensure your I2C device is powered and properly connected to the microcontroller.

## Code

```cpp
#include <Wire.h>

void setup() {
  Wire.begin();
  Serial.begin(9600);
  Serial.println("Scanning for I2C devices...");
}

void loop() {
  for (byte address = 1; address < 127; address++) {
    Wire.beginTransmission(address);
    if (Wire.endTransmission() == 0) {
      Serial.print("Found I2C device at address 0x");
      Serial.println(address, HEX);
    }
  }
  delay(1000);
}
