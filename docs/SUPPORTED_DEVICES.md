# Supported Devices

## 📋 Currently Supported Inverters

- **Deye SG0XLP1** *(Single Phase Low Voltage)*
   
  ***Single Phase Recommended baud rate: 9600 (default, nothing to change)***

- **Deye SG04LP3** *(Low Voltage)*
- **Deye SG05LP3** *(Low Voltage)*
- **Deye SG01HP3** *(High Voltage)*
- **Deye SG02HP3** *(High Voltage)*
   
  ***3 Phases Recommended baud rate: 9600 (default, nothing to change)***

### Deye Inverter Configuration

To set the baud rate on your Deye inverter:
1. Navigate to: **Advanced Settings** → **Paral. Set 3** → **Boud Rate**
2. Set the value to **9600**
3. Save the settings


**Note**: After saving, the screen will turn off and a red LED alarm will flash - this is normal behavior. Everything should return to normal after a moment.

## Controller Templates

- **Waveshare ESP32-S3-RS485-CAN**: ready-made device templates with onboard RS485 and Wi-Fi networking
- **Waveshare ESP32-S3-POE-ETH-8DI-8DO**: ready-made device templates with onboard RS485, `W5500` Ethernet, PoE support, and optional fallback to Wi-Fi by changing `network_mode`
