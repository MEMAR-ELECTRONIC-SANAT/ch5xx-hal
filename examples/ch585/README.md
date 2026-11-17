# مثال‌های CH585 | CH585 Examples

<div dir="rtl" align="right">

## معرفی

این پوشه مجموعه‌ای از برنامه‌های نمونه‌ی `no_std` مبتنی بر Rust برای میکروکنترلر **CH585** و کتابخانه‌ی `ch5xx-hal` را در بر می‌گیرد. مثال‌ها بخش‌های مختلف تراشه از جمله GPIO، ADC، کلاک، PWM، I2C، SPI، UART، RTC، Timer، DMA، USB و Watchdog را پوشش می‌دهند.

در این مجموعه هم مثال‌های ساده‌ی راه‌اندازی Peripheralها و هم برنامه‌های مبتنی بر **Embassy Async** وجود دارد. چند مثال نیز برای نمایش و آزمون OLED مبتنی بر SSD1306 و ارتباط USB طراحی شده‌اند.

## ساختار پوشه

| مسیر / فایل | کاربرد |
|---|---|
| `.cargo/config.toml` | تنظیم هدف RISC-V، ویژگی‌های معماری و Runner مربوط به CH585 |
| `Cargo.toml` | وابستگی‌ها، Featureهای Time Driver و تنظیم نسخه‌ی توسعه‌ای Embassy |
| `build.rs` | اسکریپت ساخت |
| `src/bin/` | برنامه‌های اجرایی مستقل |
| `src/bin/i2c_oled.rs` و `i2c_oled_async.rs` | نمونه‌های نمایشگر OLED با I2C همگام و ناهمگام |
| `src/bin/usb_cdc_echo.rs` و فایل‌های USBHS | نمونه‌های ارتباط USB Full-Speed و High-Speed |

## فهرست برنامه‌ها

### GPIO و کلاک

| Binary | توضیحات |
|---|---|
| `blinky` | راه‌اندازی GPIO خروجی و چشمک‌زدن LEDها با تأخیر |
| `gpio_in` | خواندن کلیدهای ورودی فعال‌پایین S1 و S2 و کنترل LEDها |
| `gpio_async` | دریافت رخداد کلیدها از طریق وقفه‌ی GPIO |
| `gpio_async_loopback` | آزمون لبه‌های ورودی/خروجی با اتصال PA14 به PA15 |
| `clk_set` | تنظیم کلاک روی 24MHz و گزارش وضعیت آن |
| `defmt_rtt` | نمایش گزارش‌های `defmt` از طریق RTT |

### ADC و PWM

| Binary | توضیحات |
|---|---|
| `adc_temp` | اندازه‌گیری دمای داخلی |
| `adc_pin` | نمونه‌برداری ADC از پایه‌ی PA4 |
| `adc_scan_dma` | اسکن سه کانال ADC با DMA داخلی ADC |
| `pwm_out` | تولید PWM روی PA12 و تغییر تدریجی Duty Cycle |

### ارتباطات و نمایشگر

| Binary | توضیحات |
|---|---|
| `uart_loopback` | آزمون داخلی UART0 بدون سیم‌کشی خارجی |
| `uart_echo` | دریافت و ارسال مجدد داده از UART3 روی PA4/PA5 |
| `i2c_scan` | اسکن آدرس‌های پاسخ‌گو روی I2C0 |
| `i2c_oled` | نمایش متن و شکل متحرک روی SSD1306 |
| `i2c_oled_async` | انتقال فریم‌های OLED با I2C وقفه‌محور |
| `spi_loopback` | آزمون Loopback رابط SPI0 |
| `spi_async_loopback` | آزمون SPI ناهمگام و انتقال DMA |

### زمان، RTC، USB و مدیریت توان

