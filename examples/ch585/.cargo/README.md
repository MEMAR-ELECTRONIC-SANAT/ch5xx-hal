<div dir="rtl" align="right">

<p align="center"><img src="../../../Images/GitHub-Assets/MES-Section-Header.svg" width="100%" alt="MES Section Header"></p>

<p align="center"><img src="../../../Images/GitHub-Assets/MES-Divider.svg" width="100%" alt="MES Divider"></p>

# تنظیمات Cargo برای CH585

این پوشه پیکربندی اختصاصی Cargo برای پروژه نمونه CH585 را نگهداری می‌کند. فایل تنظیمات Target، گزینه‌های کامپایل و Runner مورد استفاده برای پروگرام و اجرای Firmware را مشخص می‌کند.

## محتویات

| فایل | توضیحات |
|---|---|
| [config.toml](config.toml) | Target: `riscv32imc-unknown-none-elf`، تنظیمات ساخت و اجرای متناسب با CH585 (QingKe V3C) |
برای تغییر Probe یا گزینه‌های Debug، ابتدا ساختار و مقادیر موجود در `config.toml` را بررسی کنید. تغییر Target باید با معماری هسته تراشه سازگار باشد.


<p align="center"><img src="../../../Images/GitHub-Assets/MES-Thank-You-Footer.svg" width="100%" alt="MES Thank You Footer"></p>

## تهیه و تدوین
**معمار الکترونیک صنعت | MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

---

# Cargo Configuration for CH585

This directory stores Cargo-specific configuration for the CH585 example package. The configuration file selects the compilation target, build options and firmware runner.

## Contents

| File | Description |
|---|---|
| [config.toml](config.toml) | Target: `riscv32imc-unknown-none-elf`, build options and runner settings for CH585 (QingKe V3C) |
Inspect the existing `config.toml` before changing probe or debug options. The target must match the MCU core architecture.

## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

<p align="center">
  <img src="../../../Images/GitHub-Assets/MES_Animated_Logo_640x480.svg" width="140" alt="MES Animated Logo">
</p>
