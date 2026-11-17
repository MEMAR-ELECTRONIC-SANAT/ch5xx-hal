# مثال‌های کاربردی کتابخانه ch5xx-hal | CH5xx HAL Examples

<div dir="rtl" align="right">

## معرفی

این پوشه مجموعه‌ای از پروژه‌های نمونه (Example Projects) برای استفاده از کتابخانه **ch5xx-hal** در میکروکنترلرهای بی‌سیم خانواده **WCH CH5xx** را در بر می‌گیرد. مثال‌ها با زبان **Rust** و در محیط **no_std** نوشته شده‌اند و هدف آن‌ها نمایش روش راه‌اندازی و استفاده از واحدهای جانبی (Peripherals)، قابلیت‌های هم‌زمان (Async)، ارتباطات و امکانات مدیریت توان است.

نمونه‌ها بر اساس خانواده یا مدل میکروکنترلر از یکدیگر جدا شده‌اند. هر پوشه یک پروژه مستقل Rust با فایل `Cargo.toml`، تنظیمات ابزار ساخت و فایل‌های اجرایی مخصوص همان تراشه است.

> **توجه:** وجود یک مثال در این مخزن به معنی پشتیبانی کامل یا اعتبارسنجی تمام قابلیت‌ها روی همه تراشه‌ها نیست. وضعیت پشتیبانی هر Peripheral و محدودیت‌های سخت‌افزاری را در مستندات اصلی HAL و README همان تراشه بررسی کنید.

## ساختار پوشه‌ها

| پوشه | تراشه / هسته | توضیحات |
|---|---|---|
| [ch572](ch572/) | CH572 / CH570 – QingKe V3A | نمونه آزمون PWM و بررسی رجیسترهای PWM1 تا PWM5 |
| [ch582](ch582/) | CH582 – QingKe V4A | نمونه‌های GPIO، ADC، کلاک، RTC، SPI، UART، Timer، USB و Watchdog |
| [ch585](ch585/) | CH585 – QingKe V3C | مجموعه گسترده مثال‌های GPIO، ADC، PWM، UART، I2C، SPI، RTC، USB، DMA، Embassy و مدیریت توان |
| [ch592](ch592/) | CH592 – QingKe V3C | مثال‌های پایه، ADC، کلاک، PWM، RTC، SPI، Timer، TouchKey، UART، USB و Watchdog |

## راهنمای پوشه‌ها

### 1. پوشه `ch572`

این پوشه مثال‌های `no_std` مخصوص CH572 و CH570 را شامل می‌شود.

| فایل اجرایی | عملکرد |
|---|---|
| `pwm_selftest` | آزمون PWM1 تا PWM5، خواندن مجدد مقادیر رجیسترها و بررسی دوره‌های ثابت و ۱۶ بیتی؛ بدون نیاز به سیم‌کشی خارجی |

اجرای نمونه:

```console
cd examples/ch572
cargo build --release --bin pwm_selftest
cargo run --release --bin pwm_selftest
```

تنظیمات پوشه `.cargo` هدف RISC-V، گزینه‌های ساخت و Runner مربوط به پروگرام و اجرا را مشخص می‌کند. اجرای `cargo run` از `probe-rs` برای پروگرام و Reset تراشه و دریافت گزارش‌های `defmt` از طریق RTT استفاده می‌کند.

[مشاهده فایل‌های مثال CH572](ch572/)

### 2. پوشه `ch582`

این پوشه پروژه‌های نمونه برای CH582 را در بر می‌گیرد. مثال‌ها بخش‌های مختلف HAL را پوشش می‌دهند:

| گروه | فایل‌ها / مثال‌ها | کاربرد |
|---|---|---|
| راه‌اندازی و کلاک | `hello`، `clock_ladder` | راه‌اندازی اولیه، تأخیر و بررسی پله‌ای کلاک |
| مبدل آنالوگ به دیجیتال | `adc_auto`، `adc_temp` | نمونه‌برداری زمان‌بندی‌شده با DMA داخلی ADC و اندازه‌گیری دمای داخلی |
| PWM | `pwm_selftest` | آزمون عملکرد PWM |
| RTC | `rtc_calendar` | تقویم ساعت، آلارم و تایمر بازه‌ای |
| SPI | `spi_loopback`، `spi_async_loopback` | آزمون Loopback در حالت Blocking و Async |
| Timer | `timer_counter` | بررسی شمارنده تایمر |
| UART | `uart_loopback` | آزمون داخلی ارسال و دریافت UART |
| USB | `usb_cdc_echo`، `usb2_cdc_echo` | نمونه Echo با رابط USB CDC |
| Watchdog | `watchdog` | بررسی Window Watchdog و مسیر تغذیه آن |

