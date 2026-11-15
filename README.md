<p align="center">
  <img src="Images/GitHub-Assets/MES_Animated_Logo_640x480.svg" width="360" alt="MES Animated Logo">
</p>


<div dir="rtl" align="right">

<p align="center"><img src="Images/GitHub-Assets/MES-Hero-Banner.svg" width="100%" alt="معمار الکترونیک صنعت - MES"></p>

# مستندات پروژه CH32-MetaPAC

این مخزن داده‌های ساخت‌یافته و ماشین‌خوان مربوط به میکروکنترلرهای ۳۲ بیتی **WCH** را ارائه می‌کند. این داده‌ها برای تولید Peripheral Access Crate و فراداده (Metadata) تراشه‌ها در اکوسیستم Rust استفاده می‌شوند.

## معرفی پروژه

پروژه [ch32-data](https://github.com/ch32-rs/ch32-data) با هدف گردآوری داده‌های ساخت‌یافته برای میکروکنترلرهای WCH توسعه یافته است. خروجی داده‌های مربوط به دسترسی به Peripheralها و مشخصات تراشه‌ها در قالب Crate با نام [ch32-metapac](https://crates.io/crates/ch32-metapac) منتشر می‌شود. ابزار تولیدکننده در پوشه [ch32-metapac-gen](ch32-metapac-gen/) قرار دارد.

این پروژه از [stm32-data](https://github.com/embassy-rs/stm32-data) الهام گرفته است. به‌دلیل محدودیت مستندات و ابزارهای WCH، بخشی از تعریف تراشه‌ها به‌صورت دستی نگهداری می‌شود. همچنین برای کاهش تکرار داده‌ها از سازوکار include و فایل‌های مجزای خانواده‌های مختلف استفاده شده است.

**محل اصلی مشارکت:** تمام Issueها و Pull Requestهای مربوط به داده‌ها باید در مخزن [ch32-rs/ch32-data](https://github.com/ch32-rs/ch32-data) ثبت شوند، نه در مخزن خروجی/nightly متاپک.

## منابع داده

- دیتاشیت‌ها و مستندات رسمی: [WCH](https://www.wch.cn/) و [WCH-IC](https://wch-ic.com/)
- فایل‌های SVD ارائه‌شده همراه با [MounRiver Studio](https://www.mounriver.com/)
- اصلاحات و Patchهای SVD توسط پروژه [ch32-rs](https://github.com/ch32-rs/ch32-rs)
- اطلاعات تکمیلی و نمونه‌کدها از [openwch](https://github.com/openwch)

برای بررسی تعریف Peripheralها، دیتاشیت و کدهای نمونه EVT باید هم‌زمان بررسی شوند. استفاده از جدیدترین نسخه دیتاشیت ضروری است؛ گاهی نسخه چینی مستندات WCH جدیدتر از نسخه انگلیسی است.

## خانواده‌های میکروکنترلر تحت پوشش

### خانواده‌های RISC-V

| خانواده | توضیح |
|---|---|
| CH32V0 | اقتصادی، هسته V2A/V2C |
| CH32V1 | کاربرد عمومی، هسته V3A |
| CH32V203 / CH32V303 | کاربرد عمومی، هسته V4B |
| CH32V305 / CH32V307 / CH32V317 | ارتباطات پرسرعت، هسته V4F |
| CH32V407 / CH32V467 | USBHS، Ethernet و PSRAM |
| CH32V205 | USBFS/USBHS، USB PD، CAN، QSPI و PIOC |
| CH32V208 | BLE 5.3 |
| CH32X0 | PDUSB |
| CH32X315 / CH32X305 | Quad ADC، USB 3.0، USB PD و ARGB |
| CH32L1 | کم‌مصرف و PDUSB |
| CH32M103 | مبتنی بر CH32L103 به‌همراه درایور سه‌فاز Gate |
| CH32M030 | کنترل موتور، Half-Bridge و USB PD |
| CH32H4 | دو هسته V3F و V5F، USB 3.0، Gigabit Ethernet و SerDes |
| CH643 | درایور RGB |
| CH641 | USB PD |

### خانواده‌های ARM Cortex-M3

- **CH32F1:** کاربرد عمومی، نسخه پایه
- **CH32F203:** کاربرد عمومی، ظرفیت حافظه کم/زیاد
- **CH32F205:** USBFS/USBHS، CAN و SDIO
- **CH32F207:** USBFS/USBHS، Ethernet، DVP و FSMC
- **CH32F208:** BLE 5.3 و Ethernet ده مگابیتی

### خانواده‌های هنوز پیاده‌سازی‌نشده

خانواده‌های زیر به‌دلیل تفاوت Peripheralها و قابلیت‌ها برای Crate یا پروژه‌ای جداگانه در نظر گرفته شده‌اند:

- CH57x – BLE 4.2
- CH58x – BLE 5.3
- CH59x – BLE 5.4
- CH569 / CH565 – USB SuperSpeed و SerDes

برای CH58x می‌توانید پروژه آزمایشی [ch58x-hal](https://github.com/ch32-rs/ch58x-hal) را بررسی کنید که HAL همراه با پشتیبانی BLE ارائه می‌دهد.

### خانواده‌های معرفی‌شده و نیازمند اطلاعات بیشتر

- CH564 – USBHS و Ethernet صد مگابیتی
- CH645 – USB HUB و SerDes

## هسته‌های پردازشی QingKe

میکروکنترلرهای RISC-V خانواده CH32 از هسته‌های اختصاصی **QingKe** استفاده می‌کنند. قابلیت‌های مشترک شامل Hardware Push Enable (HPE)، Vector Table Free (VTF) و رابط Debug دو سیمه یا تک سیمه است.

| هسته | مجموعه دستورالعمل و ویژگی |
|---|---|
| V2A | RV32EC + XW؛ بدون PMP و User Mode |
| V2C | RV32EC + XW + Zmmul؛ بدون PMP و User Mode |
| V3A | RV32IMAC؛ بدون PMP |
| V4A | RV32IMAC |
| V4B | RV32IMAC؛ بدون PMP |
| V4C | RV32IMAC + XW |
| V4F | RV32IMAFC + XW |
| V4J | RV32IMAC، دارای I-Cache و XW |

قابلیت‌های واقعی هر هسته باید با مستندات همان تراشه تطبیق داده شوند.

## حداقل نسخه Rust

توسعه پروژه با نسخه جدید **Rust Nightly** انجام می‌شود و انتظار می‌رود نسخه‌های Beta نیز قابل استفاده باشند. برای ساخت پروژه، تنظیمات جاری مخزن و مستندات Crate را بررسی کنید.

## مشارکت در توسعه

مشارکت برای اصلاح نام‌ها، افزودن Registerهای مفقود، رفع خطاها و ترجمه مستندات مورد استقبال است.

### افزودن Peripheral جدید

1. استفاده از فایل‌های SVD اصلاح‌شده در پروژه [ch32-rs](https://github.com/ch32-rs/ch32-rs).
2. استخراج فایل YAML مربوط به Peripheral با اسکریپت d و ابزار chiptool از پروژه Embassy.
3. ویرایش YAML برای تطبیق با Peripheralها و Registerهای تراشه.
4. بررسی Transformها و نمونه‌های پروژه [stm32-data](https://github.com/embassy-rs/stm32-data).
5. ترجیحاً یک Peripheral مشابه را کپی و اصلاح کنید؛ نوشتن YAML از ابتدا توصیه نمی‌شود.

### ویرایش Peripheralهای موجود

- اطلاعات را با دیتاشیت و نمونه‌کد EVT در [openwch](https://github.com/openwch) تطبیق دهید.
- از جدیدترین نسخه دیتاشیت استفاده کنید.
- مطمئن شوید تغییرات باعث اختلال در [ch32-hal](https://github.com/ch32-rs/ch32-hal) نمی‌شوند.

## مجوز استفاده

این پروژه تحت یکی از دو مجوز **MIT** یا **Apache-2.0**، به انتخاب استفاده‌کننده، منتشر شده است. برای جزئیات، فایل‌های مجوز مخزن را بررسی کنید.

</div>

<p align="center"><img src="Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

## English Documentation

# CH32-MetaPAC Project

This repository contains structured, machine-readable data for WCH 32-bit microcontrollers. The data is used to generate peripheral access crates and chip metadata for the Rust ecosystem.

## Overview

[ch32-data](https://github.com/ch32-rs/ch32-data) aims to provide structured data for WCH microcontrollers. Generated peripheral access and chip metadata are published as the [ch32-metapac](https://crates.io/crates/ch32-metapac) crate. The generator implementation is located in [ch32-metapac-gen](ch32-metapac-gen/).

The project is inspired by [stm32-data](https://github.com/embassy-rs/stm32-data). Due to limitations in WCH documentation and tooling, many chip definitions are maintained manually. An include mechanism helps reduce duplication and keeps device-family definitions in separate files.

**Contribution location:** Issues and pull requests for the data should be submitted to the upstream [ch32-rs/ch32-data](https://github.com/ch32-rs/ch32-data) repository, not this generated/nightly metapac repository.

## Data Sources

- Official datasheets: [wch.cn](https://www.wch.cn/) and [wch-ic.com](https://wch-ic.com/)
- SVD files supplied with [MounRiver Studio](https://www.mounriver.com/)
- SVD fixes and patches maintained by [ch32-rs](https://github.com/ch32-rs/ch32-rs)
- Additional information and EVT examples from [openwch](https://github.com/openwch)

Always cross-check peripheral definitions against both the datasheet and EVT example code. Use the latest datasheet revision; the Chinese edition may be newer than the English edition.

## Supported MCU Families

### RISC-V

- CH32V0 – Low-cost devices (V2A/V2C)
- CH32V1 – General purpose (V3A)
- CH32V203 / CH32V303 – General purpose (V4B)
- CH32V305 / CH32V307 / CH32V317 – High-speed interconnect (V4F)
- CH32V407 / CH32V467 – USBHS, Ethernet and PSRAM
- CH32V205 – USBFS/USBHS, USB PD, CAN, QSPI and PIOC
- CH32V208 – BLE 5.3
- CH32X0 – PDUSB
- CH32X315 / CH32X305 – Quad ADC, USB 3.0, USB PD and ARGB
- CH32L1 – Low power and PDUSB
- CH32M103 – CH32L103-based device with a 3-phase gate driver
- CH32M030 – Motor control, half-bridge gate drivers and USB PD
- CH32H4 – Dual-core V3F + V5F, USB 3.0, Gigabit Ethernet and SerDes
- CH643 – RGB driver
- CH641 – USB PD

### ARM Cortex-M3

- CH32F1 – Basic general-purpose devices
- CH32F203 – General purpose, small/large memory variants
- CH32F205 – USBFS/USBHS, CAN and SDIO
- CH32F207 – USBFS/USBHS, Ethernet, DVP and FSMC
- CH32F208 – BLE 5.3 and 10M Ethernet

### Not-yet-implemented families

These families are planned for a separate crate because they use different peripherals and features:

- CH57x – BLE 4.2
- CH58x – BLE 5.3
- CH59x – BLE 5.4
- CH569 / CH565 – USB SuperSpeed and SerDes

For CH58x devices, see the experimental [ch58x-hal](https://github.com/ch32-rs/ch58x-hal) project, which provides a HAL with BLE support.

### Announced families requiring more information

- CH564 – USBHS and 100M Ethernet
- CH645 – USB HUB and SerDes

## QingKe CPU Cores

WCH CH32 RISC-V MCUs use the QingKe CPU IP core. Common features include Hardware Push Enable (HPE), Vector Table Free (VTF), and a two-wire or single-wire debug interface.

| Core | ISA / Features |
|---|---|
| V2A | RV32EC + XW; no PMP or user mode |
| V2C | RV32EC + XW + Zmmul; no PMP or user mode |
| V3A | RV32IMAC; no PMP |
| V4A | RV32IMAC |
| V4B | RV32IMAC; no PMP |
| V4C | RV32IMAC + XW |
| V4F | RV32IMAFC + XW |
| V4J | RV32IMAC, I-cache + XW |

Check the documentation for the specific MCU before relying on any core feature.

## Minimum Supported Rust Version

This project is developed with a recent **nightly** Rust compiler and is expected to work with beta versions. Check the current repository configuration for toolchain details.

## Contributing

Contributions are welcome, including fixes for incorrect names, missing registers, typos and translations.

To add a peripheral:

1. Use the fixed SVD files from [ch32-rs](https://github.com/ch32-rs/ch32-rs).
2. Extract the peripheral YAML using the d script and Embassy's chiptool.
3. Edit the YAML to match the target chip's actual peripherals and registers.
4. Review existing transforms and examples, including [stm32-data](https://github.com/embassy-rs/stm32-data).
5. Prefer copying and adapting an existing peripheral definition over writing raw YAML from scratch.

When editing existing peripherals, cross-check EVT demo code and the latest datasheet, use [openwch](https://github.com/openwch) as a reference, and ensure changes do not break [ch32-hal](https://github.com/ch32-rs/ch32-hal).

Submit Issues and Pull Requests to the upstream data repository:  
https://github.com/ch32-rs/ch32-data

## License

This project is licensed under either the **MIT** or **Apache-2.0** license, at your option. See the repository license files for details.

## Images and Reference Diagrams

The following MES SVG assets are included for consistent repository branding:

| Asset | Purpose |
|---|---|
| [MES-Hero-Banner.svg](Images/GitHub-Assets/MES-Hero-Banner.svg) | Main repository banner |
| [MES-Divider.svg](Images/GitHub-Assets/MES-Divider.svg) | Section separator |
| [MES-Section-Header.svg](Images/GitHub-Assets/MES-Section-Header.svg) | Section heading graphic |
| [MES-Project-Card.svg](Images/GitHub-Assets/MES-Project-Card.svg) | Project showcase panel |
| [MES-Status-Strip.svg](Images/GitHub-Assets/MES-Status-Strip.svg) | Project/status strip |
| [MES-Thank-You-Footer.svg](Images/GitHub-Assets/MES-Thank-You-Footer.svg) | README closing graphic |
| [Assets README](Images/GitHub-Assets/README.md) | Previews, usage examples and technical notes |

<p align="center"><img src="Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="Thank you for visiting MES"></p>

---

## تهیه و تدوین

**معمار الکترونیک صنعت / MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن

- [Telegram](https://t.me/Memar_Electronic)
- [Instagram](https://www.instagram.com/Memar.Electronic)
- [مشاهده سایر آموزش‌ها و پروژه‌ها در GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)
