<div dir="rtl" align="right">

# تنظیمات Cargo برای CH572

این پوشه پیکربندی اختصاصی Cargo برای پروژه نمونه CH572 را نگهداری می‌کند. فایل تنظیمات Target، گزینه‌های کامپایل و Runner مورد استفاده برای پروگرام و اجرای Firmware را مشخص می‌کند.

## محتویات

| فایل | توضیحات |
|---|---|
| [config.toml](config.toml) | Target: `riscv32imac-unknown-none-elf`، تنظیمات ساخت و اجرای متناسب با CH572/CH570 (QingKe V3A) |
برای تغییر Probe یا گزینه‌های Debug، ابتدا ساختار و مقادیر موجود در `config.toml` را بررسی کنید. تغییر Target باید با معماری هسته تراشه سازگار باشد.

## تهیه و تدوین
**معمار الکترونیک صنعت | MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

---

# Cargo Configuration for CH572

This directory stores Cargo-specific configuration for the CH572 example package. The configuration file selects the compilation target, build options and firmware runner.

## Contents

| File | Description |
|---|---|
| [config.toml](config.toml) | Target: `riscv32imac-unknown-none-elf`, build options and runner settings for CH572/CH570 (QingKe V3A) |
Inspect the existing `config.toml` before changing probe or debug options. The target must match the MCU core architecture.

## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)
