<div dir="rtl" align="right">

<p align="center"><img src="../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# یکپارچه‌سازی Embassy و Time Driverها

این پوشه اتصال HAL به زمان‌بند Embassy و منبع زمان ناهمگام را پیاده‌سازی می‌کند.

## فایل‌ها

| فایل | توضیحات |
|---|---|
| `mod.rs` | ماژول و نقطه اتصال Embassy |
| `reload_math.rs`، `reload_timer.rs` | محاسبات و پیکربندی بارگذاری مجدد تایمر |
| `time_driver_systick.rs`، `time_driver_systick_ch573.rs` | Time Driver مبتنی بر SysTick |
| `time_driver_tmr.rs` | Time Driver مبتنی بر تایمرهای سخت‌افزاری |



<p align="center"><img src="../../Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="MES Thank You Footer"></p>

## تهیه و تدوین
**معمار الکترونیک صنعت | MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

---

# Embassy Integration and Time Drivers

This directory implements the HAL integration with the Embassy executor and asynchronous time source.

## Files

| File | Description |
|---|---|
| `mod.rs` | Embassy integration module entry point |
| `reload_math.rs`, `reload_timer.rs` | Timer reload calculations and configuration |
| `time_driver_systick.rs`, `time_driver_systick_ch573.rs` | SysTick-based time drivers |
| `time_driver_tmr.rs` | Hardware-timer-based Embassy time driver |


## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)
