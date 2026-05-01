<div align="center">

# ⚡ GHOST-WIRE-Multi-Protocol-IoT-Security-Diagnostic-Toolset
### Multi-Protocol IoT Security Diagnostic Toolset

![ESP32](https://img.shields.io/badge/Platform-ESP32-blue?style=for-the-badge&logo=espressif&logoColor=white)
![Protocols](https://img.shields.io/badge/Protocols-WiFi%20%7C%20BT%20%7C%20BLE%20%7C%20RF%20%7C%20NFC-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-FYP%20Active-red?style=for-the-badge)
![Contributors](https://img.shields.io/badge/Contributors-2-orange?style=for-the-badge)

> **A handheld, all-in-one ESP32-based platform for multi-protocol IoT security diagnostics — combining signal analysis, jamming, sniffing, NFC/RFID interaction, and wireless scanning in a single portable device.**

---

<!-- Replace the path below with your actual device image once uploaded -->
![Ghost Wire Device](Logos%20And%20Pics/Finished%20Product.png)

</div>

---

## 📑 Table of Contents

- [About the Project](#-about-the-project)
- [Project Pictures](#-project-pictures)
- [Hardware Components](#-hardware-components)
- [Firmwares Used](#-firmwares-used)
- [Wiring & Connections](#-wiring--connections)
- [Advantages Over Other Systems](#-advantages-over-other-systems)
- [Unique Features](#-what-makes-ghost-wire-unique)
- [Getting Started](#-getting-started)
- [Usage Scenarios](#-usage-scenarios)
- [Folder Structure](#-folder-structure)
- [Additional Improvements & Roadmap](#-additional-improvements--roadmap)
- [Credits & Acknowledgements](#-credits--acknowledgements)
- [Disclaimer](#-disclaimer)

---

## 🔍 About the Project

**Ghost Wire** is a multi-protocol IoT security diagnostic toolset designed as a Final Year Project (FYP) for comprehensive, real-world wireless security testing. Built around the powerful **ESP32** microcontroller platform, it integrates multiple wireless tools into a single handheld device.

The project builds upon established open-source firmware ecosystems — most notably **ESP32-BlueJammer** by *EmenstaNougat*, which uses an ESP32 paired with nRF24 modules to flood the 2.4 GHz spectrum (disrupting Bluetooth, BLE, Wi-Fi, RC drones, and more) — and the **CYD-ESP32 Marauder** suite for active Wi-Fi/Bluetooth scanning and wardriving.

### Core Capabilities

| Protocol | Capability |
|----------|-----------|
| **Wi-Fi (2.4GHz)** | Scanning, deauth, beacon spam, PMKID capture |
| **Bluetooth / BLE** | Device discovery, jamming, advertising |
| **RF (2.4GHz)** | Signal flooding via nRF24L01 modules |
| **NFC / RFID** | Tag reading and emulation via PN532 |
| **RC Drones** | 2.4GHz interference diagnostic |

By time-sharing a single radio across multiple protocols, Ghost Wire reduces system cost and complexity while maximizing versatility — a principle well-established in multiprotocol IoT system design.

---

## 🖼 Project Pictures

<div align="center">

| Front View | Back View |
|:-----------:|:---------:|
| ![Front](Logos%20And%20Pics/Finished%20Product.png) | ![Back](Logos%20And%20Pics/Finished%20Product%20Both%20Sides.png) |

> 📸 *Additional images of PCB layouts, antenna circuits, and module assemblies are located in the [`Logos And Pics/`](./Logos%20And%20Pics/) folder.*

</div>

Key hardware visible in the images:
- **ESP32 CYD Module** (2.8" touchscreen)
- **nRF24L01+ transceiver** with antenna
- **PN532 NFC/RFID reader**
- **Custom PCB** with organized pin layout
- **Li-Po battery** and voltage regulation circuit

---

## 🔩 Hardware Components

| Component | Purpose | Notes |
|-----------|---------|-------|
| ESP32 CYD (2.8" TFT) | Main controller + display | Cheap Yellow Display board |
| nRF24L01+ (x2) | 2.4GHz RF transceiver | PA+LNA variant recommended |
| PN532 NFC Module | NFC/RFID read & emulate | I2C or SPI |
| Li-Po Battery | Portable power | 3.7V, 1000mAh+ |
| TP4056 Module | Battery charging | USB-C variant preferred |
| MT3608 Boost Converter | 3.3V/5V regulation | Stable supply for RF modules |
| Passive Components | Decoupling caps, resistors | 10µF caps on nRF24 VCC |

---

## 💾 Firmwares Used

All firmware used in this project is open-source. Full credit and thanks go to the original authors.

### 1. 🔵 ESP32-BlueJammer
- **Author:** [EmenstaNougat](https://github.com/EmenstaNougat)
- **Repo:** [ESP32-BlueJammer](https://github.com/EmenstaNougat/ESP32-BlueJammer)
- **Function:** Floods the 2.4GHz spectrum using dual nRF24L01 modules to disrupt Bluetooth, BLE, Wi-Fi, RC drones, and other 2.4GHz communications by transmitting noise and unnecessary packets.
- **License:** See original repo.

---

### 2. 📡 CYD-ESP32 Marauder
- **Author:** [Tony7466](https://github.com/Tony7466) *(fork of original by [justcallmekoko](https://github.com/justcallmekoko))*
- **Repo:** [CYD-ESP32Marauder](https://github.com/Tony7466/CYD-ESP32Marauder)
- **Function:** Wi-Fi and Bluetooth offensive/defensive toolkit adapted for the ESP32 2.8" TFT (CYD) board. Provides Wi-Fi scanning, BLE sniffing, deauth attacks, PMKID capture, wardriving, and more — all via a touchscreen UI.
- **License:** See original repo.

---

### 3. 👾 Evil-CYD
- **Function:** Additional payload launcher customized for the CYD ESP32 board. Extends Marauder capabilities with community-contributed attack modules.
- **Source:** Community fork — link to be added.

---

### 4. 👻 Ghost_ESP_IDF
- **Function:** A custom ESP-IDF based launcher tailored for Ghost Wire hardware. Provides low-level control over RF and BLE stacks.
- **Source:** Included in [`project/`](./project/) folder.

---

### 5. 🚁 DroneB
- **Function:** Specialized binary for RC drone signal diagnostic and interference testing in the 2.4GHz band.
- **Source:** To be linked.

---

### 6. 🚀 Bruce-Launcher
- **Function:** Multipurpose firmware launcher that allows switching between payloads without re-flashing, acting as a bootloader-level menu.
- **Source:** To be linked.

> 📁 All `.bin` firmware files are stored in the [`firmware used/`](./firmware%20used/) folder with their respective flashing instructions.

---

## 🔌 Wiring & Connections

> 📐 Full schematics are available in the [`Schematic And Diagrams/`](./Schematic%20And%20Diagrams/) folder.

### nRF24L01+ → ESP32 (SPI)

| nRF24L01 Pin | ESP32 GPIO | Notes |
|:------------:|:----------:|-------|
| VCC | 3.3V | Add 10µF cap across VCC/GND |
| GND | GND | Common ground |
| CE | GPIO 4 | Chip Enable |
| CSN | GPIO 5 | Chip Select (active LOW) |
| SCK | GPIO 18 | SPI Clock |
| MOSI | GPIO 23 | Master Out |
| MISO | GPIO 19 | Master In |
| IRQ | GPIO 36 | Optional interrupt |

---

### PN532 NFC Module → ESP32 (I2C)

| PN532 Pin | ESP32 GPIO | Notes |
|:---------:|:----------:|-------|
| VCC | 3.3V | — |
| GND | GND | — |
| SDA | GPIO 21 | I2C Data |
| SCL | GPIO 22 | I2C Clock |
| IRQ | GPIO 35 | Optional |
| RSTO | GPIO 33 | Optional reset |

> **Mode Selection:** Set PN532 DIP switches to I2C mode (SW1=OFF, SW2=ON).

---

### Power Circuit

```
Li-Po (3.7V) ──► TP4056 (Charger) ──► MT3608 (Boost) ──► 3.3V Rail ──► ESP32 / nRF24 / PN532
                                                        └──► 5V Rail  ──► (if needed for peripherals)
```

> Refer to **`main-Schematic cipher tech.jpg`** and **`Wiring Prototype to make cyd.PNG`** in the Schematics folder for the complete annotated diagrams.

---

## ✅ Advantages Over Other Systems

| Feature | Ghost Wire | Typical Single-Purpose Tools |
|--------|-----------|------------------------------|
| Protocol Coverage | Wi-Fi, BT, BLE, RF, NFC | One or two at most |
| Form Factor | Handheld, battery-powered | Bulky, lab-bound |
| Cost | Low (ESP32 ecosystem) | High per tool |
| UI | Touchscreen (CYD) | CLI only |
| Extensibility | Modular firmware switching | Fixed firmware |
| Open Source | Fully community-driven | Often proprietary |

**Key highlights:**

- **All-in-One Multiprotocol** — Ghost Wire unifies jamming, scanning, and sensor tools in one device, eliminating the need for separate tools for each protocol.
- **Portable Platform** — Battery-powered and fully handheld, enabling real-world penetration testing on-site rather than in a controlled lab.
- **Cost & Complexity Reduction** — Integrating multiple radios on one board, time-sharing a single RF frontend, reduces hardware cost and simplifies configuration significantly.
- **Wide Coverage** — Supports the full range of common IoT wireless technologies, from 2.4GHz Wi-Fi/BT to NFC/RFID, in a single sweep.
- **Open-Source & Customizable** — Built entirely on community firmware, allowing rapid adaptation to new attack surfaces and protocols.

---

## 🌟 What Makes Ghost Wire Unique

1. **Integration of Diverse Tools** — Unlike typical kits, Ghost Wire merges signal jamming (2.4GHz, BLE), Wi-Fi sniffing, NFC/RFID interaction, and drone diagnostics all in one device.

2. **CYD ESP32 Platform** — Ghost Wire leverages the distinctive 2.8" touchscreen ESP32 (Cheap Yellow Display) board, which is uncommon in other security testers. The Marauder firmware adapted for this board is a key differentiator, providing an actual GUI rather than serial terminal interaction.

3. **Modular Firmware Architecture** — Via Bruce-Launcher and Ghost_ESP_IDF, the device can switch between attack modes (jammer → scanner → NFC reader) without re-flashing, behaving almost like a platform with apps.

4. **Polished Hardware Form Factor** — The custom PCB and enclosure result in a professional, finished tool — not just a prototype jumble of wires on a breadboard.

5. **Community-First Design** — Ghost Wire is built by combining multiple respected community projects (BlueJammer, Marauder, Evil-CYD, etc.) in a novel and purposeful combination, actively contributing back to open-source IoT security research.

---

## 🚀 Getting Started

### Prerequisites

- [Arduino IDE](https://www.arduino.cc/en/software) or [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/latest/)
- [esptool.py](https://github.com/espressif/esptool) for flashing `.bin` files
- USB-C cable
- ESP32 board drivers installed

### Flashing Firmware (via esptool)

```bash
# Install esptool
pip install esptool

# Flash a firmware binary (example: BlueJammer)
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash -z 0x1000 firmware_name.bin
```

> 📂 Firmware binaries are in the [`firmware used/`](./firmware%20used/) folder. Each has a corresponding README with its specific flash address.

### SD Card Setup

Some firmware variants require files on an SD card:

1. Format SD card as **FAT32**
2. Copy the contents of [`Paste As In Sd card after formatting it/`](./Paste%20As%20In%20Sd%20card%20after%20formatting%20it/) to the root of the SD card
3. Insert into the CYD ESP32 board's SD slot

---

## 📖 Usage Scenarios

**Scenario 1 — Wi-Fi Network Audit**
Boot into CYD Marauder → Scan for nearby SSIDs → Run PMKID capture → Export `.pcap` via SD card for offline analysis.

**Scenario 2 — BLE Device Discovery**
Switch to BLE scanner mode → Identify nearby IoT devices → Log MAC addresses and advertisement data.

**Scenario 3 — NFC Tag Interaction**
Load Ghost_ESP_IDF → Navigate to NFC menu → Scan an RFID/NFC tag → Read UID and memory blocks → Optionally emulate tag.

**Scenario 4 — 2.4GHz Interference Test**
Flash ESP32-BlueJammer → Enable jamming mode → Observe effect on target 2.4GHz devices (for authorized testing only).

**Scenario 5 — Drone Signal Diagnostic**
Use DroneB firmware → Scan RC frequencies → Identify active drone control channels in the area.

---

## 📁 Folder Structure

```
GHOST-WIRE/
│
├── Logos And Pics/               # Device photos, logos, branding images
│   ├── Finished Product.png
│   ├── Finished Product Both Sides.png
│   └── ...
│
├── Schematic And Diagrams/       # Wiring diagrams and PCB schematics
│   ├── main-Schematic cipher tech.jpg
│   ├── Wiring Prototype to make cyd.PNG
│   └── ...
│
├── firmware used/                # All .bin firmware files with flash instructions
│   ├── BlueJammer.bin
│   ├── CYD-Marauder.bin
│   └── ...
│
├── Paste As In Sd card after formatting it/   # SD card root contents
│
├── project/                      # Ghost_ESP_IDF source and project files
│
├── Complete Project Detail.docx  # Full written FYP documentation
├── Chat Links.docx               # Reference links and resources
└── README.md                     # This file
```

---

## 🗺 Additional Improvements & Roadmap

- [ ] Add step-by-step video tutorial for hardware assembly
- [ ] Add flowcharts and use-case diagrams for system architecture
- [ ] Write a `CONTRIBUTING.md` guide for community additions
- [ ] Add LoRa (SX1278) module support for long-range diagnostics
- [ ] Add Zigbee protocol support via CC2531 module
- [ ] Integrate GPS module for geotagged wardriving logs
- [ ] Add CI/CD workflow for automated firmware build verification
- [ ] Publish performance benchmarks and range test results
- [ ] Add safety and legal disclaimer section with per-country guidelines
- [ ] Create a dedicated project website / documentation portal

---

## 🙏 Credits & Acknowledgements

This project stands on the shoulders of the open-source community. Sincere thanks to:

| Project | Author | Contribution |
|--------|--------|-------------|
| [ESP32-BlueJammer](https://github.com/EmenstaNougat/ESP32-BlueJammer) | EmenstaNougat | Core 2.4GHz jamming firmware |
| [ESP32 Marauder](https://github.com/justcallmekoko/ESP32Marauder) | justcallmekoko | Wi-Fi/BT offensive toolkit |
| [CYD-ESP32Marauder](https://github.com/Tony7466/CYD-ESP32Marauder) | Tony7466 | CYD touchscreen Marauder fork |
| Evil-CYD | Community | CYD payload extensions |
| Bruce-Launcher | Community | Multi-firmware launcher |
| DroneB | Community | Drone RF diagnostics |

> **Contributors to this repo:**
> - [@ShellCMD101](https://github.com/ShellCMD101) — Hardware design, firmware integration, project lead
> - [@Q3hr](https://github.com/Q3hr) — Documentation, testing, firmware configuration

---

## ⚠️ Disclaimer

> **Ghost Wire is developed strictly for educational and authorized security research purposes.**
>
> Jamming, intercepting, or interfering with wireless communications may be **illegal** in your country without explicit authorization from the appropriate authorities and device owners. The authors do **not** condone or take responsibility for any misuse of this toolset.
>
> Always obtain written permission before testing on any network or device you do not own. Comply with all applicable local, national, and international laws regarding radio frequency usage and cybersecurity research.

---

<div align="center">

**Built with ❤️ as a Final Year Project**

*Ghost Wire — Securing the Invisible*

[![GitHub](https://img.shields.io/badge/GitHub-ShellCMD101-black?style=flat-square&logo=github)](https://github.com/ShellCMD101)
[![GitHub](https://img.shields.io/badge/GitHub-Q3hr-black?style=flat-square&logo=github)](https://github.com/Q3hr)

</div>
