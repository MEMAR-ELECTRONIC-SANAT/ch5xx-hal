<div dir="rtl" align="right">

<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# فایل‌های اجرایی مثال‌های CH592

در این پوشه فایل‌های مستقل Rust قرار دارند. هر فایل معمولاً یک Binary جداگانه است که از طریق نام فایل در فرمان‌های Cargo انتخاب می‌شود. توضیح‌ها عملکرد کلی مثال را معرفی می‌کنند؛ جزئیات پایه‌ها، Featureها و سیم‌بندی را در README اختصاصی تراشه بررسی کنید.

## محتویات

| فایل | توضیحات |
|---|---|
| [`adc_auto.rs`](adc_auto.rs) | نمونه‌برداری خودکار ADC. |
| [`adc_scan.rs`](adc_scan.rs) | اسکن چند ورودی ADC. |
| [`adc_temp.rs`](adc_temp.rs) | اندازه‌گیری دمای داخلی. |
| [`clk_pll48.rs`](clk_pll48.rs) | تنظیم و بررسی کلاک PLL با هدف 48MHz. |
| [`embassy_time.rs`](embassy_time.rs) | نمونه زمان‌بندی با Embassy. |
| [`hello.rs`](hello.rs) | راه‌اندازی پایه و گزارش‌گیری. |
| [`i2c_scan.rs`](i2c_scan.rs) | اسکن آدرس‌های I2C. |
| [`pwm_16bit.rs`](pwm_16bit.rs) | آزمون PWM با تنظیمات دوره ۱۶ بیتی. |
| [`pwm_out.rs`](pwm_out.rs) | تولید خروجی PWM. |
| [`rtc_calendar.rs`](rtc_calendar.rs) | آزمون تقویم RTC. |
| [`sleep_wake.rs`](sleep_wake.rs) | آزمون حالت کم‌مصرف و بیدارباش. |
| [`spi_async_loopback.rs`](spi_async_loopback.rs) | آزمون Loopback ناهمگام SPI. |
| [`spi_loopback.rs`](spi_loopback.rs) | آزمون Loopback مسدودکننده SPI. |
| [`timer_counter.rs`](timer_counter.rs) | بررسی شمارنده تایمر. |
| [`touchkey.rs`](touchkey.rs) | خواندن کلید لمسی. |
| [`touchkey_led.rs`](touchkey_led.rs) | کنترل LED بر اساس ورودی کلید لمسی. |
| [`uart_loopback.rs`](uart_loopback.rs) | آزمون Loopback رابط UART. |
| [`usb_cdc_echo.rs`](usb_cdc_echo.rs) | نمونه Echo رابط USB CDC. |
| [`watchdog.rs`](watchdog.rs) | آزمون Window Watchdog. |
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

# Executable Examples for CH592

This directory contains standalone Rust example binaries. Each source file is generally selected by its file stem in Cargo commands. The descriptions summarize each example; consult the device README for pin assignments, feature flags and wiring details.

## Contents

| File | Description |
|---|---|
| [`adc_auto.rs`](adc_auto.rs) | Automatic ADC sampling. |
| [`adc_scan.rs`](adc_scan.rs) | Multi-channel ADC scan. |
| [`adc_temp.rs`](adc_temp.rs) | Internal temperature measurement. |
| [`clk_pll48.rs`](clk_pll48.rs) | PLL clock setup and 48MHz inspection. |
| [`embassy_time.rs`](embassy_time.rs) | Embassy time example. |
| [`hello.rs`](hello.rs) | Basic startup and logging. |
| [`i2c_scan.rs`](i2c_scan.rs) | I2C address scanner. |
| [`pwm_16bit.rs`](pwm_16bit.rs) | PWM test with 16-bit period configuration. |
| [`pwm_out.rs`](pwm_out.rs) | PWM output generation. |
| [`rtc_calendar.rs`](rtc_calendar.rs) | RTC calendar test. |
| [`sleep_wake.rs`](sleep_wake.rs) | Low-power sleep and wake-up test. |
| [`spi_async_loopback.rs`](spi_async_loopback.rs) | Asynchronous SPI loopback. |
| [`spi_loopback.rs`](spi_loopback.rs) | Blocking SPI loopback. |
| [`timer_counter.rs`](timer_counter.rs) | Timer counter test. |
| [`touchkey.rs`](touchkey.rs) | Touch-key input. |
| [`touchkey_led.rs`](touchkey_led.rs) | LED control from touch-key input. |
| [`uart_loopback.rs`](uart_loopback.rs) | UART loopback test. |
| [`usb_cdc_echo.rs`](usb_cdc_echo.rs) | USB CDC echo example. |
| [`watchdog.rs`](watchdog.rs) | Window watchdog test. |
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
