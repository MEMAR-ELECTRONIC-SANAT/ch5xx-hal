<div dir="rtl" align="right">

# فایل‌های اجرایی مثال‌های CH572

در این پوشه فایل‌های مستقل Rust قرار دارند. هر فایل معمولاً یک Binary جداگانه است که از طریق نام فایل در فرمان‌های Cargo انتخاب می‌شود. توضیح‌ها عملکرد کلی مثال را معرفی می‌کنند؛ جزئیات پایه‌ها، Featureها و سیم‌بندی را در README اختصاصی تراشه بررسی کنید.

## محتویات

| فایل | توضیحات |
|---|---|
| [`pwm_selftest.rs`](pwm_selftest.rs) | آزمون PWM1 تا PWM5، خواندن رجیسترها و بررسی تنظیمات دوره PWM. |
برای ساخت یک مثال از ریشه پروژه تراشه اجرا کنید:

```console
cargo build --release --bin <binary_name>
```

## تهیه و تدوین
**معمار الکترونیک صنعت | MEMAR ELECTRONIC SANAT (MES)**  
همراه شما در مسیر طراحی و ساخت مدارهای مطمئن  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)

</div>

---

# Executable Examples for CH572

This directory contains standalone Rust example binaries. Each source file is generally selected by its file stem in Cargo commands. The descriptions summarize each example; consult the device README for pin assignments, feature flags and wiring details.

## Contents

| File | Description |
|---|---|
| [`pwm_selftest.rs`](pwm_selftest.rs) | PWM1–PWM5 self-test, register readback and PWM period checks. |
Build an example from the device package directory:

```console
cargo build --release --bin <binary_name>
```

## Prepared and Maintained By
**Memar Electronic Sanat (MES)**  
*Your partner in the design and development of reliable circuits.*  
[Telegram](https://t.me/Memar_Electronic) · [Instagram](https://www.instagram.com/Memar.Electronic) · [GitHub](https://github.com/MEMAR-ELECTRONIC-SANAT)