برای مثال‌های SPI ناهمگام و USB CDC، Featureهای مربوطه باید مطابق تنظیمات `Cargo.toml` فعال شوند. این مثال‌ها در حالت پیش‌فرض لزوماً در فهرست Binaryهای قابل ساخت قرار ندارند.

[مشاهده فایل‌های مثال CH582](ch582/)

### 3. پوشه `ch585`

این پوشه کامل‌ترین مجموعه نمونه‌های این شاخه را ارائه می‌کند و برای بررسی عملی بسیاری از درایورهای HAL مناسب است.

| گروه | مثال‌ها | کاربرد |
|---|---|---|
| GPIO | `blinky`، `gpio_in`، `gpio_async`، `gpio_async_loopback` | خروجی دیجیتال، ورودی کلید، وقفه و آزمون Loopback |
| کلاک | `clk_set` | تنظیم و گزارش وضعیت کلاک سیستم |
| ADC | `adc_temp`، `adc_pin`، `adc_scan_dma` | اندازه‌گیری دمای داخلی، خواندن ورودی آنالوگ و اسکن چندکاناله با DMA |
| UART | `uart_loopback`، `uart_echo` | آزمون Loopback و Echo ناهمگام |
| I2C | `i2c_scan`، `i2c_oled`، `i2c_oled_async` | اسکن آدرس، راه‌اندازی نمایشگر SSD1306 و انتقال ناهمگام |
| SPI | `spi_loopback`، `spi_async_loopback` | آزمون SPI در حالت Blocking و Async همراه با DMA |
| PWM | `pwm_out` | تولید PWM و کنترل Duty Cycle |
| RTC و زمان | `rtc_calendar`، `rtc_oled`، `embassy_time`، `embassy_time_tmr` | تقویم، آلارم، نمایش ساعت و Time Driver چارچوب Embassy |
| Timer و DMA | `timer_dma_async` | اتصال وقفه Timer، انتظار DMA و لغو عملیات |
| USB | `usb_cdc_echo`، `usbhs_cdc_echo`، `usb_endpoints`، `usbhs_endpoints` | USB Full-Speed و High-Speed، ارتباط CDC و آزمون Endpointها |
| توان و نظارت | `watchdog`، `sleep_wake` | Window Watchdog و بیدارباش از حالت Sleep با RTC |
| گزارش‌گیری | `defmt_rtt` | ارسال گزارش از طریق SEGGER RTT |

اجرای نمونه ساده:

```console
cd examples/ch585
cargo run --release --bin blinky
```

انتخاب Time Driver مبتنی بر TMR به‌جای SysTick:

```console
cargo run --release --bin embassy_time_tmr --no-default-features --features time-driver-tmr0
```

برای ساخت تمام Binaryها با Time Driver مبتنی بر TMR:

```console
cargo build --release --bins --no-default-features --features time-driver-tmr0
```

**نکات سخت‌افزاری مهم CH585:**

- مثال `gpio_async_loopback` به اتصال PA14 به PA15 نیاز دارد.
- مثال `spi_loopback` و `spi_async_loopback` برای Loopback به اتصال PA14 به PA15 نیاز دارند.
- مثال‌های I2C OLED به نمایشگر SSD1306 با آدرس `0x3C` نیاز دارند.
- مثال‌های USB برای ارتباط واقعی به اتصال USB و میزبان مناسب نیاز دارند.
- در انتخاب Time Driver، Featureهای ناسازگار را هم‌زمان فعال نکنید. جزئیات هر Binary و محدودیت‌های آن در [README اختصاصی CH585](ch585/README.md) آمده است.

[مشاهده فایل‌های مثال CH585](ch585/)

### 4. پوشه `ch592`

این پوشه مجموعه‌ای از مثال‌های CH592X را ارائه می‌کند. بخشی از نمونه‌ها دارای آزمون داخلی و گزارش نتیجه هستند.

