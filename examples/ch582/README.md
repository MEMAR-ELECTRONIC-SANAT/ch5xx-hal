# مثال‌های CH582 | CH582 Examples

<div dir="rtl" align="right">

## معرفی

این پوشه شامل مثال‌های `no_std` مبتنی بر Rust برای میکروکنترلر **CH582** و کتابخانه‌ی `ch5xx-hal` است. مثال‌ها برای بررسی و راه‌اندازی بخش‌های مختلف تراشه، از GPIO و ADC تا PWM، RTC، SPI، UART و USB در نظر گرفته شده‌اند.

پروژه علاوه بر برنامه‌های پایه، نمونه‌هایی با قابلیت‌های ناهمگام (Async) و USB CDC نیز دارد. این قابلیت‌ها با Featureهای مشخص در `Cargo.toml` فعال می‌شوند.

## ساختار پوشه

| مسیر / فایل | کاربرد |
|---|---|
| `.cargo/config.toml` | هدف کامپایل RISC-V و Runner مربوط به CH582 |
| `Cargo.toml` | وابستگی‌ها و Featureهای اختیاری مانند `spi-async` و `usb-cdc` |
| `build.rs` | اسکریپت ساخت |
| `src/bin/` | فایل‌های اجرایی مستقل؛ هر فایل یک Binary جداگانه است |
| `src/usb_cdc.rs` | کد مشترک مرتبط با USB CDC |

## فهرست مثال‌ها

| نام Binary | توضیحات |
|---|---|
| `hello` | برنامه‌ی پایه برای بررسی راه‌اندازی تراشه و گزارش پیام |
| `adc_auto` | نمونه‌ی اندازه‌گیری خودکار با ADC |
| `adc_temp` | خواندن سنسور دمای داخلی |
| `clock_ladder` | بررسی و تغییر/گزارش وضعیت کلاک |
| `pwm_selftest` | آزمون و بررسی عملکرد PWM |
| `rtc_calendar` | راه‌اندازی و خواندن تقویم RTC |
| `spi_loopback` | آزمون حلقه‌ای SPI به‌صورت همگام |
| `spi_async_loopback` | آزمون حلقه‌ای SPI به‌صورت Async |
| `timer_counter` | نمونه‌ی شمارنده‌ی Timer |
| `uart_loopback` | آزمون Loopback رابط UART |
| `usb_cdc_echo` | دریافت و بازفرستادن داده از طریق USB CDC |
| `usb2_cdc_echo` | نمونه‌ی USB2 CDC Echo |
| `watchdog` | بررسی عملکرد Watchdog |

## قابلیت‌های اختیاری Cargo

برنامه‌های پایه بدون فعال‌کردن Feature اضافی قابل ساخت هستند. دو مثال زیر به Feature نیاز دارند:

- `spi_async_loopback`: با Feature به نام `spi-async`
- `usb_cdc_echo` و `usb2_cdc_echo`: با Feature به نام `usb-cdc`

Feature مربوط به `usb-cdc`، وابستگی‌های Embassy و درایور زمان‌سنج TMR3 را نیز فعال می‌کند.

## پیش‌نیازها

- Rust Toolchain و هدف `riscv32imac-unknown-none-elf`
- کامپوننت `rust-src` برای `build-std`
- ابزار `probe-rs`
- پروگرامر/دیباگر سازگار با CH582، مانند WCH-Link
- برد توسعه‌ی CH582
- برای مثال‌های USB، اتصال USB مناسب به میزبان
- برای تست SPI Loopback، سیم اتصال پایه‌های خروجی و ورودی مطابق کد نمونه

## ساخت و اجرا

دستورها را از پوشه‌ی `examples/ch582` اجرا کنید:

```console
cd examples/ch582

<p align="center"><img src="../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# نمونه‌ی پایه
cargo build --release --bin hello
cargo run --release --bin hello

# نمونه‌ی SPI ناهمگام
cargo run --release --bin spi_async_loopback --features spi-async

# نمونه‌ی USB CDC
cargo run --release --bin usb_cdc_echo --features usb-cdc

# نمونه‌ی USB2 CDC
cargo run --release --bin usb2_cdc_echo --features usb-cdc
```

برای کامپایل همه‌ی Binaryهای عادی:

```console
cargo build --release --bins
```

توجه کنید که Binaryهای دارای `required-features` بدون Feature متناظر در ساخت عمومی وارد نمی‌شوند.

## تنظیم Time Driver

در صورت استفاده از قابلیت‌های Embassy، می‌توانید منبع زمان را با Featureهای زیر انتخاب کنید:

- `time-driver-systick`
- `time-driver-tmr0`
- `time-driver-tmr1`
- `time-driver-tmr2`
- `time-driver-tmr3`

برای نمونه، جهت فعال‌سازی TMR3:

```console
cargo build --release --bin spi_async_loopback --features spi-async,time-driver-tmr3
```

Featureهای زمان‌سنج را متناسب با برنامه‌ی موردنظر انتخاب کنید؛ در صورت نیاز به Embassy، تنظیمات وابستگی‌ها و Featureهای تعریف‌شده در `Cargo.toml` را مبنا قرار دهید.

## پروگرام و دریافت گزارش

Runner در فایل `.cargo/config.toml` به شکل `probe-rs run --chip CH582` تنظیم شده است. اجرای `cargo run` عملیات پروگرام، ریست و اجرای برنامه را انجام می‌دهد و پیام‌های `defmt` را از طریق RTT دریافت می‌کند.

اگر چند WCH-Link متصل است، Probe موردنظر را مشخص کنید:

```console
PROBE_RS_PROBE=<VID:PID:SERIAL> cargo run --release --bin hello
```

## نکات سخت‌افزاری

