# Installation Guide

## 🛠️ Hardware Requirements

- **ESP Development Board** (e.g., ESP32-DevKit V1) or **Waveshare ESP32-S3-POE-ETH-8DI-8DO** / **ESP32-S3-POE-ETH-8DI-8RO-C**
- **RS485 to TTL Converter** for generic ESP32 boards
- **Deye Inverter** with Modbus RTU support
- **Connecting Cables** (for RS485 communication)

## 🔌 Wiring

Connect your ESP32-DevKit V1 to the inverter's Modbus port:

```
ESP32          RS485 Converter    Inverter
GPIO17 (TX) -> DI/A+           -> A+ (Modbus)
GPIO16 (RX) -> RO/B-           -> B- (Modbus)
3.3V        -> VCC             
GND         -> GND             -> GND (Modbus)
```

**Note**: Some RS485 converters may require a flow control pin. Uncomment and configure the `flow_control_pin` in the main configuration if needed.

If you are using the **Waveshare ESP32-S3-POE-ETH-8DI-8DO** or **ESP32-S3-POE-ETH-8DI-8RO-C**, the RS485 transceiver is already onboard. Use the dedicated device templates under `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8DO/` or `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8RO-C/` and connect the inverter directly to the board's RS485 terminal.

## 🌐 Network Modes

The project now supports two mutually exclusive ESPHome network modes:

- **Wi-Fi**: set `network_mode: "wifi"` and provide `wifi_ssid` / `wifi_password`
- **Ethernet**: set `network_mode: "ethernet"` and provide `W5500` pin mappings for your board

**Important**: ESPHome cannot use `wifi:` and `ethernet:` at the same time in one build. The selected `network_mode` decides which package is compiled.

### Waveshare ESP32-S3-POE-ETH-8DI-8DO / ESP32-S3-POE-ETH-8DI-8RO-C Ethernet Pins

The ready-made Waveshare PoE Ethernet templates in this repository already use the official `W5500` mapping (identical on both boards):

- `GPIO15` → `ETH_SCLK`
- `GPIO13` → `ETH_MOSI`
- `GPIO14` → `ETH_MISO`
- `GPIO16` → `ETH_CS`
- `GPIO12` → `ETH_INT`
- `GPIO39` → `ETH_RST`

Optional Ethernet settings:

- Set `ethernet_manual_ip_enabled: true` and define `ethernet_static_ip`, `ethernet_gateway`, `ethernet_subnet`, `ethernet_dns1`, `ethernet_dns2` if you want a static IP
- Set `ethernet_use_address_enabled: true` and define `ethernet_use_address` if you want ESPHome to use a fixed upload target over Ethernet

## ⚙️ Installation

### Method 1: Home Assistant ESPHome Add-on (Recommended)

This is the easiest way to get started if you're using Home Assistant.

#### Prerequisites
- [Home Assistant](https://www.home-assistant.io/) with Add-on store access
- ESP development board or Waveshare ESP32-S3-POE-ETH-8DI-8DO / ESP32-S3-POE-ETH-8DI-8RO-C
- RS485 to TTL converter for generic ESP32 boards

#### Step 1: Install ESPHome Add-on
1. In Home Assistant, go to **Settings** → **Add-ons** → **Add-on Store**
2. Search for **"ESPHome"** and click **Install**
3. After installation, click **Start** and optionally enable **"Start on boot"**
4. Click **"Open Web UI"** to access ESPHome dashboard

#### Step 2: Add New Device
1. In ESPHome dashboard, click **"+ NEW DEVICE"**
2. Click **"CONTINUE"** on the welcome screen
3. Enter a name for your device (e.g., "Deye Inverter")
4. Select your **"ESP"** device as device type
5. Click **"NEXT"** and note down the encryption key (save it safely)
6. Click **"SKIP"** for now - we'll add the configuration manually

#### Step 3: Configure Device
1. **Create secrets file**:
   Create `secrets.yaml` in your ESPHome configuration directory:
   ```yaml
   wifi_ssid: "YourWiFiSSID"
   wifi_password: "YourWiFiPassword"
   pv_inverter_api_key: "your-32-character-api-key"
   pv_inverter_ota_password: "your-ota-password"
   pv_inverter_fallback_password: "your-fallback-password"
   ```
2. Click **"EDIT"** on your newly created device
3. **Replace the entire content** with one of the repository templates:
   - [`pv-inverter.yaml`](../pv-inverter.yaml) for a generic ESP32 + external RS485 adapter
   - `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8DO/Deye-SG0xLP1.yaml` (or the same filenames under `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8RO-C/`)
   - `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8DO/Deye-SG0xLP3.yaml` (or `...8RO-C/...`)
   - `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8DO/Deye-SG0xHP3.yaml` (or `...8RO-C/...`)
4. Set `network_mode` to `"wifi"` or `"ethernet"` in the selected YAML
5. If you use Ethernet on a non-Waveshare board, update the `ethernet_*` pin substitutions to match your `W5500` wiring
6. Click **"SAVE"** and then **"INSTALL"**

#### Step 4: Flash to ESP32
1. Connect your ESP32 to your computer via USB
2. Click **"Plug into this computer"**
3. Select the correct COM port
4. Click **"INSTALL"** and wait for the process to complete
5. Click **"STOP LOGS"** when installation is finished

#### Step 5: Connect Hardware
1. Disconnect ESP32 from computer
2. Connect the RS485 converter according to the wiring diagram above, or connect the inverter directly to the RS485 terminal when using the Waveshare board
3. Power up the ESP32 (via USB power adapter, external power supply, or PoE for the Waveshare board)
4. The device should appear in Home Assistant automatically under **Settings** → **Devices & Services** → **ESPHome**

### Method 2: ESPHome CLI

If you prefer using command line or don't have Home Assistant:

1. **Install ESPHome CLI**:
   ```bash
   pip install esphome
   ```

2. **Download Configuration**:
   ```bash
   wget https://raw.githubusercontent.com/Janso123/esphome-deye-inverter/main/pv-inverter.yaml
   ```
   Or start from one of the device templates under `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8DO/` or `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8RO-C/` if you are using the Waveshare industrial board.

3. **Create secrets.yaml**:
   ```yaml
   wifi_ssid: "YourWiFiSSID"
   wifi_password: "YourWiFiPassword"
   pv_inverter_api_key: "your-32-character-api-key"
   pv_inverter_ota_password: "your-ota-password"
   pv_inverter_fallback_password: "your-fallback-password"
   ```
   For Ethernet-first Waveshare templates, Wi-Fi credentials can stay empty unless you change `network_mode` back to `"wifi"`.

4. **Flash to ESP**:
   ```bash
   esphome run pv-inverter.yaml
   ```
