<!--
 * @Description: None
 * @Author: LILYGO_L
 * @Date: 2023-09-11 16:13:14
 * @LastEditTime: 2024-12-06 18:05:19
 * @License: GPL 3.0
-->
<h1 align = "center">T-Keyboard-S3-Pro</h1>

<p align="center" width="100%">
    <img src="image/5.jpg" alt="">
</p>

---

<p align="center" width="100%">
    <img src="image/6.jpg" alt="">
</p>

## **[English](./README.md) | 中文**

## 版本迭代:

| Version    | Update date    | Update description  |
| :-----------: | :-----------: | :-----------: |
| T-Keyboard-S3-Pro_MCU_V1.1 | 2024-09-05              | Original version |
| T-Keyboard-S3-Pro_Keyboard_V1.1| 2024-09-05        | Original version |
| T-Keyboard-S3-Pro_Magnet_Female_V1.0| 2024-09-05        | Original version |
| T-Keyboard-S3-Pro_Magnet_Male_V1.0| 2024-09-05        | Original version |
| T-Keyboard-S3-Pro_Keyboard_LCD_FPC_V1.0| 2024-09-05        | Original version |

## 购买链接

| Product                     |Link               |
| :------------------------: | :-----------: |
| T-Keyboard-S3-Pro   |  [LILYGO Mall](https://lilygo.cc/products/t-keyboard-s3-pro?_pos=1&_sid=ab2fe5376&_ss=r) |

## 目录
- [描述](#描述)
- [预览](#预览)
- [模块](#模块)
- [相关测试](#相关测试)
- [软件引导](#软件引导)
- [常见问题](#常见问题)
- [项目](#项目)

## 描述

这是基于T-Keyboard-S3项目开发的升级版T-Keyboard-S3-Pro。升级版的T-Keyboard-S3-Pro删除了原版的外置扩展接口，引出了4个方向的具有快速连接的磁吸接口，磁吸接口将可以同时互联多个T-Keyboard-S3-Pro设备（最多6个 在连接多个设备的同时需要降低板载LED最大亮度为10）。在原版四个屏幕的基础上再增加1个屏幕，一共有5个屏幕，其中第5个位置的屏幕在主机上可替换为旋转编码器使用。值得注意的是由于硬件上的长距离走线，板子在扩展的方向上有一些限制，以主机为中心左边和右边最多只能扩1个设备，下方最多扩2个设备（上方有USB接口阻挡扩不了设备），组成一个横x列为2x3的阵列，一共6个设备。

板子上还带有14个可编程设置的RGB的LED灯，单板运行时候可以全部开到最亮，但是多个板子运行时不能开到最亮，因为该LED由于总数量过多，全部高亮后将发热严重，而且USB口的供电流有限，每接上一个板子5V电压的传输就会增加一部分的阻抗等种种原因，在同时接入6个设备的时候，将LED灯亮度调整为10将是一个合理的设置。

## 预览

### 实物图

<p align="center" width="100%">
    <img src="image/6.jpg" alt="">
</p>

---

<p align="center" width="100%">
    <img src="image/7.jpg" alt="">
</p>

---

<p align="center" width="100%">
    <img src="image/8.jpg" alt="">
</p>

### PCB板

#### 1. 尺寸

<p align="center" width="100%">
    <img src="image/1.jpg" alt="">
</p>

---

<p align="center" width="100%">
    <img src="image/2.jpg" alt="">
</p>

#### 2. 模块说明

<p align="center" width="100%">
    <img src="image/3.jpg" alt="">
</p>

---

<p align="center" width="100%">
    <img src="image/4.jpg" alt="">
</p>

## 模块

### 1. 主要的MCU

* 模块：ESP32­-S3-WROOM­-1
* 芯片：ESP32-S3-R8
* PSRAM：8M (Octal SPI)
* FLASH：16M
* 相关资料：
    >[ESP32-S3­-WROOM­-1_datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)
* 依赖库：
    >[Arduino_DriveBus-1.1.2](https://github.com/Xk-w/Arduino_DriveBus)


### 2. 次要的MCU

* 芯片：STM32G030F6P6
* SRAM：8 Kbytes
* FLASH：64 Kbytes
* 相关资料：
    >[STM32G030F6_datasheet](https://www.st.com/en/microcontrollers-microprocessors/stm32g030f6.html#documentation)

### 3. 屏幕

* 屏幕型号：N085-1212TBWIG06-C08
* 尺寸：0.85英寸
* 分辨率：128x128px
* 屏幕类型：TFT
* 驱动芯片：GC9107
* 使用总线通信协议：标准SPI
* 其他说明：所有屏幕的RST、DC、MOSI、SCLK、BL引脚各共用一条总线，初始化复位时候所有屏幕一起复位，选择不同CS线即可控制不同的屏幕刷新数据
* 相关资料：
    >[GC9107_DataSheet_V1.2](./information/GC9107_DataSheet_V1.2.pdf)
* 依赖库：
    >[TFT_eSPI-2.5.0](https://github.com/Bodmer/TFT_eSPI)<br /> 
    >[lvgl-8.3.5](https://github.com/lvgl/lvgl) <br /> 
    >[Arduino_GFX-1.3.7](https://github.com/moononournation/Arduino_GFX)<br /> 

### 4. 热插拔按键

* 规格：选用的热插拔连接器是Kailh公司的连接器，两引脚间距是6.35MM，满足间距为6.35mm的热插拔针脚按键都可适用
* PCB连接：下拉使能低电平作为判断信号，主机的KEY5复用为BOOT-0作为系统上电模式选择，默认有一个10K上拉电阻，同样以低电平作为判断信号，软件内必须配置其引脚为内部上拉才能稳定使用
* 其他说明：因为要连接屏幕，所以请务必选择中间有开孔的热插拔按键，间距应该大于排线宽度7MM以上

### 5. 板载LED

* 芯片：WS2812C
* 相关资料：
    >[WS2812C-2020](./information/WS2812C-2020.pdf)

### 6. 旋转编码器

* 描述：四脚铜顶针旋钮

## 相关测试

## 软件引导

### 1. ESP32S3 主机设备软件引导

| Branch | `[PlatformIO (arduino-espressif32_v6.5.0)]`<br />`[Arduino IDE (arduino-esp32-lib_v2.0.14)]` <br /> Support |Description   |
| :-----------: | :-----------: | :-----------: | 
|[arduino-esp32-libs_V2.0.14](https://github.com/Xinyuan-LilyGO/T-Keyboard-S3-Pro/tree/arduino-esp32-libs_V2.0.14)| <p align="center"> <img src="https://img.shields.io/badge/-supported-green" alt="example" width="25%"> </p> |  |

### 2. STM32 从机设备软件引导

| Branch | `[STM32CubeMX (stm32cubeg0-firmware-package_V1.6.2)]`<br />`[ARM Keil μVision5 (Keil.STM32G0xx_DFP.1.4.0.pack)]` <br /> Support  |Description   |
| :-----------: | :-----------: | :-----------: | 
|[stm32cubeg0-firmware-package_V1.6.2](https://github.com/Xinyuan-LilyGO/T-Keyboard-S3-Pro/tree/stm32cubeg0-firmware-package_V1.6.2)|  <p align="center"> <img src="https://img.shields.io/badge/-supported-green" alt="example" width="20%"> </p>  |  |

## 常见问题

* Q. 看了以上教程我还是不会搭建编程环境怎么办？
* A. 如果看了以上教程还不懂如何搭建环境的可以参考[LilyGo-Document](https://github.com/Xinyuan-LilyGO/LilyGo-Document)文档说明来搭建。

<br />

## 项目
* [SCH_T-Keyboard-S3-Pro_MCU_V1.1](./project/SCH_T-Keyboard-S3-Pro_MCU_V1.1.pdf)
* [SCH_T-Keyboard-S3-Pro_Keyboard_V1.1](./project/SCH_T-Keyboard-S3-Pro_Keyboard_V1.1.pdf)
* [SCH_T-Keyboard-S3-Pro_Magnet_Female_V1.0](./project/SCH_T-Keyboard-S3-Pro_Magnet_Female_V1.0.pdf)
* [SCH_T-Keyboard-S3-Pro_Magnet_Male_V1.0](./project/SCH_T-Keyboard-S3-Pro_Magnet_Male_V1.0.pdf)
* [SCH_T-Keyboard-S3-Pro_Keyboard_LCD_FPC_V1.0](./project/SCH_T-Keyboard-S3-Pro_Keyboard_LCD_FPC_V1.0.pdf)
