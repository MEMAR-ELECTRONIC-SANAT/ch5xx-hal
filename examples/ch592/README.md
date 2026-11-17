# مثال‌های CH592 | CH592 Examples

<div dir="rtl" align="right">

## معرفی

این پوشه مجموعه‌ای از مثال‌های Rust با ساختار `no_std` برای خانواده‌ی **CH59x** و به‌طور مشخص **CH592** را شامل می‌شود. این برنامه‌ها برای ارزیابی Peripheralهای مختلف کتابخانه‌ی `ch5xx-hal` و آزمودن قابلیت‌های سخت‌افزاری تراشه طراحی شده‌اند.

نمونه‌ها شامل ADC، کلاک و PLL، PWM، RTC، SPI، Timer، TouchKey، UART، USB، Watchdog و مدیریت توان هستند. تعدادی از برنامه‌ها آزمون داخلی یا Loopback دارند و نتیجه‌ی تست را با پیام‌های `SELFTEST PASS` یا `SELFTEST FAIL` گزارش می‌کنند.

## ساختار پوشه

| مسیر / فایل | کاربرد |
|---|---|
| `.cargo/config.toml` | انتخاب Target، تنظیم Runner و متغیرهای محیطی |
| `Cargo.toml` | وابستگی‌ها و Featureهای Time Driver |
| `build.rs` | اسکریپت ساخت |
| `src/bin/` | فایل‌های اجرایی مستقل هر مثال |

## فهرست مثال‌ها

| Binary | توضیحات |
|---|---|
| `hello` | برنامه‌ی پایه، کلاک پیش‌فرض 6.4MHz، تأخیر و گزارش `defmt` |
| `adc_auto` | نمونه‌برداری زمان‌بندی‌شده از دما با DMA داخلی ADC و بررسی نتیجه |
| `adc_scan` | اسکن ۱۲ کانال ADC در سه مرحله‌ی DMA؛ بدون نیاز به سیم‌کشی خارجی |
| `adc_temp` | یک بار خواندن سنسور دمای داخلی |
| `clk_pll48` | تولید کلاک 48MHz با PLL و بررسی تنظیمات Flash |
| `embassy_time` | راه‌اندازی Time Driver برای Embassy |
| `i2c_scan` | اسکن آدرس‌های I2C0 روی PB15/PB14 |
| `pwm_16bit` | تنظیم PWM با دوره و Duty شانزده‌بیتی روی PA13 و اندازه‌گیری از PA14 |
| `pwm_out` | آزمون دوره، Duty و اختلاف فاز PWM5 روی PA13 با اندازه‌گیری PA14 |
| `rtc_calendar` | تقویم RTC، آلارم یک‌باره و تایمر بازه‌ای |
| `sleep_wake` | آزمون `power::halt` و `power::sleep` با بیداری توسط RTC |
| `spi_async_loopback` | آزمون SPI0 ناهمگام و DMA داخلی |
| `spi_loopback` | آزمون SPI0 در Mode 0 و Mode 3 |
| `timer_counter` | بررسی شمارنده‌های Timer در بلوک‌های TMR0 و TMR2 |
| `touchkey` | آزمون ورودی لمسی TouchKey |
| `touchkey_led` | استفاده از TouchKey برای کنترل LED |
| `uart_loopback` | آزمون داخلی UART0 |
| `usb_cdc_echo` | دستگاه USB Full-Speed CDC ACM و بازفرستادن داده‌ی دریافتی |
| `watchdog` | بررسی Window Watchdog، مسیر Feed و تشخیص باتری |

## پیش‌نیازها

- Rust Toolchain و کامپوننت `rust-src`
- هدف کامپایل `riscv32imc-unknown-none-elf`
- ابزار `probe-rs`
- پروگرامر/دیباگر WCH-Link سازگار با CH592
- برد توسعه‌ی CH592 یا برد EVT خانواده‌ی CH59x
- کابل USB میزبان برای مثال `usb_cdc_echo`
- سیم جامپر برای تست‌های SPI و PWM مطابق توضیحات زیر

## ساخت و اجرای مثال

از پوشه‌ی `examples/ch592` دستورهای زیر را اجرا کنید:

```console
cd examples/ch592

# کامپایل مثال پایه
cargo build --release --bin hello

# پروگرام، ریست، اجرا و دریافت گزارش RTT
cargo run --release --bin hello
```

Runner در تنظیمات Cargo با فرمان `probe-rs run --chip CH592` تعریف شده است. در نتیجه `cargo run` هر سه مرحله‌ی پروگرام، ریست و اجرا را انجام می‌دهد و گزارش‌های `defmt` را از RTT دریافت می‌کند.

### انتخاب WCH-Link در صورت اتصال چند Probe

```console
PROBE_RS_PROBE=<VID:PID:SERIAL> cargo run --release --bin hello
```