- مثال‌های Loopback به اتصال فیزیکی پایه‌ی TX به RX یا MOSI به MISO مطابق توضیح داخل کد نیاز دارند؛ پیش از اجرا، فایل همان مثال را بررسی کنید.
- مثال‌های USB CDC به اتصال USB تراشه به میزبان نیاز دارند؛ اتصال Debug Probe به‌تنهایی جایگزین کابل USB میزبان نیست.
- قبل از پروگرام، از انتخاب تراشه‌ی صحیح CH582 در `probe-rs` اطمینان حاصل کنید.
- پایه‌های مورد استفاده در مثال‌ها را با شماتیک برد و پیکربندی Alternate Function تراشه تطبیق دهید.

## منابع مرتبط

- [مخزن اصلی ch5xx-hal](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [پوشه‌ی همه‌ی مثال‌ها](../)
- [مستندات probe-rs](https://probe.rs/)
- [مستندات Embassy](https://embassy.dev/)
- [زبان برنامه‌نویسی Rust](https://www.rust-lang.org/)

</div>

<div dir="ltr" align="left">

## Overview

This directory contains Rust `no_std` examples for the **CH582** microcontroller using the `ch5xx-hal` crate. The examples demonstrate peripheral initialization and testing, including GPIO, ADC, PWM, RTC, SPI, UART, and USB.

In addition to basic peripheral examples, the project includes asynchronous (Async) and USB CDC applications. These are enabled through explicit Cargo features in `Cargo.toml`.

## Directory layout

| Path / file | Purpose |
|---|---|
| `.cargo/config.toml` | RISC-V target and CH582 runner configuration |
| `Cargo.toml` | Dependencies and optional features such as `spi-async` and `usb-cdc` |
| `build.rs` | Build script |
| `src/bin/` | Independent executable binaries; each source file defines a separate binary |
| `src/usb_cdc.rs` | Shared USB CDC implementation |

## Example binaries

| Binary | Description |
|---|---|
| `hello` | Basic application for checking chip startup and logging |
| `adc_auto` | Automatic ADC measurement example |
| `adc_temp` | Reads the internal temperature sensor |
| `clock_ladder` | Clock configuration and status inspection |
| `pwm_selftest` | PWM operation test |
| `rtc_calendar` | RTC calendar setup and readback |
| `spi_loopback` | Blocking SPI loopback test |
| `spi_async_loopback` | Asynchronous SPI loopback test |
| `timer_counter` | Timer counter example |
| `uart_loopback` | UART loopback test |
| `usb_cdc_echo` | USB CDC receive-and-echo application |
| `usb2_cdc_echo` | USB2 CDC echo application |
| `watchdog` | Watchdog operation test |

## Optional Cargo features

The basic examples can be built without additional features. The following binaries require explicit features:

- `spi_async_loopback`: requires `spi-async`
- `usb_cdc_echo` and `usb2_cdc_echo`: require `usb-cdc`

The `usb-cdc` feature also enables the Embassy dependencies and the TMR3 time driver.

## Prerequisites

- Rust toolchain and the `riscv32imac-unknown-none-elf` target
- The `rust-src` component for `build-std`
- `probe-rs`
- A CH582-compatible debug probe, such as WCH-Link
- A CH582 development board
- A suitable USB host connection for USB examples
- Jumper wires for SPI loopback tests, as required by the example source

## Build and run

Run commands from `examples/ch582`:

```console
cd examples/ch582

# Basic example
cargo build --release --bin hello
cargo run --release --bin hello

# Asynchronous SPI example
cargo run --release --bin spi_async_loopback --features spi-async

# USB CDC example
cargo run --release --bin usb_cdc_echo --features usb-cdc

# USB2 CDC example
cargo run --release --bin usb2_cdc_echo --features usb-cdc
```

Build all regular binaries with:

```console
cargo build --release --bins
```

Binaries declaring `required-features` are excluded from a general build unless their required feature is enabled.

## Selecting the Embassy time driver

When using Embassy functionality, the time source can be selected with one of these features:

- `time-driver-systick`
- `time-driver-tmr0`
- `time-driver-tmr1`
- `time-driver-tmr2`
- `time-driver-tmr3`

For example, to enable TMR3:

```console
cargo build --release --bin spi_async_loopback --features spi-async,time-driver-tmr3
```

Choose the time-driver feature according to the application. The feature definitions and dependency requirements in `Cargo.toml` are authoritative.

## Flashing and logging

The local Cargo runner is configured as `probe-rs run --chip CH582`. Running `cargo run` flashes, resets, and starts the application while capturing `defmt` messages over RTT.

If multiple WCH-Link probes are connected, select the intended probe:

```console
PROBE_RS_PROBE=<VID:PID:SERIAL> cargo run --release --bin hello
```

## Hardware notes

- Loopback examples require the relevant physical connection, such as TX-to-RX or MOSI-to-MISO, as specified by the source code. Check the individual example before running it.
- USB CDC examples require the chip's USB interface to be connected to a USB host. A debug probe connection alone is not a substitute for the USB host cable.
- Verify that `probe-rs` is configured for CH582 before flashing.
- Check the board schematic and the chip's alternate-function configuration before wiring example pins.

## Related resources

- [Main ch5xx-hal repository](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [All examples](../)
- [probe-rs documentation](https://probe.rs/)
- [Embassy documentation](https://embassy.dev/)
- [The Rust programming language](https://www.rust-lang.org/)

</div>

## تصاویر و دیاگرام‌های راهنما | Images and Diagrams

<div align="center">

![MES Animated Logo](../../Images/GitHub-Assets/MES_Animated_Logo_640x480.svg)

</div>


<p align="center"><img src="../../Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="MES Thank You Footer"></p>

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

