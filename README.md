# ae_axis
> (previously know as GenesisX) 

[![License: CERN-OHL-S-2.0](https://img.shields.io/badge/License-CERN--OHL--S--2.0-blue.svg)](LICENSE)

> **License:** CERN-OHL-S-2.0  
> **Author:** phantom-ascii (Year 10 Maker)  
> **Project Goal:** Build an open-source 2-in-1 Linux laptop completely from scratch (custom motherboard, chassis, cooling, keyboard, power system, and firmware).
---
## Overview
ae_axis is an open-source 2-in-1 Linux laptop designed from scratch. Instead of just putting existing parts together into an off-the-shelf shell, the goal is to engineer a proper, high-performance laptop. The core compute platform is powered by the LattePanda Mu Ultra (Intel Lunar Lake Core Ultra 5/7 module), offering desktop-class x86 performance, incredible integrated graphics (Intel Arc), and an integrated NPU, all while sharing the same compact 69.6 × 60 mm form factor.
> *"So many of our dreams at first seem impossible, then they seem improbable, and then, when we summon the will, they soon become inevitable."* — Christopher Reeve  
> As a maker, my guiding philosophy for GenesisX is simple: **attain the unattainable.** Building a custom 2-in-1 Linux laptop from scratch with desktop-class performance is meant to push past what feels comfortable and turn an impossible blueprint into working open-source hardware.
---
## Target Specs
* **Compute Module:** LattePanda Mu Ultra (Intel Core Ultra 5 226V / Core Ultra 7 256V, 8C/8T, up to 4.8 GHz)
* **Memory:** 16GB LPDDR5X-8533 soldered on-package (with up to 11.6GB shared VRAM allocation)
* **Display:** 13–14" 16:10 OLED touchscreen (2.5K–3K, 90–120Hz) via native eDP
* **Storage:** 2TB M.2 NVMe SSD (PCIe 4.0 lanes)
* **Form Factor:** 360° hinge (laptop, tablet, tent, and stand modes) using Framework-style hinge geometry
* **Input:** Detachable wireless keyboard and glass trackpad (Bluetooth LE + pogo pins for docking/charging)
* **Battery & Power:** ~60–70Wh battery pack with 100W USB-C PD fast charging
* **Connectivity:** Wi-Fi 6E/7 module built into the laptop body
* **I/O:** 2× USB-C, USB-A, HDMI, microSD, 3.5mm audio jack
* **Cooling:** Custom active cooling solution (copper heat pipe + slim blower fan) designed for a 37W TDP target
* **Chassis:** Aluminium / 3D-printed custom enclosure
* **Target Weight & Thickness:** ~1.3–1.5kg | ~17–20mm
---
## Why I Started This
I wanted to build something genuinely challenging rather than taking the easy route. ae_axis serves as a massive hands-on learning project to dive deep into:
* Advanced PCB design (custom 6–8 layer carrier board in KiCad)
* Mechanical CAD (Onshape / FreeCAD)
* Embedded systems, power delivery, and battery management
* Thermal engineering and custom cooling
* Firmware and Linux system integration 
One of my long-term goals is to become a Hack Club Gappie, and I'm using projects like ae_axis to build the engineering skills and execution track record to get there.
---
## Roadmap
1. **Architecture & Research:** Finalize system architecture, component research, and interface mapping.
2. **Component Selection:** Lock down display panels, power management ICs, and the LattePanda Mu Ultra platform.
3. **Bill of Materials (BOM):** Build and refine the complete component list.
4. **Schematic Design:** Capture the carrier board schematic in KiCad.
5. **PCB Layout:** Route the 6–8 layer motherboard ensuring signal integrity for PCIe 4.0 and eDP.
6. **Mechanical CAD:** Design the chassis, 360° hinge brackets, and thermal modules in Onshape.
7. **Peripherals:** Design the detachable keyboard PCB, switches, trackpad, and pogo-pin dock.
8. **Review & Verification:** Perform schematic checks (ERC) and design rule checks (DRC).
9. **Documentation & Sponsorships:** Polish open-source documentation and coordinate part sourcing/sponsorships (LattePanda, JLCPCB, NextPCB, etc.).
10. **Build & Test:** Submit designs, order parts through Hack Club, assemble, and flash firmware.
---
## Rough BOM Estimates
*Note: These are early placeholder estimates and will change as component selection and sponsorships are finalized.*

| Category | Part | Qty | Estimated Cost (USD) |
| :--- | :--- | :--- | :--- |
| **Compute** | LattePanda Mu Ultra Module (Core Ultra 5/7) | 1 | $605–$740 ($599+ base) |
| **Storage** | 2TB M.2 NVMe SSD (PCIe 4.0) | 1 | $120–$175 |
| **Display** | 13–14" 16:10 OLED touchscreen (eDP) | 1 | $200–$335 |
| **Pen** | Active pen + digitizer/controller | 1 | $65–$160 |
| **Wi-Fi / Bluetooth** | Wi-Fi 6E/7 M.2 module | 1 | $25–$55 |
| **Motherboard** | Custom 6–8 layer carrier PCB | 1 | $110–$200 |
| **Power** | USB-C PD controller & charging circuitry | 1 | $25–$55 |
| **Battery** | 60–70Wh custom battery pack | 1 | $65–$110 |
| **Keyboard** | Custom keyboard PCB, switches & keycaps | 1 | $55–$95 |
| **Trackpad** | Glass trackpad + controller | 1 | $40–$80 |
| **Wireless** | Bluetooth MCU + antenna (for detached mode) | 1 | $7–$20 |
| **Pogo connector** | Keyboard dock connection set | 1 set | $7–$20 |
| **Ports** | USB-C, USB-A, HDMI, microSD, 3.5mm | 1 set | $13–$35 |
| **Speakers** | Laptop stereo speakers | 2 | $13–$27 |
| **Cooling** | Heatsink, copper heatpipe & slim fan | 1 | $40–$80 |
| **Hinge** | 360° hinge assembly | 2 | $40–$95 |
| **Chassis** | Aluminium / 3D-printed enclosure | 1 | $110–$200 |
| **Miscellaneous** | Screws, cables, antennas, thermal pads, etc. | — | $65–$135 |

### Estimated Totals (USD)
* **Lower Estimate:** ~$1,685
* **Higher Estimate:** ~$2,625
* **Working Budget Target:** ~$2,020 *(leveraging educational sponsorships from partners like LattePanda, JLCPCB, and NextPCB)*
---
## License
Hardware designs, schematics, CAD files, and documentation are licensed under the **CERN-OHL-S-2.0** (CERN Open Hardware Licence v2 - Strongly Reciprocal).