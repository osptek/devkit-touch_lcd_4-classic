<p align="left"><img alt="OSPTEK" src="./images/logo.png" width="200" /></p>

<h1 align="center">ESP32-S3 Touch LCD 4 · Classic</h1>

<p align="center">为 86 型墙面交互打造的方屏控制面板。</p>

<p align="center"><a href="./README_EN.md">English</a> | 简体中文</p>

<p align="center"><img alt="OSPTEK ESP32-S3-Touch-4-Classic 产品宣传图" src="./docs/images/banner-v2.png" width="100%" /></p>

<p align="center"><sub>屏幕界面为视觉设计示意，实际运行界面取决于所烧录的固件。 <a href="./images/product-ui-v2.png">查看产品界面预览</a></sub></p>

## 产品概览

Classic 版采用 **ESP32-S3-WROOM-1-N16R8** 和 3.95 英寸 480×480 电容触摸屏，提供 RS485、I²C、蜂鸣器与 USB Type-C 调试接口。仓库中的示例与预编译固件已在 Classic 板上验证；电源树和端子参数以 **ESP32-S3-Touch 基础板 V1.0** 原理图为准。

| 一眼了解 | 配置 |
| :--- | :--- |
| **显示** | 3.95 英寸 · 480×480 · ST7701S + FT6336U |
| **主控** | ESP32-S3 · 16 MB Flash · 8 MB PSRAM |
| **通信** | Wi-Fi / BLE 5 · RS485 · I²C |
| **板载资源** | USB Type-C · CH340K · 蜂鸣器 |

适合墙面中控、设备状态显示和本地人机交互。

