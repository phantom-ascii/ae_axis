(revise oct 26 2026)

# Project Blueprint: `ae_axis`

**12.2" High-Performance Open-Source Linux Tablet**

---

## 1. System Overview & Core Goals

* **Project Name:** `ae_axis`
* **Repository & License:** Open-source release under the **CERN-OHL-S-2.0** (Strongly Reciprocal) license.
* **Form Factor:** 12.2-inch rigid tablet chassis with an integrated fold-out friction kickstand and a detachable wireless BLE mechanical keyboard module.
* **Primary Objective:** Design a fully functional, high-performance x86-64 portable Linux workstation using off-the-shelf display components and a modular compute core, targeted for execution under a 1-year timeline within the Hack Club ecosystem.
* **Key Risk Profile:** **One-Shot Fabrication Constraint.** Funding is granted post-design approval. No physical rapid-prototyping budget is allocated prior to ordering final hardware. All mechanical clearances, high-speed signal paths, thermal paths, and power-sequencing rules must be verified through CAD and pre-routing schematic audits.

---

## 2. Hardware Architecture & Key Components

### 2.1 Main Compute Engine

* **Compute Module:** LattePanda Mu Ultra (Intel Core Ultra 5 226V "Lunar Lake", 16GB LPDDR5x in-package RAM).
* **Host Edge Interface:** Standard 260-pin DDR4 SODIMM edge connector (TE Connectivity 2309411-1 equivalent footprint, pinout customized per LattePanda Mu Ultra standard).
* **Storage Interface:** 1x M.2 2280 Key-M slot operating over PCIe 4.0 $\times 4$ (required for primary OS boot medium).
* **Wireless Connectivity:** 1x M.2 2230 Key-E slot for Wi-Fi 7 / Bluetooth 5.4 (Intel BE200 via PCIe/USB 2.0).

### 2.2 Display Subsystem

* **Display Panel:** Framework Laptop 12 12.2-inch display assembly (WUXGA touch display panel).
* **Video Interface:** 4-lane native embedded DisplayPort (eDP) routing from the 260-pin host edge connector to a fine-pitch FPC display connector.
* **Touch Controller:** Integrated USB 2.0 capacitive touch controller routed over internal differential USB 2.0 lines to the host module.

### 2.3 Power Delivery & Battery Management System (BMS)

* **USB-C Power Delivery Controller:** Texas Instruments **TPS65987D** (USB PD 3.0 controller handling dual-role power contracts up to 20V @ 5A / 100W).
* **Buck-Boost Battery Charger:** Texas Instruments **BQ25792** (I2C-controlled buck-boost NVDC charger supporting 2S-4S LiPo configurations).
* **Fuel Gauge IC:** Texas Instruments **BQ27Z561** (Impedance Track™ fuel gauge connected over host I2C).
* **Battery Pack Configuration:** Internal 3S1P or 3S2P custom flat LiPo pack (40Wh–50Wh total capacity) delivering system voltage ($V_{SYS}$) directly to the main power bus.
* **Power Output Bus:** Main system rail ($V_{CC\_IN}$) operating dynamically between 12V and 20V.

### 2.4 Wireless Detachable Keyboard Peripheral

* **Microcontroller:** Nordic Semiconductor **nRF52840** (ARM Cortex-M4F with onboard 2.4GHz BLE radio).
* **Key Switches:** Low-profile mechanical switches (Cherry MX Ultra Low Profile).
* **Pointing Device:** Precision glass trackpad connected via I2C to the nRF52840 MCU.
* **Charging & Docking:** 2-pin magnetic pogo-pin dock supplying **5V VBUS power only** for charging an onboard 1200mAh LiPo cell (no high-speed or data signals cross the physical dock; data is 100% BLE).

---

## 3. PCB & Mechanical Architecture (4-Board Topology)

To optimize weight distribution and thermal management, the computing hardware is split across four distinct boards housed within the main tablet chassis (behind the screen):