| Binary | توضیحات |
|---|---|
| `embassy_time` | اجرای Taskهای زمان‌بندی‌شده با Time Driver مبتنی بر SysTick |
| `embassy_time_tmr` | اجرای Taskها با Time Driver مبتنی بر Timer |
| `timer_dma_async` | آزمون وقفه‌ی Timer، انتظار DMA و لغو عملیات |
| `rtc_calendar` | تنظیم RTC، خواندن زمان و بررسی Alarm و Timer |
| `rtc_oled` | نمایش تاریخ و ساعت روی OLED |
| `sleep_wake` | ورود به حالت‌های Halt/Sleep و بیداری با RTC |
| `watchdog` | بررسی Window Watchdog و مسیر تغذیه‌ی آن |
| `usb_cdc_echo` | USB CDC ACM با سرعت Full-Speed |
| `usbhs_cdc_echo` | USB CDC ACM با سرعت High-Speed |
| `usb_endpoints` | آزمون Endpointهای 1 تا 7 در USB Full-Speed |
| `usbhs_endpoints` | آزمون Endpointهای 1 تا 7 در USB High-Speed |

## پیش‌نیازها

- Rust Toolchain و کامپوننت `rust-src`
- ابزار `probe-rs`
- پروگرامر/دیباگر سازگار با CH585
- برد توسعه‌ی CH585
- کابل USB و میزبان برای مثال‌های USB
- نمایشگر SSD1306 برای مثال‌های OLED
- سیم جامپر برای تست‌های Loopback مطابق توضیحات هر برنامه

## ساخت و اجرا

دستورها را از پوشه‌ی `examples/ch585` اجرا کنید:

```console
cd examples/ch585

# اجرای مثال GPIO
cargo run --release --bin blinky

# ساخت همه‌ی برنامه‌ها با تنظیم پیش‌فرض
cargo build --release --bins
```

Runner در `.cargo/config.toml` به صورت `probe-rs run --chip CH585` تنظیم شده است. اجرای `cargo run` برنامه را پروگرام و ریست می‌کند و خروجی `defmt` را از طریق RTT دریافت می‌کند.

## انتخاب Time Driver برای Embassy

به‌صورت پیش‌فرض، Feature مربوط به `time-driver-systick` فعال است. برای استفاده از Timer به‌عنوان منبع زمان، می‌توانید یکی از Featureهای `time-driver-tmr0` تا `time-driver-tmr3` را انتخاب کنید.

برای نمونه، اجرای مثال مبتنی بر TMR0:

```console
cargo run --release --bin embassy_time_tmr --no-default-features --features time-driver-tmr0
```

برای ساخت همه‌ی Binaryها با Time Driver مبتنی بر TMR0:

```console
cargo build --release --bins --no-default-features --features time-driver-tmr0
```

نکته: برنامه‌ی `embassy_time_tmr` عمداً استفاده از SysTick را نمی‌پذیرد؛ بنابراین ساخت همه‌ی Binaryها با Feature پیش‌فرض ممکن است به‌دلیل بررسی Feature همین برنامه متوقف شود. برای ساخت یکپارچه، Time Driver مبتنی بر TMR را صریحاً انتخاب کنید.

## معماری هسته و تنظیمات کامپایل

هسته‌ی QingKe V3C در CH585 از هدف `riscv32imc-unknown-none-elf` استفاده می‌کند. این تنظیم با هدف رایج `riscv32imac` یکسان نیست؛ زیرا نباید بدون بررسی، دستورهای Atomic مربوط به افزونه‌ی A در خروجی کامپایلر تولید شوند. برای مدیریت عملیات Atomic در وابستگی‌ها از `portable-atomic` و Critical Section استفاده شده است.

در فایل `.cargo/config.toml` ویژگی‌های معماری موردنیاز این تراشه تنظیم شده‌اند. هشدارهای کامپایل مربوط به ویژگی اختصاصی `xwchc` را با تغییر خودسرانه‌ی Target Featureها برطرف نکنید؛ تنظیم فعلی بر اساس رفتار هسته و آزمون سخت‌افزاری پروژه انتخاب شده است.

## نکات سخت‌افزاری و سیم‌بندی

