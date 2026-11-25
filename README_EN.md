<p align="left"><img alt="OSPTEK" src="./images/logo.png" width="200" /></p>

<h1 align="center">ESP32-S3 Touch LCD 4 · Classic</h1>

<p align="center">A square touch panel for 86-type wall controls.</p>

<p align="center">English | <a href="./README.md">简体中文</a></p>

<p align="center"><img alt="OSPTEK ESP32-S3-Touch-4-Classic product banner" src="./docs/images/banner-v2.png" width="100%" /></p>

<p align="center"><sub>Screen UI is a design concept; the running interface depends on the firmware. <a href="./images/product-ui-v2.png">View the product UI preview</a></sub></p>

## Overview

Classic combines the **ESP32-S3-WROOM-1-N16R8** with a 3.95-inch 480×480 capacitive display. It provides RS485, I²C, a buzzer, and USB Type-C debugging. The examples and prebuilt firmware in this repository were verified on the Classic board. Refer to the **ESP32-S3-Touch Base Board V1.0** schematic for the power tree and terminal ratings.

| At a glance | Configuration |
| :--- | :--- |
| **Display** | 3.95 in · 480×480 · ST7701S + FT6336U |
| **Processor** | ESP32-S3 · 16 MB Flash · 8 MB PSRAM |
| **Connectivity** | Wi-Fi / BLE 5 · RS485 · I²C |
| **Onboard** | USB Type-C · CH340K · buzzer |

Designed for wall controls, device status displays, and local HMI.