اگر متغیر بالا تنظیم نشود، `probe-rs` اولین Probe را انتخاب می‌کند. پیش از پروگرام، مطمئن شوید تراشه‌ی متصل‌شده CH592 است.

## انتخاب Time Driver

به‌صورت پیش‌فرض `time-driver-systick` فعال است. برای انتخاب Timer به‌عنوان منبع زمان Embassy می‌توانید از Featureهای زیر استفاده کنید:

- `time-driver-tmr0`
- `time-driver-tmr1`
- `time-driver-tmr2`
- `time-driver-tmr3`

برای نمونه، اجرای `embassy_time` با TMR1:

```console
cargo run --release --bin embassy_time --no-default-features --features time-driver-tmr1
```

هر چهار Timer قابلیت استفاده به‌عنوان منبع زمان Embassy را دارند. در CH592 برخی بلوک‌های Timer فاقد رجیسترهای DMA محلی هستند؛ APIهای DMA در HAL برای نمونه‌های فاقد این قابلیت در زمان کامپایل محدود می‌شوند.

## آزمون‌های Loopback و اتصالات سخت‌افزاری

- **SPI Loopback:** در مثال `spi_loopback` پایه‌ی PA14 (MOSI) را به PA15 (MISO) وصل کنید. در برد EVT، محل اتصال در توضیحات کد با P2 مشخص شده است.
- **SPI Async:** مثال `spi_async_loopback` نیز از اتصال PA14 به PA15 استفاده می‌کند.
- **PWM:** در مثال‌های `pwm_out` و `pwm_16bit`، پایه‌ی PA13 را به PA14 متصل کنید تا سیگنال خروجی اندازه‌گیری شود؛ در برد مرجع، این اتصال با P9 pin 9 به pin 10 مشخص شده است.
- **USB CDC:** مثال `usb_cdc_echo` به اتصال کانکتور USB-C برد به میزبان نیاز دارد. پروگرامر Debug به‌تنهایی VBUS یا اتصال USB میزبان را فراهم نمی‌کند.
- **I2C:** پایه‌های PB14/PB15 در این تراشه با رابط Debug دو سیمه نیز مرتبط هستند. در زمان اتصال `probe-rs` ممکن است اسکن I2C با خطاهای Arbitration مواجه شود؛ برای آزمون واقعی I2C، شرایط Debug و اتصال Slave را مطابق توضیحات پروژه تنظیم کنید.
- **TouchKey:** برای ارزیابی عملکرد TouchKey، الکترود و طراحی برد را مطابق الزامات دیتاشیت و سخت‌افزار واقعی بررسی کنید.

## نکات مهم درباره Sleep و RTT

در مثال `sleep_wake`، هنگام توقف هسته Probe قادر به دسترسی عادی به آن نیست؛ بنابراین نشست RTT در اولین ورود به Sleep خاتمه می‌یابد. نتیجه‌ی آزمون در SRAM نگهداری می‌شود.

برای اجرای این مثال، مطابق راهنمای موجود در کد از دستور زیر استفاده کنید:

```console
cargo run --release --bin sleep_wake --no-default-features
```

آدرس حافظه‌ای که برنامه پیش از ورود به Sleep چاپ می‌کند، برای خواندن نتیجه با `probe-rs read` استفاده می‌شود.

## نکات معماری و کامپایل

- هدف کامپایل این پوشه `riscv32imc-unknown-none-elf` است.
- تنظیمات `Cargo.toml` از `portable-atomic` و Critical Section استفاده می‌کند؛ هدف را بدون بررسی به `riscv32imac` تغییر ندهید.
- Feature مربوط به `+b` برای CH592 فعال نشده است؛ فعال‌سازی آن می‌تواند باعث اجرای دستور نامعتبر روی این هسته شود.
- در این مثال‌ها گزارش‌ها از طریق `defmt` و RTT دریافت می‌شوند.

## منابع مرتبط

