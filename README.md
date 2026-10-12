# 🛍️ سامانه هوشمند اتصال فروشگاه به دیوار و انتشار خودکار محصولات
### Divar & WooCommerce Automated Sync Engine

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-brightgreen?style=for-the-badge&logo=github)](https://kavexiron-png.github.io/divar-store-sync/)
[![Python](https://img.shields.io/badge/Python-3.9%20%7C%203.10%20%7C%203.11%20%7C%203.12-blue?style=for-the-badge&logo=python)](https://python.org)
[![WooCommerce](https://img.shields.io/badge/WooCommerce-REST%20API%20v3-96588a?style=for-the-badge&logo=woocommerce)](https://woocommerce.com)
[![Divar](https://img.shields.io/badge/Divar-Open%20Platform%20OAuth2-a62626?style=for-the-badge)](https://divar.ir)
[![Database](https://img.shields.io/badge/Database-SQLite%20Cache-003B57?style=for-the-badge&logo=sqlite)](https://sqlite.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Developer](https://img.shields.io/badge/Developer-kavexiron-orange?style=for-the-badge)](https://kavexiron.com)

---

## 📖 معرفی سامانه (Overview)
این پروژه یک موتور اتوماسیون مستقل، پرسرعت و پایدار برای اتصال فروشگاه‌های اینترنتی (ووکامرس، وردپرس و وب‌سایت‌های اختصاصی) به **پلتفرم باز دیوار (Divar Open Platform)** است.

هدف اصلی این سامانه، برطرف کردن نیاز فروشگاه‌داران به وارد کردن دستی صدها محصول در دیوار و جلوگیری از مغایرت قیمت کالاها با مشتریان است. این موتور به صورت ۲۴ ساعته کاتالوگ فروشگاه را رصد کرده و هرگونه تغییر قیمت، تخفیف، تغییر موجودی انبار یا محصول جدید را بلافاصله در دیوار اعمال می‌کند.

---

## 🌟 ویژگی‌های کلیدی (Key Features)
* **انتشار خودکار و دسته‌ای کاتالوگ:** استخراج نام، تصویر شاخص، قیمت، گالری و توضیحات فنی و تبدیل به ساختار رسمی آگهی‌های دیوار.
* **بروزرسانی لحظه‌ای قیمت و موجودی:** رصد دائمی تغییرات با Cron Job و اعمال در کسری از ثانیه در دیوار.
* **بدون افزونه سنگین وردپرس:** اجرای مستقل با پایتون؛ هاست سایت دچار افت سرعت، تداخل یا بار ترافیکی نمی‌شود.
* **کشینگ هوشمند محلی (SQLite Local Cache):** تنها کالاهایی که قیمت یا موجودی آن‌ها تغییر کرده است شناسایی و برای ارسال صف‌بندی می‌شوند.
* **مدیریت سقف درخواست (Rate-Limit Handling):** پایش نرخ درخواست و کدهای خطای HTTP 429 پلتفرم دیوار جهت حفظ سلامت توکن فروشگاه.
* **داشبورد تعاملی دمو (Web App Mockup):** همراه با پیش‌نمایش گرافیکی صفحه آگهی در اپلیکیشن دیوار و کنسول لاگ زنده API.

---

## 🏗️ دیاگرام معماری سیستم (System Architecture)

```
┌─────────────────────────────┐        ┌─────────────────────────────┐
│   فروشگاه اینترنتی کاربر    │        │  پلتفرم رسمی باز دیوار      │
│  (WooCommerce REST API v3)  │        │   (Divar Open Platform)     │
└──────────────┬──────────────┘        └──────────────▲──────────────┘
               │                                      │
               │ HTTP GET (Products)                  │ HTTP POST/PATCH
               ▼                                      │ (Manage Ads)
┌─────────────────────────────────────────────────────┴──────────────┐
│                  موتور همگام‌ساز پایتون (kavexiron)                 │
│    • Product Catalog Fetcher      • Rate-Limiter Engine            │
│    • Price Difference Detector    • Category/Payload Mapper        │
└──────────────────────────────┬─────────────────────────────────────┘
                               │
               ┌───────────────▼───────────────┐
               │    پایگاه داده محلی (SQLite)  │
               │  Cached Hash, SKU, Last Prices│
               └───────────────────────────────┘
```

---

## 🚀 نحوه نصب و راه‌اندازی سریع (Quick Start)

### ۱. اجرای وب‌اپلیکیشن دمو (Live UI & Mockup)
فایل `index.html` را در هر مرورگری (Chrome, Edge, Firefox, Safari) باز کنید یا از طریق **[لینک آنلاین GitHub Pages](https://kavexiron-png.github.io/divar-store-sync/)** به صورت زنده تست نمایید.

### ۲. اجرای موتور پایتون (Python Sync Engine)
```bash
# نصب وابستگی‌ها
pip install requests

# اجرای تست جامع ماژول‌ها در حالت شبیه‌ساز (Mock Test)
python3 divar_sync_engine.py test

# اجرای همگام‌سازی واقعی با کاتالوگ فروشگاه
export WC_URL="https://yourshop.com"
export WC_KEY="ck_your_consumer_key"
export WC_SECRET="cs_your_consumer_secret"
export DIVAR_TOKEN="your_divar_api_token"

python3 divar_sync_engine.py sync
```

---

## 📄 مجوز (License)
این پروژه تحت مجوز MIT منتشر شده است.

## 👤 توسعه‌دهنده (Developer)
توسعه داده شده توسط **kavexiron** | متخصص اتوماسیون، توسعه ربات‌ها و امنیت وب
