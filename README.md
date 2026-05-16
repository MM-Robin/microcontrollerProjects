<div align="center">

# Microcontroller Projects — TM4C1294

**Embedded C · GPIO · UART · ADC · PWM · Interrupts**

[![C](https://img.shields.io/badge/Language-C-00599C?style=flat-square&logo=c&logoColor=white)](https://en.wikipedia.org/wiki/C_(programming_language))
[![TM4C1294](https://img.shields.io/badge/MCU-TM4C1294NCPDT-CC0000?style=flat-square)](https://www.ti.com/product/TM4C1294NCPDT)
[![TI](https://img.shields.io/badge/Tool-TI_Code_Composer-CC0000?style=flat-square)](https://www.ti.com/tool/CCSTUDIO)
[![HAW Hamburg](https://img.shields.io/badge/HAW-Hamburg-004F9F?style=flat-square)]()

</div>

---

## Overview

This repository contains embedded C projects developed for the **Texas Instruments TM4C1294NCPDT** microcontroller (ARM Cortex-M4F) as part of the **Microcontroller Lab** course at **HAW Hamburg**. Each project demonstrates hands-on use of core MCU peripherals — ADC, PWM, UART, GPIO — with interrupt-driven design patterns.

---

## Repository Structure

```
microcontrollerProjects/
│
├── LED_Pendulum_UART_Display/          # Project 1 — UART-controlled LED pendulum display
├── LED_Dimmer_XY_Joystick/             # Project 2 — PWM LED dimmer via analog XY joystick
├── Digital_Multimeter_WeightedConversion/  # Project 3 — Digital voltmeter using weighted conversion
│
└── README.md
```

---

## Projects

### Project 1 — LED Pendulum UART Display

**Folder:** `LED_Pendulum_UART_Display/`

Displays characters typed on a PC onto a swinging LED pendulum in real time via UART. The microcontroller receives ASCII characters, maps them to a bitmap font, and renders them column by column as the pendulum swings.

| Feature | Detail |
|---|---|
| **Communication** | UART0 — PC to MCU character streaming |
| **Display** | 10-character string rendered on LED pendulum (5×5 bitmap font) |
| **Interrupt sources** | UART RX interrupt + GPIO button interrupt |
| **Display modes** | Toggle between red-on-black and black-on-red via push button |
| **Supported chars** | A–Z, 0–9 (ASCII 0x41–0x5A) |

**Key files:**
- `main.c` — main loop and peripheral configuration
- `int_handler.c / .h` — UART and GPIO interrupt handlers
- `int_handler_invert.c` — inverted display mode handler
- `5x5_font.h` — bitmap character definitions
- `tm4c1294ncpdt_startup_ccs.c` — CCS startup file

---

### Project 2 — PWM LED Dimmer via Analog XY Joystick

**Folder:** `LED_Dimmer_XY_Joystick/`

Controls LED brightness using a 12-bit ADC reading from an analog XY joystick. PWM duty cycle (5%–95%) is adjusted based on joystick position, with a button to toggle between full and minimum brightness.

| Feature | Detail |
|---|---|
| **ADC** | Internal 12-bit ADC (Sequence 0) reading joystick X-axis |
| **PWM** | 1 kHz square wave via Timer2, duty cycle 5%–95% |
| **Joystick behavior** | Right → increase brightness · Left → decrease · Center → hold |
| **Button behavior** | Toggle full ↔ minimum brightness |
| **Interrupt sources** | Timer interrupt for PWM · GPIO for button |

**Key files:**
- `main.c` — ADC polling, PWM control logic
- `int_portM_handler.c / .h` — GPIO port M interrupt handler

---

### Project 3 — Digital Voltmeter via Weighted Conversion

**Folder:** `Digital_Multimeter_WeightedConversion/`

Measures an external analog voltage using the **Weighted Conversion Method** with an external DAC and the TM4C1294 ADC. The result is displayed as a 4-digit BCD value (e.g. `12.34`) on a BCD display.

| Feature | Detail |
|---|---|
| **Method** | Weighted (successive approximation) conversion |
| **Interface** | External DAC + TM4C1294 ADC |
| **Output** | 4-digit BCD display (integer + decimal parts) |
| **LSB resolution** | ~0.0195 V |
| **Build system** | CMake (CLion / GCC toolchain) |

**Key files:**
- `main.c` — conversion logic, BCD display output
- `CMakeLists.txt` — build configuration

---

## Hardware Platform

| Property | Value |
|---|---|
| **MCU** | Texas Instruments TM4C1294NCPDT |
| **Architecture** | ARM Cortex-M4F @ 120 MHz |
| **Flash / RAM** | 1 MB / 256 KB |
| **Peripherals used** | GPIO, ADC, PWM (Timer), UART0 |
| **IDE** | TI Code Composer Studio (CCS) / CLion |

---

## Getting Started

### Prerequisites

- [TI Code Composer Studio](https://www.ti.com/tool/CCSTUDIO) or CLion with GCC ARM toolchain
- TM4C1294 LaunchPad or compatible evaluation board
- TivaWare peripheral driver library

### Build & Flash (CCS)

1. Import the project folder into Code Composer Studio
2. Select the correct target device: `TM4C1294NCPDT`
3. Build → Flash via JTAG/XDS110 debugger
4. Open a serial terminal (115200 baud) for UART projects

### Build (CMake — Project 3)

```bash
cd Digital_Multimeter_WeightedConversion
mkdir build && cd build
cmake ..
make
```

---

## Author

<div align="center">

**Mainuddin Monsur Robin**
*M.Sc. Information and Communication Engineering — HAW Hamburg*

[![GitHub](https://img.shields.io/badge/GitHub-MM--Robin-181717?style=flat-square&logo=github)](https://github.com/MM-Robin)

</div>
