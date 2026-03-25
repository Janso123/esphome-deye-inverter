# Configuration

## 🔧 Configuration Options

### Main Configuration (`pv-inverter.yaml`)

| Parameter | Description | Default | Required |
|-----------|-------------|---------|----------|
| `name` | Device name in ESPHome | depends on inverter type | No |
| `friendly_name` | Friendly device name | depends on inverter type | No |
| `device_description` | Device description | depends on inverter type | No |
| `modbus_controller_id` | Modbus controller ID | depends on inverter type | No |
| `modbus_inverter_address` | Modbus address of your inverter | `0x01` | No |
| `baud_rate` | Baud rate for Modbus communication | `9600` | No |
| `update_interval` | How often sensor values are updated from inverter | 5s | No |
| `network_mode` | Selects the compiled network stack: `wifi` or `ethernet` | `wifi` | No |

### Network Configuration

| Parameter | Description | Default | Required |
|-----------|-------------|---------|----------|
| `wifi_ssid` | Wi-Fi SSID used when `network_mode: "wifi"` | none | Wi-Fi only |
| `wifi_password` | Wi-Fi password used when `network_mode: "wifi"` | none | Wi-Fi only |
| `fallback_password` | Password for the fallback AP in Wi-Fi mode | none | Wi-Fi only |
| `ethernet_clk_pin` | `W5500` SPI clock pin | `GPIO15` | Ethernet only |
| `ethernet_mosi_pin` | `W5500` SPI MOSI pin | `GPIO13` | Ethernet only |
| `ethernet_miso_pin` | `W5500` SPI MISO pin | `GPIO14` | Ethernet only |
| `ethernet_cs_pin` | `W5500` chip select pin | `GPIO16` | Ethernet only |
| `ethernet_interrupt_pin` | `W5500` interrupt pin | `GPIO12` | Ethernet only |
| `ethernet_reset_pin` | `W5500` reset pin | `GPIO39` | Ethernet only |
| `ethernet_manual_ip_enabled` | Enables the static IP package for Ethernet builds | `false` | No |
| `ethernet_static_ip` | Static IP used when `ethernet_manual_ip_enabled: true` | `192.168.1.50` | Static IP only |
| `ethernet_gateway` | Gateway used when `ethernet_manual_ip_enabled: true` | `192.168.1.1` | Static IP only |
| `ethernet_subnet` | Subnet used when `ethernet_manual_ip_enabled: true` | `255.255.255.0` | Static IP only |
| `ethernet_dns1` | Primary DNS used when `ethernet_manual_ip_enabled: true` | `1.1.1.1` | Static IP only |
| `ethernet_dns2` | Secondary DNS used when `ethernet_manual_ip_enabled: true` | `8.8.8.8` | Static IP only |
| `ethernet_use_address_enabled` | Enables a fixed ESPHome upload target for Ethernet builds | `false` | No |
| `ethernet_use_address` | Address used when `ethernet_use_address_enabled: true` | `192.168.1.50` | Optional |

**Important**: ESPHome can compile either `wifi:` or `ethernet:` in a single build, but not both at the same time.

### Inverter Configuration

| Parameter | Description | Default | Required | Supported Inverters |
|-----------|-------------|---------|----------|---------------------|
| `safe_mode_delay` | Delay before activating safe mode when disconnected | `600s` | No | All (1P/3P) |
| `default_maximum_battery_charge_current` | Maximum battery charge current in safe mode | `140` | No | All (1P/3P) |
| `default_max_sell_power` | Maximum power export in safe mode | `12000` | No | All (1P/3P) |
| `default_system_work_mode` | System work mode in safe mode | `"Zero Export To Load"` | No | All (1P/3P) |
| `default_solar_sell` | Solar selling state in safe mode | `"on"` | No | All (1P/3P) |
| `default_force_off_grid` | Force Off Grid switch state in safe mode | `"off"` | No | 3P only (SG0XLP3, SG0XHP3) |
| `enable_sync_time` | Enable automatic time synchronization with Home Assistant | `false` | No | 3P only (SG0XLP3, SG0XHP3) |

### Default Hardware Configuration

- **Generic ESP32 + RS485 adapter**: GPIO17 (TX), GPIO16 (RX), optional flow control on GPIO4
- **Waveshare ESP32-S3-POE-ETH-8DI-8DO**: GPIO17 (TX), GPIO18 (RX), flow control on GPIO21
- **Default Ethernet pin mapping for Waveshare `W5500`**: GPIO15 / GPIO13 / GPIO14 / GPIO16 / GPIO12 / GPIO39
- **Baud Rate**: 9600
- **Board**: ESP32-DevKit v1 by default, configurable per device template

## 🔄 Updates

The configuration automatically updates packages from this repository every 12 hours. To force an update:
1. In ESPHome dashboard, click "CLEAN BUILD FILES" on your device
2. Click "INSTALL" to rebuild with latest packages