**Start here**　[Quick Start](#quick-start) · [Examples](#examples) · [Prebuilt Firmware](#prebuilt-firmware)

**Explore**　[Specifications](#specifications) · [Display](#display) · [Hardware Resources](#hardware-resources) · [Documentation](#documentation)

---

## Specifications

### MCU & Memory

| Item | Specification |
| ---- | ------------- |
| Product model | ESP32-S3-Touch-4-Classic |
| Board / schematic | ESP32-S3-Touch Standard board V1.0 |
| Module | ESP32-S3-WROOM-1-N16R8 |
| Flash | 16 MB |
| PSRAM | 8 MB |
| Wireless | 2.4 GHz Wi-Fi, Bluetooth LE 5 |

### Display & Touch

Summary below; full module parameters, driver, and touch details are in [Display](#display).

| Item | Specification |
| ---- | ------------- |
| Panel module | YDP395BT009-V1 (~3.95") |
| Resolution | 480×480 |
| Driver IC | ST7701S |
| Display interface | RGB 18-bit |
| Touch | Capacitive (FT6336U, I²C) |
| Brightness | 350 cd/m² typ. |

### Interfaces & Power

| Item | Specification |
| ---- | ------------- |
| USB | Type-C (power, flash) |
| USB-UART | CH340K |
| RS485 | Onboard |
| Sensor | I²C |
| Audio cue | Onboard buzzer |

Power tree and exact electrical ratings: see the [schematic](./docs/ESP32-S3-Touch基础板V1.0.pdf).

## Display

This panel uses OSPTEK TFT module **YDP395BT009-V1** with driver IC **ST7701S**, connected via the board LCD FPC. Touch is capacitive (I²C, FT6336U).

<details>
<summary><strong>Full display module specifications · YDP395BT009-V1</strong></summary>

| Item | Specification |
| ---- | ------------- |
| Module model | YDP395BT009-V1 |
| Size | 3.95" (diagonal) |
| Display mode | Normally black |
| Resolution | 480 (H) RGB × 480 (V) |
| Dot pitch | 153 μm × 153 μm |
| Active area | 71.86 × 70.18 mm |
| Module outline | 83.85 × 83.85 × 3.27 mm |
| Color arrangement | RGB vertical stripe |
| Interface | RGB 18-bit (HSYNC / VSYNC / DE / DCLK); driver init via 3-wire SPI (SDA / SCL / CS) |
| Driver IC | ST7701S |
| Brightness | 350 cd/m² typ. (min. ~300) |
| Viewing angle | All view (typ. ~80°) |
| Contrast ratio | ~1000:1 typ. |
| Backlight | 8 white LEDs (typ. ~12 V / 40 mA) |
| Operating temp. | −20 ℃ ~ +70 ℃ |
| Storage temp. | −30 ℃ ~ +80 ℃ |

Touch signals such as `TP_SCL` / `TP_SDA` / `TP_INT` / `TP_RESET` are brought out on the same FPC; typical touch supply is 2.8–3.3 V.

</details>

### Display Documents

- [Panel datasheet YDP395BT009-V1 (PDF)](./docs/YDP395BT009-V1.pdf)
- [Assembly CAD (YDP395BT009-V1)](./docs/YDP395BT009-V1.dwg)
- [Driver IC ST7701S datasheet (PDF)](./docs/ST7701S_SPEC_V1.3.pdf)
- [Touch IC FT6336U datasheet (PDF)](./docs/FT6336U_DataSheet_V1.1.pdf)
- [Init sequence (text)](./docs/BOE3.95_480x480_ST7701S_init.txt)

## Hardware Resources

### Onboard Overview

| Resource | Description |
| -------- | ----------- |
| ESP32-S3-WROOM-1-N16R8 | Wi-Fi + BLE MCU module |
| RS485 | Onboard transceiver |
| USB bridge | CH340K |
| LCD connector | FPC to the LCD |
| Buzzer | Onboard |

### Schematic

- [ESP32-S3-Touch Standard board V1.0 schematic (PDF)](./docs/ESP32-S3-Touch基础板V1.0.pdf)

## Quick Start

**Check the display first, then choose a development path.** You need the panel, a data-capable USB cable, and a computer.

| Goal | What to do |
| :--- | :--- |
| See it running | Connect USB and flash the merged image using the address and settings in [Prebuilt Firmware](#prebuilt-firmware). |
| Build your own app | Pick an [example](#examples), install its matching ESP-IDF version, then build and flash it. |

On Windows, you can use Espressif's [Flash Download Tools](https://www.espressif.com/en/support/download/other-tools). For wiring and board details, see the [Base Board V1.0 schematic](./docs/ESP32-S3-Touch基础板V1.0.pdf). Command-line flash steps are in [Prebuilt Firmware](#prebuilt-firmware).

## Examples

Touch uses Espressif `i2c_master` + `esp_lcd_touch_ft5x06` (legacy `driver/i2c.h` / `i2c_driver_install` removed). Panel: RGB ST7701, 480×480.

| Description | Path |
| ----------- | ---- |
| ESP-IDF 5 · LVGL 8 common demo | [`examples/s3-idf5_st7701-rgb_lvgl8-common-demo/`](./examples/s3-idf5_st7701-rgb_lvgl8-common-demo/) |
| ESP-IDF 5 · LVGL 9 common demo | [`examples/s3-idf5_st7701-rgb_lvgl9-common-demo/`](./examples/s3-idf5_st7701-rgb_lvgl9-common-demo/) |
| ESP-IDF 5 · 3.95" box project (rev2) | [`examples/ESP32S3_3.95In_Box_rev2/`](./examples/ESP32S3_3.95In_Box_rev2/) |
| ESP-IDF 5 · LVGL 8 game demo | [`examples/esp32s3_st7701_lvgl-game/`](./examples/esp32s3_st7701_lvgl-game/) |
| ESP-IDF 5 · LVGL 9 Lottie player | [`examples/esp32s3-idf5_st7701-rgb_lvgl9-lottie-player/`](./examples/esp32s3-idf5_st7701-rgb_lvgl9-lottie-player/) |
| ESP-IDF 6 · LVGL 8 common demo | [`examples/esp32s3-idf6_st7701-rgb_lvgl8-common-demo/`](./examples/esp32s3-idf6_st7701-rgb_lvgl8-common-demo/) |
| ESP-IDF 6 · LVGL 9 common demo | [`examples/esp32s3-idf6_st7701-rgb_lvgl9-common-demo/`](./examples/esp32s3-idf6_st7701-rgb_lvgl9-common-demo/) |

> The examples and prebuilt firmware are verified on the **Classic** board (same panel as v1).

With the matching ESP-IDF installed (IDF 5 projects: ≥5.5; IDF 6 projects: IDF 6):

```bash
cd examples/s3-idf5_st7701-rgb_lvgl8-common-demo
idf.py set-target esp32s3
idf.py build
idf.py -p <PORT> flash monitor
```

Component dependencies are managed by each project's `main/idf_component.yml` and are fetched on the first build.

## Prebuilt Firmware

| File | Flash address | Description |
| ---- | ------------- | ----------- |
| [`firmware/esp32-s3-touch-lcd-4.bin`](./firmware/esp32-s3-touch-lcd-4.bin) | **`0x0`** | Merged image (bootloader + partition table + app), factory demo firmware |

Flash settings match the project: chip **ESP32-S3**, Flash **16 MB**, **DIO**, **80 MHz**. Write the merged package from address **`0x0`**.

### Option 1: Flash Download Tools (Windows, easiest)

1. Download and open Espressif **[Flash Download Tools](https://www.espressif.com/en/support/download/other-tools)**.
2. Set `ChipType` to **ESP32-S3**, `WorkMode` to Develop, `LoadMode` to UART.
3. Enable one row, select [`firmware/esp32-s3-touch-lcd-4.bin`](./firmware/esp32-s3-touch-lcd-4.bin), address **`0x0`** (do not use app-partition `0x10000`).
4. Set SPI SPEED / SPI MODE / FLASH SIZE as above (80 MHz, DIO, 16 MB).
5. Select the correct COM port and click **START**.

UI details: [Flash Download Tool User Guide · ESP32-S3](https://docs.espressif.com/projects/esp-test-tools/en/latest/esp32s3/production_stage/tools/flash_download_tool.html)

### Option 2: esptool (CLI)

Replace `<PORT>` with your serial port (e.g. `/dev/ttyUSB0`, `COM3`); address is **`0x0`**:

```bash
esptool.py --chip esp32s3 -p <PORT> write_flash 0x0 firmware/esp32-s3-touch-lcd-4.bin
```

## Repository layout

```text
devkit-touch_lcd_4-classic/
├── README.md
├── README_EN.md
├── images/
├── docs/          # datasheets, schematic, shared 86-type enclosure CAD
├── firmware/
└── examples/
```

## Documentation

### Product Documents

- [ESP32-S3-Touch Standard board V1.0 schematic (PDF)](./docs/ESP32-S3-Touch基础板V1.0.pdf)
- [Panel datasheet YDP395BT009-V1 (PDF)](./docs/YDP395BT009-V1.pdf)
- [Assembly CAD (YDP395BT009-V1)](./docs/YDP395BT009-V1.dwg)
- [Driver IC ST7701S datasheet (PDF)](./docs/ST7701S_SPEC_V1.3.pdf)
- [Touch IC FT6336U datasheet (PDF)](./docs/FT6336U_DataSheet_V1.1.pdf)
- [Init sequence (text)](./docs/BOE3.95_480x480_ST7701S_init.txt)
- [Examples](#examples)
- [Prebuilt firmware esp32-s3-touch-lcd-4.bin](./firmware/esp32-s3-touch-lcd-4.bin)

### Shared enclosure CAD

The 86-type enclosure (2-layer / 4-layer) is shared by every SKU. Files live in the repo-root `docs/` folder.

- [4-layer: `0302(1).dwg`](./docs/86-enclosure-4-layer/0302(1).dwg)
- [4-layer: `WSD4寸-2d-1116.dwg`](./docs/86-enclosure-4-layer/WSD4%E5%AF%B8-2d-1116.dwg)
- [2-layer: `3.95-01 PCB.dwg`](./docs/86-enclosure-2-layer/3.95-01%20PCB.dwg)
- [2-layer: `增加开口结构外壳20250102.dwg`](./docs/86-enclosure-2-layer/%E5%A2%9E%E5%8A%A0%E5%BC%80%E5%8F%A3%E7%BB%93%E6%9E%84%E5%A4%96%E5%A3%B320250102.dwg)
- [2-layer: `装配0718(1).DWG`](./docs/86-enclosure-2-layer/%E8%A3%85%E9%85%8D0718(1).DWG)

### Chip Documents (Espressif)

- [ESP32-S3 product page](https://www.espressif.com/en/products/socs/esp32-s3)
- [ESP32-S3 系列产品页（中文）](https://www.espressif.com/zh-hans/products/socs/esp32-s3)
- [ESP-IDF Programming Guide · ESP32-S3](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/index.html)
- [ESP-IDF 编程指南 · ESP32-S3（中文）](https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32s3/index.html)

## Where to Buy

<p align="center">
  <a href="https://www.aliexpress.com/store/1105701619"><img alt="AliExpress Official Store" src="https://img.shields.io/badge/AliExpress-Official_Store-E62E04?style=for-the-badge&logo=aliexpress&logoColor=white" /></a>
  &nbsp;&nbsp;
  <a href="https://shop110742373.taobao.com/"><img alt="Taobao Official Store" src="https://img.shields.io/badge/Taobao-Official_Store-FF6A00?style=for-the-badge" /></a>
</p>

**International (AliExpress)**

- Store: [OSPTEK Official Store](https://www.aliexpress.com/store/1105701619)

**China (Taobao)**

- Store: [鱼鹰光电工厂店](https://shop110742373.taobao.com/)

---

## Support

For technical questions or business inquiries:

- Technical support / product inquiry: <luyu@osptek.com>
- QQ technical group: **985881096**
- Website: <https://osptek.com/>
- Feel free to open an Issue in this repository if you have any questions

---

<p align="center"><sub>© 2026 OSPTEK · Materials in this repository are licensed under CC BY 4.0</sub></p>
