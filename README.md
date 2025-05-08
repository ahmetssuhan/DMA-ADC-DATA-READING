# STM32F407G-DISC1 • ADC1 with DMA2_Stream0  
Single-channel continuous conversion from PA0 (potentiometer input)

---

## Overview
This project demonstrates low-overhead acquisition of an analog signal on **PA0** using **ADC1** and **DMA2_Stream0**. The ADC operates in continuous mode while DMA transfers each 12-bit sample to a circular buffer in memory, leaving the CPU free for other tasks.

---

## Hardware

| Resource            | Details                                            |
|---------------------|----------------------------------------------------|
| MCU / Board         | STM32F407G-DISC1                                   |
| Analog input pin    | **PA0** (connect the wiper of a 10 kΩ potentiometer) |
| Reference voltage   | 3.0 V (board default)                              |
| Debug interface     | On-board ST-LINK/V2                                |

**Potentiometer wiring**

| Potentiometer Pin | Connects To           |
|-------------------|-----------------------|
| CW end            | 3 V pin (CN3-5)       |
| CCW end           | GND (CN3-3)           |
| Wiper             | **PA0** (CN3-1)       |

---

## Software Prerequisites

| Component          | Minimum Version | Notes                                  |
|--------------------|-----------------|----------------------------------------|
| STM32CubeIDE       | 1.15            | Generates startup files and builds ELF |
| ARM GCC toolchain  | Installed with CubeIDE |                                  |
| STM32 HAL drivers  | F4 v1.27.x      | Included in CubeIDE project template   |

---

## Project Structure

```plaintext /Inc └── main.h /Src └── main.c ← GPIO, ADC, DMA configuration README.md ← This document ``` 


All configuration is performed in `main.c`; no additional CubeMX code generation is required.

---

## Build and Flash

1. **Import the project** into STM32CubeIDE (`File ▸ Import ▸ Existing Projects into Workspace`).
2. **Build** the project (`Project ▸ Build Project` or the hammer icon).
3. **Connect** the Discovery board via USB.
4. **Run / Debug** (`Run ▸ Debug` or the bug icon).  
   The program is loaded and starts automatically.

---

## Verifying Operation

1. Open **Live Expressions** in CubeIDE.
2. Add the symbol `adc_value[0]`.
3. Rotate the potentiometer.  
   The variable should vary between 0 and 4095, reflecting the 0–3 V input.

---

## Extending the Code

| Objective                     | Required Changes                                             |
|-------------------------------|--------------------------------------------------------------|
| Increase buffer length        | Update `#define BufferLength` and enlarge `adc_value[]`.     |
| Add more ADC channels         | Enable scan mode, configure additional channels, adjust DMA. |
| Generate interrupts on half/full buffer | Enable `DMA_IT_HT` / `DMA_IT_TC` and add ISR.     |

---

## License
Distributed under the MIT License. See `LICENSE` file for details.