```
+-----------------------------------------------------------------------------------+
|                         TABLET MAIN CHASSIS (RIGID LID)                           |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  |             FRAMEWORK 12 DISPLAY PANEL (12.2" WUXGA Touchscreen)            |  |
|  +-----------------------------------------------------------------------------+  |
|                                       || Native 4-Lane eDP                        |
|                                       || + USB 2.0 Touch                          |
|  +------------------+         +-------------------+         +------------------+  |
|  |  LEFT I/O BOARD  |=========|   MAIN CARRIER    |=========|  RIGHT I/O BOARD |  |
|  | - USB-C PD Port  |  FPC    | - LattePanda Mu   |   FPC   | - USB-A / Audio  |  |
|  | - TPS65987D Ctrl |         | - 2TB NVMe SSD    |         | - MicroSD Reader |  |
|  +------------------+         | - BE200 Wi-Fi 7   |         +------------------+  |
|           ||                  +-------------------+                            |
|           || Power Rails                ||                                     |
|           ||                            || Telemetry (I2C)                     |
|  +-----------------------------------------------------------------------------+  |
|  |                            BMS DAUGHTERBOARD                                |  |
|  |        TI BQ25792 Buck-Boost + TI BQ27Z561 Gauge + 40-50Wh LiPo             |  |
|  +-----------------------------------------------------------------------------+  |
|                                       ||                                          |
|                          (2-Pin Magnetic Pogo-Pin Dock)                          |
+-----------------------------------------------------------------------------------+
                                        || 5V VBUS + GND Charging Only
                                        ||
+-----------------------------------------------------------------------------------+
|                        DETACHABLE BLE KEYBOARD & TRACKPAD                         |
|   Cherry MX ULP Switches | nRF52840 BLE MCU | Glass Trackpad | 1200mAh LiPo Cell  |
+-----------------------------------------------------------------------------------+

```

1. **Main Carrier Board (Center):** Houses the 260-pin SODIMM connector for the LattePanda Mu Ultra module, M.2 NVMe slot, M.2 Wi-Fi slot, main system rail regulators ($5\text{V}$, $3.3\text{V}$ buck converters), display FPC header, and internal interconnect headers.
2. **Left I/O Daughterboard:** Houses primary USB-C PD input connector, TPS65987D PD logic, and TVS protection diode arrays. Connected to the Main Carrier via high-current FPC.
3. **Right I/O Daughterboard:** Houses user peripheral ports (USB 3.2 Gen 2 Type-A, 3.5mm TRRS audio jack, MicroSD card reader). Connected via high-speed FPC.
4. **BMS Daughterboard:** Houses the BQ25792 charger, BQ27Z561 fuel gauge, battery protection MOSFETs, and battery pack wire-to-board harness.

---

## 4. Design & Execution Rules

### 4.1 Electrical & Schematic Rules

* **Hierarchical Capture:** Schematics organized across 4 primary sub-sheets (`01_SoM_INTERFACE`, `02_DISPLAY_eDP`, `03_POWER_PD`, `04_EXPANSION_STORAGE`).
* **$0\ \Omega$ Bring-up Jumpers:** $0\ \Omega$ isolation resistors placed on $V_{CC\_IN}$, $+5\text{V}$, and $+3.3\text{V}$ output lines to isolate individual rails during initial power-on testing.
* **Decoupling Placement:** Decoupling capacitors must be placed immediately adjacent to respective IC power pins in the schematic and layout phase ($<10\text{mm}$ trace distance).
* **Test Points:** Dedicated surface-mount test pads for `GND`, `I2C_SDA`, `I2C_SCL`, `eDP_HPD`, `PWRBTN#`, and primary power supply rails.

### 4.2 PCB Layout & Stackup Targets

* **Layer Count:** 6-layer stackup configured in KiCad 8.
* **Controlled Impedance Classes:**
* **$85\ \Omega$ Differential:** 4-lane eDP video bus and USB 3.2 data lines.
* **$100\ \Omega$ Differential:** PCIe Gen 4 lanes (NVMe SSD).
* **$50\ \Omega$ Single-Ended:** Standard high-speed signals and clock lines.



### 4.3 Mechanical Envelope (Onshape Targets)

* **Chassis Outer Bounding Box:** Maximum dimensions $275\text{ mm (Width)} \times 200\text{ mm (Height)} \times 14\text{ mm (Thickness)}$.
* **Structural Material:** Machined aluminum backplate or high-temp PETG/ABS-CF 3D-printed outer shell with brass heat-set inserts ($M2.5$ and $M3$) for all structural mounting points.
* **Kickstand Mechanism:** Dual Southco E6 series or Microsoft Surface-style constant-torque positioning friction hinges (rated $\approx 1.5 - 2.5\text{ N}\cdot\text{m}$ combined torque) mounted flat to the rear chassis.

---

## 5. Development Toolchain

* **ECAD:** KiCad 8 (Schematic Capture, 6-layer PCB Layout, DRC verification).
* **MCAD:** Onshape (3D Parametric Mechanical Modeling, STEP assembly checks).
* **Target Operating System:** Ubuntu 24.04 LTS / Mainline Linux.
