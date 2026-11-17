<div dir="rtl" align="right">

<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# فایل‌های اجرایی مثال‌های CH585

در این پوشه فایل‌های مستقل Rust قرار دارند. هر فایل معمولاً یک Binary جداگانه است که از طریق نام فایل در فرمان‌های Cargo انتخاب می‌شود. توضیح‌ها عملکرد کلی مثال را معرفی می‌کنند؛ جزئیات پایه‌ها، Featureها و سیم‌بندی را در README اختصاصی تراشه بررسی کنید.

## محتویات

| فایل | توضیحات |
|---|---|
| [`adc_pin.rs`](adc_pin.rs) | خواندن ورودی آنالوگ از پایه ADC. |
| [`adc_scan_dma.rs`](adc_scan_dma.rs) | اسکن ورودی‌های ADC با DMA. |
| [`adc_temp.rs`](adc_temp.rs) | اندازه‌گیری دمای داخلی. |
| [`blinky.rs`](blinky.rs) | نمونه پایه چشمک‌زدن LED. |
| [`clk_set.rs`](clk_set.rs) | پیکربندی کلاک سیستم. |
| [`defmt_rtt.rs`](defmt_rtt.rs) | نمونه گزارش‌گیری از طریق defmt و RTT. |
| [`embassy_time.rs`](embassy_time.rs) | استفاده از زمان‌بند Embassy و Time Driver پیش‌فرض. |
| [`embassy_time_tmr.rs`](embassy_time_tmr.rs) | استفاده از Time Driver مبتنی بر تایمر سخت‌افزاری. |
| [`gpio_async.rs`](gpio_async.rs) | ورودی/خروجی GPIO با API ناهمگام. |
| [`gpio_async_loopback.rs`](gpio_async_loopback.rs) | آزمون ناهمگام GPIO با اتصال Loopback. |
| [`gpio_in.rs`](gpio_in.rs) | خواندن ورودی دیجیتال GPIO. |
| [`i2c_oled.rs`](i2c_oled.rs) | راه‌اندازی نمایشگر OLED از طریق I2C. |
| [`i2c_oled_async.rs`](i2c_oled_async.rs) | راه‌اندازی OLED با انتقال ناهمگام I2C. |
| [`i2c_scan.rs`](i2c_scan.rs) | اسکن آدرس دستگاه‌های I2C. |
| [`pwm_out.rs`](pwm_out.rs) | تولید خروجی PWM. |
| [`rtc_calendar.rs`](rtc_calendar.rs) | آزمون تقویم RTC. |
| [`rtc_oled.rs`](rtc_oled.rs) | نمایش اطلاعات RTC روی OLED. |
| [`sleep_wake.rs`](sleep_wake.rs) | آزمون Sleep و بیدارباش. |
| [`spi_async_loopback.rs`](spi_async_loopback.rs) | آزمون SPI ناهمگام و Loopback. |
| [`spi_loopback.rs`](spi_loopback.rs) | آزمون SPI مسدودکننده و Loopback. |
| [`timer_dma_async.rs`](timer_dma_async.rs) | ترکیب Timer، وقفه و عملیات DMA ناهمگام. |
| [`uart_echo.rs`](uart_echo.rs) | نمونه Echo ناهمگام UART. |
| [`uart_loopback.rs`](uart_loopback.rs) | آزمون Loopback رابط UART. |
| [`usb_cdc_echo.rs`](usb_cdc_echo.rs) | نمونه Echo دستگاه USB CDC. |
| [`usb_endpoints.rs`](usb_endpoints.rs) | آزمون Endpointهای USB Full-Speed. |
| [`usbhs_cdc_echo.rs`](usbhs_cdc_echo.rs) | نمونه Echo برای USB High-Speed CDC. |
| [`usbhs_endpoints.rs`](usbhs_endpoints.rs) | آزمون Endpointهای USB High-Speed. |
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

# Executable Examples for CH585

This directory contains standalone Rust example binaries. Each source file is generally selected by its file stem in Cargo commands. The descriptions summarize each example; consult the device README for pin assignments, feature flags and wiring details.

## Contents

| File | Description |
|---|---|
| [`adc_pin.rs`](adc_pin.rs) | Read an analog input pin. |
| [`adc_scan_dma.rs`](adc_scan_dma.rs) | ADC channel scanning with DMA. |
| [`adc_temp.rs`](adc_temp.rs) | Internal temperature measurement. |
| [`blinky.rs`](blinky.rs) | Basic LED blink. |
| [`clk_set.rs`](clk_set.rs) | System clock configuration. |
| [`defmt_rtt.rs`](defmt_rtt.rs) | Logging with defmt over RTT. |
| [`embassy_time.rs`](embassy_time.rs) | Embassy timing with the default time driver. |
| [`embassy_time_tmr.rs`](embassy_time_tmr.rs) | Embassy time using a hardware timer driver. |
| [`gpio_async.rs`](gpio_async.rs) | GPIO using asynchronous APIs. |
| [`gpio_async_loopback.rs`](gpio_async_loopback.rs) | Asynchronous GPIO loopback test. |
| [`gpio_in.rs`](gpio_in.rs) | Digital GPIO input. |
| [`i2c_oled.rs`](i2c_oled.rs) | OLED display over I2C. |
| [`i2c_oled_async.rs`](i2c_oled_async.rs) | OLED display using asynchronous I2C. |
| [`i2c_scan.rs`](i2c_scan.rs) | I2C bus address scanner. |
| [`pwm_out.rs`](pwm_out.rs) | PWM output generation. |
| [`rtc_calendar.rs`](rtc_calendar.rs) | RTC calendar test. |
| [`rtc_oled.rs`](rtc_oled.rs) | Display RTC information on OLED. |
| [`sleep_wake.rs`](sleep_wake.rs) | Sleep and wake-up test. |
| [`spi_async_loopback.rs`](spi_async_loopback.rs) | Asynchronous SPI loopback. |
| [`spi_loopback.rs`](spi_loopback.rs) | Blocking SPI loopback. |
| [`timer_dma_async.rs`](timer_dma_async.rs) | Timer, interrupt and asynchronous DMA interaction. |
| [`uart_echo.rs`](uart_echo.rs) | Asynchronous UART echo. |
| [`uart_loopback.rs`](uart_loopback.rs) | UART loopback test. |
| [`usb_cdc_echo.rs`](usb_cdc_echo.rs) | USB CDC device echo. |
| [`usb_endpoints.rs`](usb_endpoints.rs) | USB Full-Speed endpoint test. |
| [`usbhs_cdc_echo.rs`](usbhs_cdc_echo.rs) | USB High-Speed CDC echo. |
| [`usbhs_endpoints.rs`](usbhs_endpoints.rs) | USB High-Speed endpoint test. |
| [`watchdog.rs`](watchdog.rs) | Window watchdog test. |
Build an example from the device package directory:

```console
cargo build --release --bin <binary_name>
```

## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)
