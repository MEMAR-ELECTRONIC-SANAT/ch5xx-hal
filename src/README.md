<div dir="rtl" align="right">

<p align="center"><img src="../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# کد منبع کتابخانه ch5xx-hal

این پوشه پیاده‌سازی اصلی HAL را شامل می‌شود. ماژول‌ها APIهای Rust برای Peripheralهای خانواده WCH CH5xx و جزئیات رجیستر، وقفه، DMA و زمان‌بندی را سازمان‌دهی می‌کنند.

## فایل‌ها

| فایل | توضیحات |
|---|---|
| `lib.rs` | نقطه ورود کتابخانه، انتخاب تراشه و راه‌اندازی |
| `gpio.rs`، `rcc.rs` | GPIO و کلاک/Reset |
| `adc.rs`، `pwm.rs` | ADC و PWM |
| `i2c.rs`، `spi.rs`، `uart.rs` | رابط‌های ارتباطی |
| `rtc.rs`، `time.rs`، `delay.rs` | زمان، RTC و تأخیر |
| `dma.rs`، [dma/](dma/README.md) | انتقال DMA و ابزارهای کمکی |
| [embassy/](embassy/README.md) | اتصال به Embassy و Time Driverها |
| [timer/](timer/README.md) | شمارنده، Capture و قابلیت‌های Timer |
| [usb/](usb/README.md)، [usbhs/](usbhs/README.md) | کنترلرهای USB Full-Speed و High-Speed |
| [internal/](internal/README.md) | اجزای داخلی پیاده‌سازی |
این کد سطح پایین با رجیسترهای سخت‌افزاری سروکار دارد. پیش از تغییر، محدودیت‌های مدل CH5xx و تفاوت هسته‌های QingKe را بررسی کنید.


<p align="center"><img src="../Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="MES Thank You Footer"></p>

## تهیه و تدوین
**معمار الکترونیک صنعت | MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

---

# ch5xx-hal Source Code

This directory contains the core HAL implementation. Modules provide Rust APIs for WCH CH5xx peripherals and organize register, interrupt, DMA and timing details.

## Files

| File | Description |
|---|---|
| `lib.rs` | Library entry point, device selection and initialization |
| `gpio.rs`, `rcc.rs` | GPIO and clock/reset control |
| `adc.rs`, `pwm.rs` | ADC and PWM |
| `i2c.rs`, `spi.rs`, `uart.rs` | Communication interfaces |
| `rtc.rs`, `time.rs`, `delay.rs` | Timekeeping, RTC and delays |
| `dma.rs`, [dma/](dma/README.md) | DMA and helper utilities |
| [embassy/](embassy/README.md) | Embassy integration and time drivers |
| [timer/](timer/README.md) | Timer counter, capture and related features |
| [usb/](usb/README.md), [usbhs/](usbhs/README.md) | USB Full-Speed and High-Speed controllers |
| [internal/](internal/README.md) | Internal implementation components |
This low-level code interacts with hardware registers. Check CH5xx device limitations and QingKe core differences before changing behavior.

## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)