| گروه | مثال‌ها | کاربرد |
|---|---|---|
| شروع به کار | `hello` | راه‌اندازی اولیه، تأخیر و گزارش‌گیری `defmt` |
| ADC | `adc_auto`، `adc_scan`، `adc_temp` | نمونه‌برداری خودکار، اسکن چندکاناله و اندازه‌گیری دمای داخلی |
| کلاک | `clk_pll48` | تولید و بررسی کلاک 48MHz با PLL |
| PWM | `pwm_16bit`، `pwm_out` | تنظیم دوره و Duty Cycle و بررسی خروجی |
| RTC | `rtc_calendar` | تقویم، آلارم یک‌باره و تایمر بازه‌ای |
| SPI | `spi_loopback`، `spi_async_loopback` | آزمون SPI در حالت Blocking و Async و DMA |
| Timer | `timer_counter` | بررسی شمارنده تایمر |
| TouchKey | `touchkey`، `touchkey_led` | تشخیص کلید لمسی و کنترل LED |
| UART | `uart_loopback` | آزمون داخلی UART |
| USB | `usb_cdc_echo` | ارتباط USB CDC و بازگرداندن داده دریافتی |
| توان | `sleep_wake` | آزمون Halt/Sleep و بیدارباش با RTC |
| Watchdog | `watchdog` | بررسی Window Watchdog و مسیر تغذیه |

اجرای مثال پایه:

```console
cd examples/ch592
cargo build --release --bin hello
cargo run --release --bin hello
```

برای انتخاب Time Driver مبتنی بر TMR:

```console
cargo build --release --bin embassy_time --no-default-features --features time-driver-tmr1
```

**نکات سخت‌افزاری مهم CH592:**

- برای مثال `spi_loopback`، پایه‌های PA14 و PA15 را به یکدیگر متصل کنید.
- مثال `pwm_out` و `pwm_16bit` به اتصال PA13 به PA14 برای اندازه‌گیری Loopback نیاز دارند.
- مثال `usb_cdc_echo` به اتصال USB برد به میزبان نیاز دارد؛ اتصال پروگرامر به‌تنهایی کافی نیست.
- در مثال `sleep_wake` ممکن است ارتباط RTT هنگام ورود به Sleep قطع شود؛ روش ثبت و خواندن نتیجه در README اختصاصی توضیح داده شده است.
- برخی پایه‌های رابط I2C ممکن است با رابط Debug مشترک باشند؛ برای آزمون I2C، محدودیت اتصال Debug را در نظر بگیرید.

[مشاهده فایل‌های مثال CH592](ch592/)

## ساختار مشترک هر پروژه

| مسیر / فایل | توضیحات |
|---|---|
| `Cargo.toml` | تعریف Package، وابستگی‌ها، Featureها و تنظیمات Build |
| `.cargo/config.toml` | تنظیم Target، گزینه‌های کامپایل و Runner (در پوشه‌هایی که این فایل را دارند) |
| `build.rs` | اسکریپت Build پروژه |
| `src/bin/` | فایل‌های مستقل هر مثال؛ نام فایل، نام Binary قابل اجرا را مشخص می‌کند |
| `src/` | کدهای مشترک یا ماژول‌های کمکی پروژه، در صورت وجود |
| `README.md` | راهنمای اختصاصی تراشه، فرمان‌های اجرا و توضیحات سیم‌بندی (در پوشه‌هایی که موجود است) |

## پیش‌نیازها و اجرای مثال‌ها

1. ابزارهای Rust و Cargo را نصب کنید.
2. Target مناسب هسته تراشه را به Toolchain اضافه کنید. برای نمونه، CH585 و CH592 از خانواده QingKe V3C و CH582 از QingKe V4A هستند؛ Target دقیق را از تنظیمات `.cargo/config.toml` همان پروژه بررسی کنید.
3. ابزار `probe-rs` و درایور/اتصال Debug سازگار با برد را آماده کنید.
4. WCH-Link یا Probe مورد استفاده را به برد متصل کنید.
5. وارد پوشه تراشه مورد نظر شوید و فرمان Build یا Run را اجرا کنید.

نمونه فرمان عمومی:

```console
cd examples/<chip>
cargo build --release --bin <example_name>
cargo run --release --bin <example_name>
```