- [مخزن اصلی ch5xx-hal](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [پوشه‌ی همه‌ی مثال‌ها](../)
- [مستندات probe-rs](https://probe.rs/)
- [مستندات Embassy](https://embassy.dev/)
- [مستندات Rust](https://www.rust-lang.org/)

</div>

<div dir="ltr" align="left">

## Overview

This directory contains Rust `no_std` examples for the **CH59x** family, specifically **CH592**. The applications are intended to evaluate the peripherals provided by `ch5xx-hal` and exercise the device's hardware features.

The examples cover ADC, clock and PLL, PWM, RTC, SPI, timers, TouchKey, UART, USB, watchdog, and power management. Several applications include internal or loopback tests and report their result using `SELFTEST PASS` or `SELFTEST FAIL` messages.

## Directory layout

| Path / file | Purpose |
|---|---|
| `.cargo/config.toml` | Target selection, runner configuration, and environment variables |
| `Cargo.toml` | Dependencies and time-driver features |
| `build.rs` | Build script |
| `src/bin/` | Independent executable example files |

## Example binaries

| Binary | Description |
|---|---|
| `hello` | Basic application, default 6.4 MHz clock, delay, and `defmt` logging |
| `adc_auto` | Timed temperature sampling using the ADC-local DMA engine, with self-check |
| `adc_scan` | Twelve-channel ADC scan over three DMA passes; no external wiring |
| `adc_temp` | Single conversion from the internal temperature sensor |
| `clk_pll48` | 48 MHz PLL clock setup and Flash timing readback |
| `embassy_time` | Embassy time-driver example |
| `i2c_scan` | I2C0 address scan on PB15/PB14 |
| `pwm_16bit` | 16-bit PWM period and duty on PA13, measured on PA14 |
| `pwm_out` | PWM5 period, duty, and stagger test on PA13, measured on PA14 |
| `rtc_calendar` | RTC calendar, one-shot alarm, and interval timer |
| `sleep_wake` | `power::halt` and `power::sleep` with RTC wake-up |
| `spi_async_loopback` | Asynchronous SPI0 and local-DMA loopback |
| `spi_loopback` | SPI0 loopback in Mode 0 and Mode 3 |
| `timer_counter` | Timer counters on TMR0 and TMR2 blocks |
| `touchkey` | TouchKey input test |
| `touchkey_led` | Uses TouchKey input to control an LED |
| `uart_loopback` | Internal UART0 loopback test |
| `usb_cdc_echo` | USB Full-Speed CDC ACM device that echoes received data |
| `watchdog` | Window watchdog, feed path, and battery detector test |

## Prerequisites

- Rust toolchain and the `rust-src` component
- The `riscv32imc-unknown-none-elf` compilation target
- `probe-rs`
- A CH592-compatible WCH-Link debug probe
- A CH592 development board or CH59x EVT board
- USB host cable for `usb_cdc_echo`
- Jumper wires for SPI and PWM tests as described below

## Build and run

Run commands from `examples/ch592`:

```console
cd examples/ch592

# Build the basic example
cargo build --release --bin hello

# Flash, reset, run, and capture RTT logs
cargo run --release --bin hello
```

The Cargo runner is configured as `probe-rs run --chip CH592`. Therefore, `cargo run` performs flashing, reset, and execution while capturing `defmt` output over RTT.

### Selecting a WCH-Link when multiple probes are connected

```console
PROBE_RS_PROBE=<VID:PID:SERIAL> cargo run --release --bin hello
```

If the variable is not set, `probe-rs` selects the first available probe. Verify that the connected target is CH592 before flashing.

## Selecting the time driver

The default feature is `time-driver-systick`. To use a timer as the Embassy time source, select one of:

- `time-driver-tmr0`
- `time-driver-tmr1`
- `time-driver-tmr2`
- `time-driver-tmr3`

For example, run `embassy_time` with TMR1:

```console
cargo run --release --bin embassy_time --no-default-features --features time-driver-tmr1
```

All four timer instances can be used as Embassy time drivers. Some CH592 timer blocks do not include timer-local DMA registers; the HAL compile-time API constraints prevent DMA entry points from being used on instances without that hardware capability.

## Loopback tests and hardware connections

- **SPI loopback:** For `spi_loopback`, connect PA14 (MOSI) to PA15 (MISO). The EVT board connection is identified as P2 in the example notes.
- **SPI Async:** `spi_async_loopback` uses the same PA14-to-PA15 connection.
- **PWM:** For `pwm_out` and `pwm_16bit`, connect PA13 to PA14 to measure the output signal. On the reference board this is identified as P9 pin 9 to pin 10.
- **USB CDC:** `usb_cdc_echo` requires the board's USB-C connector to be connected to a host. The debug probe alone does not provide VBUS or a USB host connection.
- **I2C:** PB14/PB15 are also associated with the two-wire debug interface on this device. An I2C scan may report arbitration-loss flags while `probe-rs` is attached. For an actual I2C test, configure the debug interface and connect a slave as described by the project.
- **TouchKey:** Evaluate the TouchKey electrode and PCB layout against the datasheet requirements and the actual hardware design.

## Sleep and RTT notes

In `sleep_wake`, the probe cannot normally access the core while it is stopped. The RTT session therefore ends at the first Sleep entry, and the test result is retained in SRAM.

Run this example as documented by the source:

```console
cargo run --release --bin sleep_wake --no-default-features
```

The memory address printed before the first Sleep entry can be used to read the result with `probe-rs read`.

## Architecture and build notes

- This directory targets `riscv32imc-unknown-none-elf`.
- `Cargo.toml` uses `portable-atomic` and critical sections; do not switch to `riscv32imac` without validating the core and generated instructions.
- The `+b` target feature is not enabled for CH592; enabling it may cause unsupported instructions to execute on this core.
- Example logs are provided through `defmt` over RTT.

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