- `gpio_async_loopback`: پایه‌ی PA14 را به PA15 متصل کنید.
- `spi_loopback` و `spi_async_loopback`: برای Loopback، PA14 را به PA15 متصل کنید.
- `i2c_oled` و `i2c_oled_async`: نمایشگر SSD1306 با آدرس پیش‌فرض `0x3C) لازم دارند؛ پایه‌های I2C0 در کد نمونه PB13/PB12 هستند.
- `uart_echo`: رابط UART3 روی PA4/PA5 با تنظیم 115200 و قالب 8N1 استفاده می‌شود.
- `usb_cdc_echo`: از PB11/PB10 استفاده می‌کند و به اتصال USB میزبان نیاز دارد.
- `usbhs_cdc_echo`: رابط USB High-Speed از PB13/PB12 استفاده می‌کند.
- `pwm_out`: خروجی PWM روی PA12 قرار دارد و برای مشاهده‌ی شکل موج می‌توان LED خارجی را با مقاومت محدودکننده‌ی جریان متصل کرد.
- `sleep_wake`: هنگام ورود به Sleep ممکن است ارتباط RTT قطع شود؛ برای اجرای این مثال، توضیحات اختصاصی README و پیام‌های برنامه را در نظر بگیرید.

## منابع مرتبط

- [مخزن اصلی ch5xx-hal](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [پوشه‌ی همه‌ی مثال‌ها](../)
- [مستندات probe-rs](https://probe.rs/)
- [مستندات Embassy](https://embassy.dev/)
- [مستندات Rust](https://www.rust-lang.org/)

</div>

<div dir="ltr" align="left">

## Overview

This directory contains Rust `no_std` examples for the **CH585** microcontroller using the `ch5xx-hal` crate. The examples cover GPIO, ADC, clock configuration, PWM, I2C, SPI, UART, RTC, timers, DMA, USB, and watchdog functionality.

The collection includes basic peripheral demonstrations as well as **Embassy Async** applications. It also provides SSD1306 OLED and USB communication examples.

## Directory layout

| Path / file | Purpose |
|---|---|
| `.cargo/config.toml` | RISC-V target, architecture features, and CH585 runner |
| `Cargo.toml` | Dependencies, time-driver features, and the pinned Embassy development revision |
| `build.rs` | Build script |
| `src/bin/` | Independent executable applications |
| `src/bin/i2c_oled.rs` and `i2c_oled_async.rs` | Blocking and asynchronous I2C OLED examples |
| `src/bin/usb_cdc_echo.rs` and USBHS files | Full-Speed and High-Speed USB examples |

## Example binaries

### GPIO and clock

| Binary | Description |
|---|---|
| `blinky` | GPIO output and LED blinking with a blocking delay |
| `gpio_in` | Reads active-low S1/S2 buttons and controls LEDs |
| `gpio_async` | Handles button events through GPIO interrupts |
| `gpio_async_loopback` | GPIO edge test using a PA14-to-PA15 jumper |
| `clk_set` | Configures the clock to 24 MHz and reports its state |
| `defmt_rtt` | Sends `defmt` logs over RTT |

### ADC and PWM

| Binary | Description |
|---|---|
| `adc_temp` | Internal temperature measurement |
| `adc_pin` | ADC conversion on PA4 |
| `adc_scan_dma` | Three-channel ADC scan using the ADC-local DMA engine |
| `pwm_out` | PWM output on PA12 with a changing duty cycle |

### Communication and display

| Binary | Description |
|---|---|
| `uart_loopback` | Internal UART0 loopback; no external wiring |
| `uart_echo` | UART3 echo on PA4/PA5 at 115200 8N1 |
| `i2c_scan` | Scans responding addresses on I2C0 |
| `i2c_oled` | Text and animated graphics on an SSD1306 |
| `i2c_oled_async` | Interrupt-driven I2C OLED frame transfers |
| `spi_loopback` | SPI0 loopback test |
| `spi_async_loopback` | Asynchronous SPI and DMA loopback test |

### Timing, RTC, USB, and power management

| Binary | Description |
|---|---|
| `embassy_time` | Scheduled tasks using the SysTick time driver |
| `embassy_time_tmr` | Scheduled tasks using a timer-based time driver |
| `timer_dma_async` | Timer interrupt binding, DMA waits, and cancellation |
| `rtc_calendar` | RTC setup, readback, alarm, and timer checks |
| `rtc_oled` | Date and time display on an OLED |
| `sleep_wake` | Halt/Sleep entry and RTC wake-up |
| `watchdog` | Window watchdog and feed-path test |
| `usb_cdc_echo` | Full-Speed USB CDC ACM |
| `usbhs_cdc_echo` | High-Speed USB CDC ACM |
| `usb_endpoints` | Exercises USB Full-Speed endpoints 1 through 7 |
| `usbhs_endpoints` | Exercises USB High-Speed endpoints 1 through 7 |

## Prerequisites

- Rust toolchain and the `rust-src` component
- `probe-rs`
- A CH585-compatible debug probe
- A CH585 development board
- USB cable and host for USB examples
- SSD1306 display for OLED examples
- Jumper wires for loopback tests, as specified by each application

## Build and run

Run commands from `examples/ch585`:

```console
cd examples/ch585

