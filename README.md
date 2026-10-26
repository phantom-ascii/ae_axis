# ae_axis

  <a href="https://creativecommons.org/licenses/by-nc/4.0/">
    <img src="https://licensebuttons.net/l/by-nc/4.0/88x31.png" alt="Creative Commons Attribution-NonCommercial 4.0 International License"></a> <a href="https://hackclub.com">
    <img alt="Funded by Hack Club" src="https://img.shields.io/badge/Hack_Club-Funded-ec3750?style=for-the-badge&logo=hackclub&logoColor=ec3750"></img>
  </a>
  
[![License: CERN-OHL-S-2.0](https://img.shields.io/badge/License-CERN--OHL--S--2.0-blue.svg)](LICENSE)

> **License:** CERN-OHL-S-2.0  

> **Author:** phantom-ascii (15 year old Maker)  

> **Project Goal:** Design and build a fully open-source 12.2" 2-in-1 Linux laptop completely from scratch — custom carrier boards, modular chassis, power management, custom cooling, and a detached wireless keyboard.
---

## What is ae_axis?
Most custom laptop projects either re-shell an existing donor motherboard or stack off-the-shelf maker boards into a bulky, 3D-printed brick. **ae_axis** is an attempt to build a real, high-performance 2-in-1 machine from the ground up.
At its core sits the **LattePanda Mu Ultra** (Intel Lunar Lake Core Ultra 5 226V / Core Ultra 7 256V). It packs 8 cores, Intel Arc graphics, and a dedicated NPU into a credit-card-sized 69.6 × 60 mm compute module. The goal is to build an ultrabook-class Linux convertible around this module that feels great to use daily.

> *"So many of our dreams at first seem impossible, then they seem improbable, and then, when we summon the will, they soon become inevitable."* — Christopher Reeve 

As a high school maker, my guiding philosophy for ae_axis is simple: **attain the unattainable.** Building a custom 2-in-1 Linux laptop from scratch with desktop-class performance is meant to push past what feels comfortable and turn an impossible blueprint into working open-source hardware.
---

## Target Specs
* **Compute Module:** LattePanda Mu Ultra (Intel Core Ultra 5 226V / Core Ultra 7 256V, 8C/8T, up to 4.8 GHz)
* **Memory:** 16GB LPDDR5X-8533 soldered on-package (with up to 11.6GB shared VRAM allocation)
* **Display & Hinge:** 12.2" WUXGA (1920 × 1200) 16:10 touchscreen (Framework 12 OEM panel via native eDP) utilizing Framework 12 360° hinge geometry
* **Storage:** 2TB M.2 NVMe SSD (PCIe 4.0 lanes)
* **Keyboard & Trackpad:** Detachable magnetic wireless keyboard with Cherry MX Ultra-Low Profile (3.5mm) mechanical switches, glass trackpad, and nRF52840 BLE controller (charges via 2-pin pogo pads when docked)
* **Battery & Power:** ~40–50Wh custom LiPo battery pack with 100W USB-C PD fast charging (TI TPS65987D PD + BQ25792 buck-boost charger)
* **Connectivity:** Intel Wi-Fi 7 BE200 M.2 module (Wi-Fi 7 + Bluetooth 5.4)
* **Motherboard Layout:** 4-board split architecture (Main, Left I/O, Right I/O, BMS) on a custom 6-layer PCB stackup
* **Cooling:** Custom active cooling solution (copper heat spreader + slim blower fan) tuned for a ~37W TDP target
* **Chassis:** Custom aluminum frame / 3D-printed enclosure with brass heat-set inserts
* **Target Weight & Thickness:** ~1.2–1.4kg | ~14–18mm
---

## Why I Started This
I wanted to build something genuinely challenging rather than taking the easy route. ae_axis serves as a massive hands-on learning project to dive deep into:
* **Advanced PCB Design:** Routing eDP differential pairs, PCIe Gen 4, and USB 3.2 across a custom 6-layer carrier board in KiCad.
* **Power Delivery:** Designing USB-C Power Delivery negotiation, buck-boost charging, and I2C fuel gauge telemetry.
* **Mechanical CAD:** Modeling thin-wall enclosures, display brackets, and thermal clearance in Onshape.
* **Embedded Firmware:** Writing custom BLE keyboard code on Nordic nRF chips and tuning Linux power states.
One of my long-term goals is to become a **Hack Club Gappie**, and I'm using projects like ae_axis to build the real-world hardware execution skills to get there.
---

## Roadmap
1. **Architecture & Research:** Finalize system architecture, component research, split 4-board layout, and interface mapping.
2. **Component Selection:** Lock down display panels, power management ICs, Framework hinge integration, and the LattePanda Mu Ultra platform.
3. **Bill of Materials (BOM):** Build and refine the complete component list.
4. **Schematic Design:** Capture the carrier board and daughterboard schematics in KiCad.
5. **PCB Layout:** Route the 6-layer motherboard ensuring signal integrity for PCIe 4.0 and eDP.
6. **Mechanical CAD:** Design the chassis, Framework hinge mounts, and thermal modules in Onshape.
7. **Peripherals:** Design the detachable keyboard PCB, Cherry MX ULP switches, glass trackpad, and pogo-pin dock.
8. **Review & Verification:** Perform schematic checks (ERC) and design rule checks (DRC).
9. **Documentation & Sponsorships:** Polish open-source documentation and coordinate part sourcing/sponsorships (LattePanda, JLCPCB, NextPCB, Hack Club).
10. **Build & Test:** Submit designs, order parts, assemble, and flash firmware.
---
## Bill of Materials (BOM) Estimates
*Note: These are early planning estimates and will change as component selection and sponsorships are finalized.*

| Category | Part | Qty | Estimated Cost (USD) |
| :--- | :--- | :--- | :--- |
| **Compute** | LattePanda Mu Ultra Module (Core Ultra 5/7) | 1 | $605–$740 |
| **Storage** | 2TB M.2 NVMe SSD (PCIe 4.0) | 1 | $120–$175 |
| **Display & Hinge** | Framework 12 12.2" Touch Display + 360° Hinge Kit | 1 | $180–$250 |
| **Wi-Fi / Bluetooth** | Intel Wi-Fi 7 BE200 M.2 Module | 1 | $25–$45 |
| **Motherboard** | Custom 6-layer Carrier Board PCBs | 1 set | $90–$160 |
| **Power Delivery** | TPS65987D PD + BQ25792 Charger & Fuel Gauge | 1 set | $25–$45 |
| **Battery** | 40–50Wh custom LiPo pack | 1 | $50–$85 |
| **Keyboard** | Cherry MX ULP Switches, custom PCB & keycaps | 1 | $55–$95 |
| **Trackpad & Wireless** | Glass trackpad module + nRF52840 BLE MCU | 1 set | $45–$80 |
| **Ports & Dock** | USB-C/A connectors, audio jack, Pogo pins | 1 set | $15–$30 |
| **Cooling** | Custom copper heat spreader + slim blower fan | 1 | $35–$60 |
| **Chassis** | Aluminum / 3D-printed enclosure parts | 1 | $80–$150 |
| **Hardware / Misc** | Screws, brass inserts, FPC cables, antennas | — | $45–$85 |

### Estimated Totals (USD)
* **Working Budget Target:** ~$1,400–$1,800 *(leveraging educational sponsorships from partners like LattePanda, JLCPCB, NextPCB, and Hack Club)*
---

## License
Hardware designs, schematics, CAD files, and documentation are licensed under the **CERN-OHL-S-2.0** (CERN Open Hardware Licence v2 - Strongly Reciprocal).
