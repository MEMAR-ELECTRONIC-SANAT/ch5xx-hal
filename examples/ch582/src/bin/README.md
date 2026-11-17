<div dir="rtl" align="right">

<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# فایل‌های اجرایی مثال‌های CH582

در این پوشه فایل‌های مستقل Rust قرار دارند. هر فایل معمولاً یک Binary جداگانه است که از طریق نام فایل در فرمان‌های Cargo انتخاب می‌شود. توضیح‌ها عملکرد کلی مثال را معرفی می‌کنند؛ جزئیات پایه‌ها، Featureها و سیم‌بندی را در README اختصاصی تراشه بررسی کنید.

## محتویات

| فایل | توضیحات |
|---|---|
| [`adc_auto.rs`](adc_auto.rs) | نمونه‌برداری ADC با زمان‌بندی و DMA داخلی. |
| [`adc_temp.rs`](adc_temp.rs) | خواندن سنسور دمای داخلی. |
| [`clock_ladder.rs`](clock_ladder.rs) | بررسی مرحله‌ای تنظیمات و فرکانس کلاک. |
| [`hello.rs`](hello.rs) | راه‌اندازی پایه و گزارش‌گیری اولیه. |
| [`pwm_selftest.rs`](pwm_selftest.rs) | آزمون خروجی و رجیسترهای PWM. |
| [`rtc_calendar.rs`](rtc_calendar.rs) | آزمون تقویم و امکانات RTC. |
| [`spi_async_loopback.rs`](spi_async_loopback.rs) | آزمون Loopback رابط SPI در حالت Async. |
| [`spi_loopback.rs`](spi_loopback.rs) | آزمون Loopback رابط SPI در حالت Blocking. |
| [`timer_counter.rs`](timer_counter.rs) | بررسی شمارنده تایمر. |
| [`uart_loopback.rs`](uart_loopback.rs) | آزمون ارسال و دریافت داخلی UART. |
| [`usb2_cdc_echo.rs`](usb2_cdc_echo.rs) | نمونه Echo رابط USB CDC در مسیر USB2. |
| [`usb_cdc_echo.rs`](usb_cdc_echo.rs) | نمونه Echo رابط USB CDC. |
| [`watchdog.rs`](watchdog.rs) | آزمون Window Watchdog و تغذیه آن. |
برای ساخت یک مثال از ریشه پروژه تراشه اجرا کنید:

```console
cargo build --release --bin <binary_name>
```


<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="MES Thank You Footer"></p>

## تهیه و تدوین
**معمار الکترونیک صنعت | MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

---

# Executable Examples for CH582

This directory contains standalone Rust example binaries. Each source file is generally selected by its file stem in Cargo commands. The descriptions summarize each example; consult the device README for pin assignments, feature flags and wiring details.

## Contents

| File | Description |
|---|---|
| [`adc_auto.rs`](adc_auto.rs) | Timed ADC sampling using the ADC-local DMA. |
| [`adc_temp.rs`](adc_temp.rs) | Internal temperature sensor reading. |
| [`clock_ladder.rs`](clock_ladder.rs) | Stepwise clock configuration and frequency inspection. |
| [`hello.rs`](hello.rs) | Basic startup and logging. |
| [`pwm_selftest.rs`](pwm_selftest.rs) | PWM output and register self-test. |
| [`rtc_calendar.rs`](rtc_calendar.rs) | RTC calendar and related functions. |
| [`spi_async_loopback.rs`](spi_async_loopback.rs) | Asynchronous SPI loopback test. |
| [`spi_loopback.rs`](spi_loopback.rs) | Blocking SPI loopback test. |
| [`timer_counter.rs`](timer_counter.rs) | Timer counter test. |
| [`uart_loopback.rs`](uart_loopback.rs) | UART transmit/receive loopback. |
| [`usb2_cdc_echo.rs`](usb2_cdc_echo.rs) | USB CDC echo example using the USB2 path. |
| [`usb_cdc_echo.rs`](usb_cdc_echo.rs) | USB CDC echo example. |
| [`watchdog.rs`](watchdog.rs) | Window watchdog and refresh test. |
Build an example from the device package directory:

```console
cargo build --release --bin <binary_name>
```

## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

<p align="center">
  <img src="../../../../Images/GitHub-Assets/MES_Animated_Logo_640x480.svg" width="140" alt="MES Animated Logo">
</p>
