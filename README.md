# Spectra Watermaker Monitoring

[![Buy Me A Coffee](https://img.shields.io/badge/☕-Buy%20Me%20a%20Coffee-yellow?style=for-the-badge)](https://buymeacoffee.com/lnx13)
![Stars](https://img.shields.io/github/stars/lnx13/spectra-watermaker-monitor?color=yellow&style=flat)
![Issues](https://img.shields.io/github/issues/lnx13/spectra-watermaker-monitor?color=orange&style=flat)
![Last Commit](https://img.shields.io/github/last-commit/lnx13/spectra-watermaker-monitor?color=blue&style=flat)
![ESPHome](https://img.shields.io/badge/ESPHome-100%25-blue?style=flat)
[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/badges/StandWithUkraine.svg)](https://stand-with-ukraine.pp.ua)
---

## 📘 Overview

This project provides a **real‑time monitoring system for the Spectra Ventura Watermaker**, powered by an **ESP32 + ADS1115 + ST7789 display**.  
It visualizes watermaker performance, detects clarks pump cycles, monitors pressures, TDS, flow, and exports clean data to Home Assistant.

---

## 📚 Table of Contents  
- [📸 Photos](#-photos)  
- [⚙️ Hardware Used](#️-hardware-used)  
- [🔌 Pinout](#-pinout)  
- [📊 Display UI Layout](#-display-ui-layout-placeholder)  
- [🧠 Features](#-features)  
- [⚙️ Firmware Structure](#️-configuration-firmware)  
- [☕ Support](#-support)  
- [🙌 Credits](#-credits)

---

## 📸 Photos

```
/docs/1.jpg
/docs/2.jpg
/docs/3.jpg
```

---

## ⚙️ Hardware Used

| Module | Description |
|-------|-------------|
| **IdeaSpark ESP32 Dev Board (16MB)** | Main controller + integrated ST7789 display |
| **ADS1115 (0x48)** | 4‑channel 16‑bit ADC |
| **Hall Flow Sensor (1/4")** | Pulse output, via voltage divider |
| **Pressure Transducers (0–200 PSI, 0.5–4.5V)** | Before & after filter pressures |
| **Active Buzzer (5V)** | Alarm output via transistor |
| **Misc Wiring / Resistors** | Installation‑dependent |

---

## 🔌 Pinout

### **ESP32 → Display (ST7789)**  
| Signal | GPIO |
|--------|------|
| MOSI | 23 |
| SCLK | 18 |
| CS | 15 |
| DC | 2 |
| RESET | 4 |
| Backlight | 32 (PWM) |

### **ESP32 → ADS1115**
| ADS1115 | ESP32 |
|---------|--------|
| SDA | 21 |
| SCL | 22 |
| VDD | 5V |
| GND | GND |

### **ADS1115 Channels**
| Channel | Usage |
|---------|--------|
| A0 | TDS voltage |
| A1 | Pressure Before |
| A2 | Pressure After |
| A3 | *free* |

### **ESP32 Other**
| Function | GPIO |
|----------|-------|
| Flow Sensor Input | 25 |
| Buzzer Output | 26 |

---

## 📊 Display UI Layout (Placeholder)

```
+------------------------------------------------------+
| TDS:  124 ppm                      12:48:55          |
| Flow: 6.8 gph      P_out: 42.1 psi                   |
| P_in: 52.4 psi     dP:    10.3 psi                   |
| A: 4.8   B: 5.1            Imb: 0.3 psi              |
|                                                      |
| !!! HIGH TDS !!!  (only shown when alarm active)     |
+------------------------------------------------------+
```

---

## 🧠 Features

- 📺 **Real‑time TFT UI** on ST7789 (large fonts, dark‑mode friendly)
- ⚡ **High‑frequency RAW sampling** (10 ms interval)
- 🎚 **16‑bit ADC (ADS1115)** for stable pressure values
- 💧 **Flow sensor** with proper debouncing
- 🔍 **Piston cycle analyzer:**
  - Detects piston A & B strokes  
  - Measures stroke amplitudes  
  - Computes imbalance indicator  
- 🚨 **TDS alarm + buzzer**
- 🔧 **Calibration parameters** saved across reboots:
  - Pressure gain/offset  
  - TDS factor  
  - Flow K‑factor  
- 🏠 **Home Assistant integration**
  - Separate HA‑safe throttled sensors  
  - RAW sensors internal for performance  
- 🎨 Clean, readable ESPHome‑drawn UI

---

## ⚙️ Firmware Structure

The full ESPHome config lives in:

```
ro-monitor.yaml
```

Includes:

- Sensor pipelines  
- Display drawing  
- Calibration storage  
- Piston detector logic  
- All HA sensor wrappers  

---

## ☕ Support

If this project helped you, consider supporting development:

[![Buy Me A Coffee](https://img.shields.io/badge/☕-Support%20This%20Project-yellow?style=for-the-badge)](https://buymeacoffee.com/lnx13)

---

## 🙌 Credits

Built by **lnx13**  
Enhanced with ❤️ using ESPHome.  
PRs welcome!