**从这里开始**　[快速开始](#快速开始) · [示例工程](#示例工程) · [预编译固件](#预编译固件)

**继续了解**　[规格参数](#规格参数) · [屏幕](#屏幕) · [硬件资源](#硬件资源) · [相关资料](#相关资料)

---

## 规格参数

### 主控与存储

| 项目 | 规格 |
| ---- | ---- |
| 产品型号 | ESP32-S3-Touch-4-Classic |
| 主板 / 原理图 | ESP32-S3-Touch 基础板 V1.0 |
| 主控模组 | ESP32-S3-WROOM-1-N16R8 |
| Flash | 16 MB |
| PSRAM | 8 MB |
| 无线 | 2.4 GHz Wi-Fi、Bluetooth LE 5 |

### 显示与触摸

概览如下；完整模组参数、驱动与触摸说明见 [屏幕](#屏幕)。

| 项目 | 规格 |
| ---- | ---- |
| 屏模组 | YDP395BT009-V1（约 3.95 英寸） |
| 分辨率 | 480×480 |
| 驱动 IC | ST7701S |
| 显示接口 | RGB 18-bit |
| 触摸 | 电容触摸（FT6336U，I²C） |
| 亮度 | 典型 350 cd/m² |

### 接口与电源

| 项目 | 规格 |
| ---- | ---- |
| USB | Type-C（供电、烧录） |
| USB 转串口 | CH340K |
| RS485 | 板载 |
| 传感器 | I²C |
| 听觉 | 板载蜂鸣器 |

电源树、收发器件与精确电气参数见 [原理图](./docs/ESP32-S3-Touch基础板V1.0.pdf)。

## 屏幕

本面板搭载 OSPTEK 自产 TFT 模组 **YDP395BT009-V1**，驱动 IC 为 **ST7701S**，通过主板 LCD FPC 连接；触摸为电容方案（I²C，FT6336U）。

<details>
<summary><strong>查看完整屏幕模组参数 · YDP395BT009-V1</strong></summary>

| 项目 | 规格 |
| ---- | ---- |
| 模组型号 | YDP395BT009-V1 |
| 尺寸 | 3.95 英寸（对角线） |
| 显示模式 | Normally Black |
| 分辨率 | 480（H）RGB × 480（V） |
| 点距 | 153 μm × 153 μm |
| 有效显示区 | 71.86 × 70.18 mm |
| 模组外形 | 83.85 × 83.85 × 3.27 mm |
| 排列 | RGB 垂直条纹 |
| 接口 | RGB 18-bit（含 HSYNC / VSYNC / DE / DCLK）；驱动初始化为 3-wire SPI（SDA / SCL / CS） |
| 驱动 IC | ST7701S |
| 亮度 | 典型 350 cd/m²（最小约 300） |
| 视角 | 全视角（典型约 80°） |
| 对比度 | 典型约 1000:1 |
| 背光 | 8 颗白光 LED（背光供电典型约 12 V / 40 mA） |
| 工作温度 | −20 ℃ ~ +70 ℃ |
| 存储温度 | −30 ℃ ~ +80 ℃ |

触摸侧经同一 FPC 引出 `TP_SCL` / `TP_SDA` / `TP_INT` / `TP_RESET` 等信号，供电典型 2.8–3.3 V。

</details>

### 屏幕相关资料

- [屏模组规格书 YDP395BT009-V1（PDF）](./docs/YDP395BT009-V1.pdf)
- [总成图 CAD（YDP395BT009-V1）](./docs/YDP395BT009-V1.dwg)
- [驱动 IC ST7701S Datasheet（PDF）](./docs/ST7701S_SPEC_V1.3.pdf)
- [触摸 IC FT6336U Datasheet（PDF）](./docs/FT6336U_DataSheet_V1.1.pdf)
- [初始化序列（文本）](./docs/BOE3.95_480x480_ST7701S_init.txt)

## 硬件资源

### 板载资源概览

| 资源 | 说明 |
| ---- | ---- |
| ESP32-S3-WROOM-1-N16R8 | Wi-Fi + BLE MCU 模组 |
| RS485 | 板载收发 |
| USB 转换 | CH340K |
| LCD 连接器 | FPC，连接 LCD |
| 蜂鸣器 | 板载 |

### 原理图

- [ESP32-S3-Touch 基础板 V1.0 原理图（PDF）](./docs/ESP32-S3-Touch基础板V1.0.pdf)

## 快速开始

**先验证显示，再选择开发路径。** 准备本面板、支持数据传输的 USB 线和电脑。

| 目标 | 操作 |
| :--- | :--- |
| 先看运行效果 | 用 USB 连接面板，按[预编译固件](#预编译固件)中的地址和参数烧录合并镜像。 |
| 自行开发 | 选择下方[示例工程](#示例工程)，安装与工程匹配的 ESP-IDF 版本后编译、烧录。 |

Windows 用户可使用乐鑫 [Flash 下载工具](https://www.espressif.com/zh-hans/support/download/other-tools)；串口、接线和硬件细节见[基础板 V1.0 原理图](./docs/ESP32-S3-Touch基础板V1.0.pdf)。使用命令行的烧录步骤见[预编译固件](#预编译固件)。

## 示例工程

触摸走乐鑫 `i2c_master` + `esp_lcd_touch_ft5x06`，已去掉旧版 `driver/i2c.h` / `i2c_driver_install`。屏为 RGB ST7701，480×480。

| 说明 | 路径 |
| ---- | ---- |
| ESP-IDF 5 · LVGL 8 通用 Demo | [`examples/s3-idf5_st7701-rgb_lvgl8-common-demo/`](./examples/s3-idf5_st7701-rgb_lvgl8-common-demo/) |
| ESP-IDF 5 · LVGL 9 通用 Demo | [`examples/s3-idf5_st7701-rgb_lvgl9-common-demo/`](./examples/s3-idf5_st7701-rgb_lvgl9-common-demo/) |
| ESP-IDF 5 · 3.95 寸盒体工程（rev2） | [`examples/ESP32S3_3.95In_Box_rev2/`](./examples/ESP32S3_3.95In_Box_rev2/) |
| ESP-IDF 5 · LVGL 8 游戏 Demo | [`examples/esp32s3_st7701_lvgl-game/`](./examples/esp32s3_st7701_lvgl-game/) |
| ESP-IDF 5 · LVGL 9 Lottie 播放 | [`examples/esp32s3-idf5_st7701-rgb_lvgl9-lottie-player/`](./examples/esp32s3-idf5_st7701-rgb_lvgl9-lottie-player/) |
| ESP-IDF 6 · LVGL 8 通用 Demo | [`examples/esp32s3-idf6_st7701-rgb_lvgl8-common-demo/`](./examples/esp32s3-idf6_st7701-rgb_lvgl8-common-demo/) |
| ESP-IDF 6 · LVGL 9 通用 Demo | [`examples/esp32s3-idf6_st7701-rgb_lvgl9-common-demo/`](./examples/esp32s3-idf6_st7701-rgb_lvgl9-common-demo/) |

> 下列示例与预编译固件已在 **Classic** 板上验证。

在已安装对应版本 ESP-IDF 的环境下（IDF 5 工程建议 ≥5.5；IDF 6 工程用 IDF 6）：

```bash
cd examples/s3-idf5_st7701-rgb_lvgl8-common-demo
idf.py set-target esp32s3
idf.py build
idf.py -p <串口> flash monitor
```

组件依赖由各工程 `main/idf_component.yml` 管理，首次编译会自动拉取。

## 预编译固件

| 文件 | 烧录地址 | 说明 |
| ---- | -------- | ---- |
| [`firmware/esp32-s3-touch-lcd-4.bin`](./firmware/esp32-s3-touch-lcd-4.bin) | **`0x0`** | 合并烧录镜像（bootloader + 分区表 + 应用），出厂演示固件 |

Flash 参数与工程配置一致：芯片 **ESP32-S3**，Flash **16 MB**，**DIO**，**80 MHz**。合并包从地址 **`0x0`** 整包写入。

### 方式一：Flash 下载工具（Windows，推荐上手）

1. 下载并打开乐鑫 **[Flash 下载工具](https://www.espressif.com/zh-hans/support/download/other-tools)**。
2. `ChipType` 选 **ESP32-S3**，`WorkMode` 选 Develop，`LoadMode` 选 UART。
3. 勾选一行，固件选 [`firmware/esp32-s3-touch-lcd-4.bin`](./firmware/esp32-s3-touch-lcd-4.bin)，地址填 **`0x0`**（不要填成应用分区的 `0x10000`）。
4. SPI SPEED / SPI MODE / FLASH SIZE 按上表选择（80 MHz、DIO、16 MB）。
5. 选择正确 COM 口，点 **START** 烧录。

详细界面说明见：[Flash 下载工具用户指南 · ESP32-S3](https://docs.espressif.com/projects/esp-test-tools/zh_CN/latest/esp32s3/production_stage/tools/flash_download_tool.html)

### 方式二：esptool（命令行）

将 `<串口>` 换成实际端口（如 `/dev/ttyUSB0`、`COM3`）；地址为 **`0x0`**：

```bash
esptool.py --chip esp32s3 -p <串口> write_flash 0x0 firmware/esp32-s3-touch-lcd-4.bin
```

## 仓库结构

```text
devkit-touch_lcd_4-classic/
├── README.md
├── README_EN.md
├── images/
├── docs/          # 规格书、原理图、86 型外壳 CAD
├── firmware/
└── examples/
```

## 相关资料

### 本产品资料

- [ESP32-S3-Touch 基础板 V1.0 原理图（PDF）](./docs/ESP32-S3-Touch基础板V1.0.pdf)
- [屏模组规格书 YDP395BT009-V1（PDF）](./docs/YDP395BT009-V1.pdf)
- [总成图 CAD（YDP395BT009-V1）](./docs/YDP395BT009-V1.dwg)
- [驱动 IC ST7701S Datasheet（PDF）](./docs/ST7701S_SPEC_V1.3.pdf)
- [触摸 IC FT6336U Datasheet（PDF）](./docs/FT6336U_DataSheet_V1.1.pdf)
- [初始化序列（文本）](./docs/BOE3.95_480x480_ST7701S_init.txt)
- [示例工程](#示例工程)
- [预编译固件 esp32-s3-touch-lcd-4.bin](./firmware/esp32-s3-touch-lcd-4.bin)

### 系列通用外壳 CAD

86 型外壳（2 层 / 4 层）全型号通用，文件在本仓库 `docs/`。

- [4 层：`0302(1).dwg`](./docs/86-enclosure-4-layer/0302(1).dwg)
- [4 层：`WSD4寸-2d-1116.dwg`](./docs/86-enclosure-4-layer/WSD4%E5%AF%B8-2d-1116.dwg)
- [2 层：`3.95-01 PCB.dwg`](./docs/86-enclosure-2-layer/3.95-01%20PCB.dwg)
- [2 层：`增加开口结构外壳20250102.dwg`](./docs/86-enclosure-2-layer/%E5%A2%9E%E5%8A%A0%E5%BC%80%E5%8F%A3%E7%BB%93%E6%9E%84%E5%A4%96%E5%A3%B320250102.dwg)
- [2 层：`装配0718(1).DWG`](./docs/86-enclosure-2-layer/%E8%A3%85%E9%85%8D0718(1).DWG)

### 芯片资料（乐鑫官方）

- [ESP32-S3 系列产品页（中文）](https://www.espressif.com/zh-hans/products/socs/esp32-s3)
- [ESP32-S3 系列产品页（英文）](https://www.espressif.com/en/products/socs/esp32-s3)
- [ESP-IDF 编程指南 · ESP32-S3（中文）](https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32s3/index.html)
- [ESP-IDF Programming Guide · ESP32-S3（English）](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/index.html)

## 购买链接

<p align="center">
  <a href="https://shop110742373.taobao.com/"><img alt="淘宝官方店铺" src="https://img.shields.io/badge/淘宝-官方店铺-FF6A00?style=for-the-badge" /></a>
  &nbsp;&nbsp;
  <a href="https://www.aliexpress.com/store/1105701619"><img alt="速卖通官方店铺" src="https://img.shields.io/badge/速卖通-官方店铺-E62E04?style=for-the-badge&logo=aliexpress&logoColor=white" /></a>
</p>

**国内（淘宝）**

- 店铺：[鱼鹰光电工厂店](https://shop110742373.taobao.com/)

**海外（AliExpress）**

- 店铺：[OSPTEK Official Store](https://www.aliexpress.com/store/1105701619)

---

## 技术支持

如有技术问题或合作需求，欢迎通过以下方式联系我们：

- 技术支持 / 产品咨询：<luyu@osptek.com>
- QQ 技术交流群：**985881096**
- 公司官网：<https://osptek.com/>
- 有任何问题，都可以在本仓库 Issues 中提问

---

<p align="center"><sub>© 2026 OSPTEK 鱼鹰光电 · 本仓库资料采用 CC BY 4.0 许可</sub></p>