برای مشاهده فهرست Binaryهای هر تراشه، فایل‌های موجود در مسیر `src/bin/` یا جدول README اختصاصی همان پوشه را بررسی کنید. نام Binary معمولاً با نام فایل Rust و بدون پسوند `.rs` یکسان است.

## گزارش‌گیری و اشکال‌زدایی

بیشتر مثال‌ها از `defmt` و `defmt-rtt` برای گزارش‌گیری استفاده می‌کنند. فرمان `cargo run` در پروژه‌هایی که Runner آن‌ها تنظیم شده است، عملیات پروگرام، Reset و دریافت خروجی RTT را یکجا انجام می‌دهد.

اگر چند پروگرامر WCH-Link متصل باشد، می‌توان Probe موردنظر را با متغیر محیطی `PROBE_RS_PROBE` انتخاب کرد؛ قالب دقیق مقدار را مطابق نسخه `probe-rs` و شناسه USB/Serial دستگاه خود تنظیم کنید.

## منابع مرتبط

- [مخزن اصلی ch5xx-hal](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [مستندات API کتابخانه در docs.rs](https://docs.rs/ch5xx-hal)
- [مخزن داده‌ها و متادیتای CH5xx](https://github.com/ch32-rs/ch5xx-data)
- [مستندات و منابع CH585 در MES](https://github.com/MEMAR-ELECTRONIC-SANAT/MES-CH585)

## مجوز و ملاحظات

مخزن حاضر Fork پروژه [ch32-rs/ch5xx-hal](https://github.com/ch32-rs/ch5xx-hal) است. برای شرایط استفاده، تغییر و بازتوزیع، فایل‌های مجوز مخزن و مجوزهای وابستگی‌ها را بررسی کنید. مثال‌ها را ابتدا روی برد آزمایشی و با توجه به محدودیت پایه‌ها و ولتاژهای مجاز تراشه اجرا کنید.

</div>

---

<p align="center"><img src="../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# CH5xx HAL Examples

<div dir="ltr" align="left">

## Overview

This directory contains example projects demonstrating the **ch5xx-hal** Rust hardware abstraction layer for WCH **CH5xx wireless microcontrollers**. The examples are written for bare-metal `no_std` environments and cover peripheral initialization, blocking and asynchronous operations, communication interfaces, timing, power management and debugging.

Examples are organized by target device. Each device directory is an independent Rust package with its own `Cargo.toml`, build configuration and executable examples.

> **Important:** An example being present does not imply that every peripheral is fully supported or validated on every device. Check the HAL status documentation and the device-specific README before relying on a feature.

## Directory Overview

| Directory | Device / Core | Description |
|---|---|---|
| [ch572](ch572/) | CH572 / CH570 – QingKe V3A | PWM self-test and PWM1–PWM5 register readback |
| [ch582](ch582/) | CH582 – QingKe V4A | GPIO, ADC, clock, RTC, SPI, UART, timer, USB and watchdog examples |
| [ch585](ch585/) | CH585 – QingKe V3C | Extensive GPIO, ADC, PWM, UART, I2C, SPI, RTC, USB, DMA, Embassy and power examples |
| [ch592](ch592/) | CH592 – QingKe V3C | Basic startup, ADC, clock, PWM, RTC, SPI, timer, TouchKey, UART, USB and watchdog examples |

## Device Examples

### 1. CH572

The `ch572` directory contains `no_std` examples for CH572 and CH570.

| Binary | Description |
|---|---|
| `pwm_selftest` | PWM1–PWM5 register readback and fixed/16-bit cycle checks; no external wiring required |

Build and run:

```console
cd examples/ch572
cargo build --release --bin pwm_selftest
cargo run --release --bin pwm_selftest
```

The `.cargo` configuration selects the RISC-V target, build options and probe runner. `cargo run` uses `probe-rs` to flash and reset the chip and capture `defmt` output over RTT.

[Browse CH572 examples](ch572/)

### 2. CH582

The `ch582` directory provides examples for several HAL subsystems.

| Category | Examples | Description |
|---|---|---|
| Startup and clock | `hello`, `clock_ladder` | Basic startup, delay and clock-step inspection |
| ADC | `adc_auto`, `adc_temp` | Timed ADC-local DMA sampling and internal temperature measurement |
| PWM | `pwm_selftest` | PWM self-test |
| RTC | `rtc_calendar` | RTC calendar, alarm and interval timer |
| SPI | `spi_loopback`, `spi_async_loopback` | Blocking and asynchronous SPI loopback |
| Timer | `timer_counter` | Timer counter test |
| UART | `uart_loopback` | Internal UART loopback |
| USB | `usb_cdc_echo`, `usb2_cdc_echo` | USB CDC echo examples |
| Watchdog | `watchdog` | Window watchdog and feed-path test |

The asynchronous SPI and USB CDC examples require their corresponding Cargo features. They are not necessarily included in the default binary build.

[Browse CH582 examples](ch582/)

### 3. CH585

The `ch585` directory provides the broadest example set in this collection and is useful for hands-on evaluation of many HAL drivers.

| Category | Examples | Description |
|---|---|---|
| GPIO | `blinky`, `gpio_in`, `gpio_async`, `gpio_async_loopback` | Digital output, button input, interrupts and loopback |
| Clock | `clk_set` | System clock configuration and status |
| ADC | `adc_temp`, `adc_pin`, `adc_scan_dma` | Internal temperature, analog input and DMA scan |
| UART | `uart_loopback`, `uart_echo` | UART loopback and asynchronous echo |
| I2C | `i2c_scan`, `i2c_oled`, `i2c_oled_async` | Address scan and SSD1306 display, blocking/async |
| SPI | `spi_loopback`, `spi_async_loopback` | Blocking and asynchronous SPI with DMA |
| PWM | `pwm_out` | PWM generation and duty-cycle control |
| RTC and time | `rtc_calendar`, `rtc_oled`, `embassy_time`, `embassy_time_tmr` | Calendar, alarm, clock display and Embassy time drivers |
| Timer and DMA | `timer_dma_async` | Timer interrupt binding, DMA waits and cancellation |
| USB | `usb_cdc_echo`, `usbhs_cdc_echo`, `usb_endpoints`, `usbhs_endpoints` | USB Full-Speed/High-Speed, CDC and endpoint tests |
| Power and supervision | `watchdog`, `sleep_wake` | Window watchdog and RTC wake-up from sleep |
| Logging | `defmt_rtt` | Logging over SEGGER RTT |

Run a basic example:

```console
cd examples/ch585
cargo run --release --bin blinky
```

Select a TMR-based time driver instead of SysTick:

```console
cargo run --release --bin embassy_time_tmr --no-default-features --features time-driver-tmr0
```

Build all binaries with a TMR-based time driver:

```console
cargo build --release --bins --no-default-features --features time-driver-tmr0
```

**CH585 hardware notes:**

- `gpio_async_loopback` requires PA14 connected to PA15.
- `spi_loopback` and `spi_async_loopback` require a PA14-to-PA15 loopback connection.
- I2C OLED examples require an SSD1306 display at address `0x3C`.
- USB examples require a suitable USB host connection.
- Select only a compatible Embassy time-driver feature. See the [CH585 README](ch585/README.md) for binary-specific details and limitations.

[Browse CH585 examples](ch585/)

### 4. CH592

The `ch592` directory contains a collection of examples for CH592X. Several examples include internal checks and report their results.

| Category | Examples | Description |
|---|---|---|
| Startup | `hello` | Basic initialization, delay and `defmt` logging |
| ADC | `adc_auto`, `adc_scan`, `adc_temp` | Automatic sampling, multi-channel scan and internal temperature |
| Clock | `clk_pll48` | 48 MHz PLL clock generation and readback |
| PWM | `pwm_16bit`, `pwm_out` | Period/duty configuration and output checks |
| RTC | `rtc_calendar` | Calendar, one-shot alarm and interval timer |
| SPI | `spi_loopback`, `spi_async_loopback` | Blocking/async SPI and DMA loopback |
| Timer | `timer_counter` | Timer counter test |
| TouchKey | `touchkey`, `touchkey_led` | Touch input detection and LED control |
| UART | `uart_loopback` | Internal UART loopback |
| USB | `usb_cdc_echo` | USB CDC echo |
| Power | `sleep_wake` | Halt/sleep and RTC wake-up |
| Watchdog | `watchdog` | Window watchdog test |

Run the basic example:

```console
cd examples/ch592
cargo build --release --bin hello
cargo run --release --bin hello
```

Select a TMR-based time driver:

```console
cargo build --release --bin embassy_time --no-default-features --features time-driver-tmr1
```

**CH592 hardware notes:**

- For `spi_loopback`, connect PA14 to PA15.
- `pwm_out` and `pwm_16bit` require PA13 connected to PA14 for loopback measurement.
- `usb_cdc_echo` requires the board USB connection to a host; the debug probe alone is not sufficient.
- The RTT session may stop when `sleep_wake` enters sleep. The device-specific README explains how to retrieve the recorded result.
- Some I2C pins may be shared with the debug interface. Account for the debug connection when testing I2C.

[Browse CH592 examples](ch592/)

## Common Project Layout

| Path / File | Description |
|---|---|
| `Cargo.toml` | Package metadata, dependencies, features and build profiles |
| `.cargo/config.toml` | Target, compiler options and runner configuration, where present |
| `build.rs` | Build script |
| `src/bin/` | Independent executable examples; the Rust filename determines the binary name |
| `src/` | Shared source code or helper modules, where present |
| `README.md` | Device-specific instructions, run commands and wiring notes, where present |

## Prerequisites and Running

1. Install the Rust toolchain and Cargo.
2. Install the target appropriate for the device core. CH585 and CH592 use QingKe V3C, while CH582 uses QingKe V4A; verify the exact target in the device directory's `.cargo/config.toml`.
3. Install `probe-rs` and prepare a compatible debug connection.
4. Connect a WCH-Link or supported probe to the development board.
5. Enter the target device directory and run the build or run command.

Generic command template:

```console
cd examples/<chip>
cargo build --release --bin <example_name>
cargo run --release --bin <example_name>
```

To list the available binaries, inspect `src/bin/` or the device-specific README. A binary name normally matches its Rust source filename without the `.rs` extension.

## Logging and Debugging

Most examples use `defmt` and `defmt-rtt` for logging. In directories with a configured runner, `cargo run` performs flashing, reset and RTT log capture in one step.

When multiple WCH-Link probes are connected, select a specific probe with the `PROBE_RS_PROBE` environment variable. Use the value format supported by your installed `probe-rs` version and the USB/serial identity of your probe.

## Related Resources

- [ch5xx-hal repository](https://github.com/MEMAR-ELECTRONIC-SANAT/ch5xx-hal)
- [HAL API documentation on docs.rs](https://docs.rs/ch5xx-hal)
- [CH5xx register data and metadata](https://github.com/ch32-rs/ch5xx-data)
- [MES CH585 documentation and resources](https://github.com/MEMAR-ELECTRONIC-SANAT/MES-CH585)

## License and Usage

This repository is a fork of [ch32-rs/ch5xx-hal](https://github.com/ch32-rs/ch5xx-hal). Review the repository license files and dependency licenses before using, modifying or redistributing the code. Test examples on a development board first and observe the device's pin and voltage limitations.

</div>

---

## تصاویر و دیاگرام‌های راهنما | Images and Reference Diagrams

این پوشه در حال حاضر شامل مثال‌های نرم‌افزاری است؛ تصاویر هویتی و گرافیکی MES در مسیر [Images/GitHub-Assets](../Images/GitHub-Assets/) مخزن اصلی نگهداری می‌شوند.

The examples directory currently focuses on firmware projects. MES visual identity assets are maintained in the main repository at [Images/GitHub-Assets](../Images/GitHub-Assets/).


<p align="center"><img src="../Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="MES Thank You Footer"></p>

## تهیه و تدوین | Credits and Documentation

**معمار الکترونیک صنعت / MEMAR ELECTRONIC SANAT (MES)**

همراه شما در مسیر طراحی و ساخت مدارهای مطمئن

*Your partner in designing and building reliable circuits.*

- Telegram: [https://t.me/Memar_Electronic](https://t.me/Memar_Electronic)
- Instagram: [https://www.instagram.com/Memar.Electronic](https://www.instagram.com/Memar.Electronic)
- GitHub: [MEMAR-ELECTRONIC-SANAT](https://github.com/MEMAR-ELECTRONIC-SANAT)

[مشاهده سایر آموزش‌ها / Explore more tutorials](https://github.com/MEMAR-ELECTRONIC-SANAT)