# Run the GPIO example
cargo run --release --bin blinky

# Build all binaries with the default configuration
cargo build --release --bins
```

The runner in `.cargo/config.toml` is configured as `probe-rs run --chip CH585`. Running `cargo run` flashes and resets the target and captures `defmt` output over RTT.

## Selecting the Embassy time driver

The default feature is `time-driver-systick`. To use a timer as the time source, select one of `time-driver-tmr0` through `time-driver-tmr3`.

For example, run the TMR0-based example:

```console
cargo run --release --bin embassy_time_tmr --no-default-features --features time-driver-tmr0
```

Build all binaries with the TMR0 time driver:

```console
cargo build --release --bins --no-default-features --features time-driver-tmr0
```

Note: `embassy_time_tmr` intentionally rejects the SysTick driver. Therefore, building every binary with the default feature may stop at this example's feature guard. Select a TMR-based driver explicitly for an all-binaries build.

## Core architecture and compiler configuration

The CH585 QingKe V3C core uses the `riscv32imc-unknown-none-elf` target. This is not interchangeable with the common `riscv32imac` target: Atomic instructions from the A extension must not be emitted without verifying hardware support. The project uses `portable-atomic` and critical sections to provide the required atomic operations in its dependencies.

Architecture-specific options are configured in `.cargo/config.toml`. Do not remove or alter the WCH-specific `xwchc` target option merely to silence compiler warnings; the current configuration reflects the core's behavior and the project's hardware testing.

## Hardware and wiring notes

- `gpio_async_loopback`: connect PA14 to PA15.
- `spi_loopback` and `spi_async_loopback`: connect PA14 to PA15 for loopback.
- `i2c_oled` and `i2c_oled_async`: require an SSD1306 at the default address `0x3C`; the example uses PB13/PB12 for I2C0.
- `uart_echo`: uses UART3 on PA4/PA5 at 115200, 8N1.
- `usb_cdc_echo`: uses PB11/PB10 and requires a USB host connection.
- `usbhs_cdc_echo`: uses PB13/PB12 for the USB High-Speed interface.
- `pwm_out`: outputs PWM on PA12; an external LED with a current-limiting resistor can be used to observe the output.
- `sleep_wake`: RTT may disconnect when the core enters Sleep. Follow the example-specific README notes and application log messages.

## Related resources

- [Main ch5xx-hal repository](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [All examples](../)
- [probe-rs documentation](https://probe.rs/)
- [Embassy documentation](https://embassy.dev/)
- [Rust documentation](https://www.rust-lang.org/)

</div>

## تصاویر و دیاگرام‌های راهنما | Images and Diagrams

<div align="center">

![MES Animated Logo](../../Images/GitHub-Assets/MES_Animated_Logo_640x480.svg)

</div>

## تهیه و تدوین | Credits

<div dir="rtl" align="right">

**معمار الکترونیک صنعت (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن

- [کانال تلگرام](https://t.me/Memar_Electronic)
- [صفحه اینستاگرام](https://www.instagram.com/Memar.Electronic)
- [مخزن GitHub سازمان](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

<div dir="ltr" align="left">

**MEMAR ELECTRONIC SANAT (MES)**  
Your partner in designing and building reliable circuits.

- [Telegram](https://t.me/Memar_Electronic)
- [Instagram](https://www.instagram.com/Memar.Electronic)
- [GitHub Organization](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

