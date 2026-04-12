# ESPHome Deye Inverter

<!--
Copyright 2025 Lewa-Reka <lewareka.yt@gmail.com> (original project)
Modifications and this fork: Copyright 2026 Janso123

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

![Maintenance](https://img.shields.io/maintenance/yes/2026?style=for-the-badge)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/Janso123/esphome-deye-inverter/build-ci.yaml?style=for-the-badge)
![GitHub License](https://img.shields.io/github/license/Janso123/esphome-deye-inverter?style=for-the-badge)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/Janso123/esphome-deye-inverter?style=for-the-badge)

An ESPHome-based solution for monitoring and controlling Deye photovoltaic inverters via Modbus RTU communication. This project provides comprehensive integration with Home Assistant, enabling real-time monitoring and control of solar power systems.

The project supports both **Wi-Fi** and **W5500 Ethernet** builds through a selectable `network_mode`, and includes ready-made templates for **Waveshare** industrial boards (including **ESP32-S3-POE-ETH-8DI-8DO** and **ESP32-S3-POE-ETH-8DI-8RO-C**; same Ethernet and RS485 pinout, the latter uses relay outputs instead of transistor outputs).

Installation & Presentation (upstream): https://youtu.be/iJjsA_MzmnE [PL]

## About this fork (Janso123)

This repository is a **fork** of [Lewa-Reka/esphome-deye-inverter](https://github.com/Lewa-Reka/esphome-deye-inverter). The integration logic and inverter packages still follow upstream; this fork adds **maintainer-specific configuration** and keeps the same **Apache-2.0** license.

**Why URLs point to `Janso123/esphome-deye-inverter` instead of Lewa-Reka**

- **ESPHome package imports** (`packages:` with `url:` / `github://` / `dashboard_import`) must match the repository that actually holds **your** `main` branch and tags. When you compile in the Home Assistant ESPHome add-on, ESPHome fetches `pv_inverter` (and related paths) from that URL. Pointing to your fork avoids silently building against upstream while you maintain local changes, and keeps `ref: main` aligned with what you push.
- **GitHub Pages / HTTP OTA** (`update.source` manifest URLs under `*.github.io`) must match the account that **publishes** firmware. Upstream's Pages URL would not serve binaries from your Actions/Pages pipeline, so those links were switched to **`https://janso123.github.io/esphome-deye-inverter/...`** for consistency. They only work after you enable Pages and publish builds (see `.github/workflows/build-and-publish.yaml`).

**Notable changes in this fork**

- Device templates for **Waveshare ESP32-S3-POE-ETH-8DI-8RO-C** under `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8RO-C/` (relay output variant; same W5500 / RS485 pins as the 8DI-8DO board for Deye communication).
- CI test configs for that board under `tests/`.
- Repository-wide link updates for packages, factory/dashboard import, and documentation examples so they target **this** fork and your Pages hostname.

For improvements that belong in the original project, consider opening an issue or PR on [Lewa-Reka/esphome-deye-inverter](https://github.com/Lewa-Reka/esphome-deye-inverter).

## Documentation

- **[Supported Devices](docs/SUPPORTED_DEVICES.md)**: List of supported inverters and specific configurations.
- **[Features & Capabilities](docs/FEATURES.md)**: Detailed overview of features, safety mechanisms, and monitoring capabilities.
- **[Installation Guide](docs/INSTALLATION.md)**: Hardware requirements, wiring diagrams, and step-by-step installation instructions.
- **[Configuration](docs/CONFIGURATION.md)**: Configuration options, parameters, and update instructions.
- **Waveshare board templates**: `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8DO/` and `devices/Waveshare-ESP32-S3-POE-ETH-8DI-8RO-C/` for Ethernet-first industrial deployments.
- **[Troubleshooting](docs/TROUBLESHOOTING.md)**: Common issues and solutions.
- **[Contributing](docs/CONTRIBUTING.md)**: Guidelines for contributing to the project.

## Home Assistant Visualization Examples

The integration works seamlessly with the **[Sunsynk Power Flow Card](https://github.com/slipx06/sunsynk-power-flow-card)** by [slipx06](https://github.com/slipx06), providing an elegant visualization of energy flow in your photovoltaic system. Below are example card configurations available for 3-phase inverters:

![Sunsynk Power Flow Card Examples](docs/examples/img/card_3p_all.png)

### Card Styles:

- **[Example 1: Full Style (Modern)](docs/examples/SUNSYNK_POWER_FLOW_CARD.md#example-1-full-style-modern---3-phase)** - Modern style with large fonts, ideal for standard dashboard views
- **[Example 2: Compact Style](docs/examples/SUNSYNK_POWER_FLOW_CARD.md#example-2-compact-style---3-phase)** - Compact style that saves space, featuring a Deye-style inverter icon
- **[Example 3: Wide Style with Dual Battery](docs/examples/SUNSYNK_POWER_FLOW_CARD.md#example-3-wide-style-with-dual-battery---3-phase)** - Wide style with dual battery support, perfect for wider dashboard layouts (tablets, desktops)

Detailed installation instructions and full configurations can be found in the [examples documentation](docs/examples/SUNSYNK_POWER_FLOW_CARD.md).

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

### Copyright Notice

```
Copyright 2025 Lewa-Reka <lewareka.yt@gmail.com> (original project)
Modifications and this fork: Copyright 2026 Janso123

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

### Third-Party Components

This project uses ESPHome and related components. Please refer to the [NOTICE](NOTICE) file for additional license information.

## Acknowledgments

- **[Lewa-Reka / esphome-deye-inverter](https://github.com/Lewa-Reka/esphome-deye-inverter)** — original project and inverter integration
- [Solarman Stick Logger by David Rapan](https://github.com/davidrapan/ha-solarman) and [pilipphenkel](https://github.com/philipphenkel/esphome-config) for inspirations
- [Sunsynk Power Flow Card by slipx06](https://github.com/slipx06/sunsynk-power-flow-card) for the excellent visualization card
- [ESPHome Team](https://esphome.io/) for the excellent home automation platform
- [Home Assistant Community](https://community.home-assistant.io/) for continuous support and inspiration
- All contributors and testers who helped improve this integration

## Support

- **This fork**: [Issues](https://github.com/Janso123/esphome-deye-inverter/issues) and [Discussions](https://github.com/Janso123/esphome-deye-inverter/discussions)
- **Upstream project**: [Lewa-Reka/esphome-deye-inverter](https://github.com/Lewa-Reka/esphome-deye-inverter)
- **Home Assistant Community**: [ESPHome section](https://community.home-assistant.io/c/esphome/) for general ESPHome help

## Related Projects

- [HA-Solarman](https://github.com/davidrapan/ha-solarman) - Alternative WiFi stick integration
- [Sunsynk Power Flow Card](https://github.com/slipx06/sunsynk-power-flow-card) - Home Assistant card for visualizing solar power flow
- [ESPHome Official Docs](https://esphome.io/) - ESPHome documentation

---

**Disclaimer**: This project is not officially affiliated with Deye. Use at your own risk and ensure compliance with local electrical codes and regulations. Always consult with a qualified electrician for installation and safety verification. The authors are not responsible for any damage to equipment or injury resulting from the use of this software.
