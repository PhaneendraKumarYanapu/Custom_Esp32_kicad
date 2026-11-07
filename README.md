# Custom ESP32 IMU Development Board

A compact, custom-designed ESP32 development board featuring an integrated **MPU-6050 6-axis IMU (Accelerometer & Gyroscope)**, **USB Type-C interface**, **automatic boot/reset circuitry**, and **dual power management** supporting both USB power and an external single-cell LiPo/Li-ion battery.

---

## 🚀 Key Features

* **Microcontroller Core:** Powered by the **ESP32-WROOM-32E** module, providing robust Wi-Fi and Bluetooth connectivity alongside a dual-core Tensilica processor.
* **Integrated 6-DOF IMU:** Features onboard **MPU-6050** connected via I2C (`GPIO21` for SDA, `GPIO22` for SCL) for motion tracking, orientation, and vibration analysis.
* **USB Type-C Connectivity:** Modern Type-C interface with proper CC pull-down resistors (`5.1kΩ`) for reliable host detection and power delivery.
* **Auto-Programming & Reset Circuit:** Built around the **CP2102N** USB-to-UART bridge paired with dual NPN transistors (`Q1`, `Q2`) to allow seamless one-click code uploading without manually holding down boot buttons.
* **Dual Power Path & Battery Charging:** Integrated **MCP73831** linear charge management IC for safe 3.7V single-cell LiPo/Li-ion battery charging, with automatic power switching via Schottky diodes and an onboard 3.3V LDO regulator (**AP2112K**).

---

## 📌 Schematic Overview

The schematic is designed with modular blocks for clarity and ease of manufacturing:
1. **ESP32 Core:** MCU connections, decoupling capacitors (`10µF`, `0.1µF`), tactile Reset (`EN`) and Boot (`IO0`) push buttons.
2. **USB & UART Bridge:** Type-C receptacle, ESD protection diode array (`USBLC6-2SC6`), CP2102N bridge, and auto-reset transistor switching logic.
3. **Power Management:** JST battery header (`J2`), MCP73831 charger circuit, status LEDs, and AP2112K-3.3V step-down regulation.
4. **Sensor Subsystem:** MPU-6050 IC with mandatory I2C pull-up resistors (`4.7kΩ`) and filtering capacitors.

---

## 📋 Bill of Materials (BOM) Summary

| Category | Key Components | Qty | Primary Function |
| :--- | :--- | :---: | :--- |
| **MCU & Logic** | ESP32-WROOM-32E, Tactile Switches, Pull-up Resistors | 5 | Core processing, wireless communication, manual boot/reset controls |
| **USB & UART** | USB-C 16P Connector, CP2102N, S8050 Transistors, ESD Array | 9 | Firmware flashing, serial debugging, static discharge protection |
| **Power & Battery**| MCP73831 Charger IC, AP2112K LDO, Schottky Diodes, JST Header | 11 | Battery charging management, stable 3.3V power regulation, source switching |
| **Sensor Subsystem**| MPU-6050 (QFN-24), I2C Pull-ups, Decoupling Capacitors | 5 | 6-axis acceleration and gyro measurements over I2C |
| **Passives & Misc**| 0.1µF & 10µF Ceramic Capacitors, Status LEDs, Current Resistors | 12 | Power filtering, high-frequency noise decoupling, visual indicators |

---

## 🛠️ Pinout Mapping

| Pin / Net | ESP32 GPIO | Connected Component / Function |
| :--- | :--- | :--- |
| **SDA** | GPIO 21 | MPU-6050 SDA (Data Line) |
| **SCL** | GPIO 22 | MPU-6050 SCL (Clock Line) |
| **TXD0** | GPIO 1 | CP2102N RXD (UART Serial TX) |
| **RXD0** | GPIO 3 | CP2102N TXD (UART Serial RX) |
| **EN** | CH_PD | Reset Circuit & Tactile Button (`SW1`) |
| **IO0** | GPIO 0 | Boot Mode Select & Tactile Button (`SW2`) |
