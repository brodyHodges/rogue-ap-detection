## Verified Hardware and Setup Status

Last updated: 2026-10-31

### Edge computer

- Device: Raspberry Pi 5
- Memory: 16 GB
- Architecture: aarch64
- Operating system: Ubuntu Server 24.04.5 LTS
- Kernel: 6.8.0-1065-raspi
- Wireless interface: `wlan0`
- Current wireless mode: managed
- Monitor-mode status: monitor mode is not advertised by the currently loaded Wi-Fi driver. The Pi's built-in wireless interface is therefore not being used as the monitor sensor.

### ESP32 sensor

- Chip: ESP32-D0WD-V3
- Chip revision: v3.1
- Identification method: `esptool` v5.6.0, using `py -m esptool --port COM3 chip-id`
- Exact development-board and module model: unknown
- A prior WROOM-32-family identification is unconfirmed; do not treat it as established.
- Radio scope: 2.4 GHz Wi-Fi
- Planned role: passive sensor for collecting relevant 802.11 management-frame information and RSSI, then sending records to the Raspberry Pi over USB serial.
- Promiscuous-mode capture and serial data transfer still need to be validated with project firmware.

### Development computer and tools

- Development computer: Windows laptop
- VS Code extension present: PlatformIO
- PlatformIO framework and project configuration: not yet confirmed
- ESP32 serial port: `COM3` worked during the chip-identification session. This is a Windows port assignment and may change if the board or USB port changes.

### Other hardware findings

- RTL-SDR Blog V4: not suitable for capturing Wi-Fi frames; its tuning range does not reach 2.4 GHz.

### Current implementation status

- Raspberry Pi SSH connectivity has been established.
- The ESP32 chip has been identified successfully.
- ESP32 monitoring firmware, serial logging, the analysis pipeline, and the detection rules have not yet been implemented or tested.
