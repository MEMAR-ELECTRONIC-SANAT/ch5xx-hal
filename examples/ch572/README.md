# مثال‌های CH572 | CH572 Examples

<div dir="rtl" align="right">

## معرفی

این پوشه شامل برنامه‌های نمونه‌ی `no_std` برای استفاده از کتابخانه‌ی `ch5xx-hal` روی میکروکنترلرهای **CH572 / CH570** با هسته‌ی **QingKe V3A** است. در وضعیت فعلی، یک برنامه‌ی خودآزمایی برای بررسی رجیسترها و عملکرد کانال‌های PWM در این پوشه قرار دارد.

هدف این مثال، فراهم‌کردن نقطه‌ی شروعی برای بررسی PWM و آشنایی با ساختار پروژه‌های Embedded Rust در خانواده‌ی CH57x است.

## ساختار پوشه

| مسیر / فایل | کاربرد |
|---|---|
| `.cargo/config.toml` | انتخاب هدف RISC-V، تنظیم `build-std` و معرفی `probe-rs` به‌عنوان Runner |
| `Cargo.toml` | وابستگی‌ها، قابلیت‌های HAL و تنظیمات ساخت |
| `build.rs` | اسکریپت ساخت پروژه |
| `src/bin/pwm_selftest.rs` | برنامه‌ی بررسی PWM1 تا PWM5 و خواندن مقادیر رجیسترها |

## معرفی برنامه‌ها

### `pwm_selftest`

این برنامه برای بررسی وضعیت رجیسترهای PWM طراحی شده است و موارد زیر را پوشش می‌دهد:

- بررسی کانال‌های PWM1 تا PWM5
- خواندن مقادیر رجیسترهای مرتبط با PWM
- بررسی حالت‌های دوره‌ی ثابت و دوره‌ی ۱۶ بیتی
- گزارش نتیجه از طریق `defmt` و RTT

این تست در سطح رجیستر انجام می‌شود و برای اجرای آن به اتصال خروجی PWM به مدار خارجی نیاز نیست.

## پیش‌نیازها

- نصب Rust و ابزارهای مربوط به هدف‌های Embedded
- نصب کامپوننت `rust-src` برای ساخت `core` با `build-std`
- نصب `probe-rs`
- پروگرامر/دیباگر سازگار، مانند WCH-Link با پشتیبانی `probe-rs`
- برد دارای تراشه‌ی CH572 یا CH570

## ساخت و اجرای برنامه

دستورها را از ریشه‌ی مخزن اجرا نکنید؛ ابتدا وارد این پوشه شوید:

```console
cd examples/ch572

<p align="center"><img src="../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# کامپایل برنامه
cargo build --release --bin pwm_selftest

# کامپایل، پروگرام، ریست و اجرای برنامه
cargo run --release --bin pwm_selftest
```

تنظیمات `.cargo/config.toml` هدف `riscv32imac-unknown-none-elf` و فرمان `probe-rs run --chip CH572` را انتخاب می‌کند. بنابراین `cargo run` علاوه بر اجرا، عملیات پروگرام و ریست را نیز انجام می‌دهد و خروجی‌های `defmt` را از طریق RTT دریافت می‌کند.

### انتخاب WCH-Link

اگر چند پروگرامر متصل است، می‌توانید دستگاه موردنظر را با شناسه‌ی آن انتخاب کنید:

```console
PROBE_RS_PROBE=<VID:PID:SERIAL> cargo run --release --bin pwm_selftest
```

همچنین می‌توان شناسه‌ی Probe را به آرگومان‌های Runner ارسال کرد. در صورت تعیین‌نکردن شناسه، اولین Probe انتخاب می‌شود.

## نکات فنی

- این پروژه از هدف `riscv32imac-unknown-none-elf` استفاده می‌کند؛ هسته‌ی QingKe V3A در CH572 از مجموعه‌دستور RV32IMAC پشتیبانی می‌کند.
- قابلیت `build-std = ["core"]` در تنظیمات Cargo فعال است؛ بنابراین وجود `rust-src` ضروری است.
- سطح گزارش‌دهی پیش‌فرض `DEFMT_LOG=info` است.
- برای مشاهده‌ی پیام‌های RTT، اجرای برنامه از طریق Runner تنظیم‌شده در `.cargo/config.toml` توصیه می‌شود.

## منابع مرتبط

- [مخزن اصلی ch5xx-hal](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [پوشه‌ی همه‌ی مثال‌ها](../)
- [مستندات probe-rs](https://probe.rs/)
- [زبان برنامه‌نویسی Rust](https://www.rust-lang.org/)

</div>

<div dir="ltr" align="left">

## Overview

This directory contains `no_std` example binaries for the `ch5xx-hal` crate on **CH572 / CH570** microcontrollers featuring the **QingKe V3A** core. At present, it provides a PWM register self-test.

The example is intended as a starting point for PWM inspection and for understanding the Embedded Rust project layout used by the CH57x family.

## Directory layout

| Path / file | Purpose |
|---|---|
| `.cargo/config.toml` | Selects the RISC-V target, enables `build-std`, and configures `probe-rs` as the runner |
| `Cargo.toml` | Dependencies, HAL features, and build profiles |
| `build.rs` | Build script |
| `src/bin/pwm_selftest.rs` | PWM1–PWM5 register inspection and self-test |

## Example binary

### `pwm_selftest`

This program inspects the PWM peripheral registers and covers:

- PWM1 through PWM5
- Reading back PWM-related register values
- Fixed-period and 16-bit-period configurations
- Reporting through `defmt` over RTT

The test is register-level and does not require an external load or PWM output wiring.

## Prerequisites

- Rust toolchain with Embedded/RISC-V support
- The `rust-src` component for `build-std`
- `probe-rs`
- A compatible debug probe, such as a WCH-Link supported by `probe-rs`
- A CH572 or CH570 target board

## Build and run

Run the commands from this directory:

```console
cd examples/ch572

# Build
cargo build --release --bin pwm_selftest

# Build, flash, reset, run, and capture RTT output
cargo run --release --bin pwm_selftest
```

The local Cargo configuration selects `riscv32imac-unknown-none-elf` and the runner `probe-rs run --chip CH572`. Consequently, `cargo run` also flashes and resets the target and captures `defmt` output over RTT.

### Selecting a WCH-Link

When multiple probes are connected, select one by its identifier:

```console
PROBE_RS_PROBE=<VID:PID:SERIAL> cargo run --release --bin pwm_selftest
```

The probe identifier can also be passed to the runner. If it is omitted, `probe-rs` selects the first available probe.

## Technical notes

- The project targets `riscv32imac-unknown-none-elf`; the CH572 QingKe V3A core supports RV32IMAC.
- Cargo is configured with `build-std = ["core"]`, so the `rust-src` component is required.
- The default log level is `DEFMT_LOG=info`.
- Running through the configured Cargo runner is recommended for RTT log capture.

## Related resources

- [Main ch5xx-hal repository](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [All examples](../)
- [probe-rs documentation](https://probe.rs/)
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

