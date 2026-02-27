# ببینتو

ببینتو یک فرانت‌اند استاتیک و فارسی برای مرور، جستجو و مشاهده جزئیات فیلم‌ها، سریال‌ها و پلی‌لیست‌ها است. این پروژه با HTML، Tailwind CSS و Alpine.js ساخته شده و به‌صورت اپن‌سورس نگه‌داری می‌شود.

## ویژگی‌ها

- صفحه خانه برای مرور محتوا و پیشنهادها
- صفحه جستجو با فیلتر و مرتب‌سازی
- صفحه جزئیات فیلم و سریال
- صفحه لیست پلی‌لیست‌ها
- صفحه جزئیات هر پلی‌لیست
- تایپوگرافی فارسی با فونت `AradVF`

## صفحات پروژه

- `index.html`
- `search.html`
- `details.html`
- `playlists.html`
- `playlist-details.html`

## تکنولوژی‌ها

- HTML
- [Tailwind CSS Browser Build](https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4)
- [Alpine.js](https://alpinejs.dev/)
- [Plyr](https://plyr.io/) برای پلیر ویدئو در صفحه جزئیات

## API

این پروژه برای دریافت داده‌ها از API استفاده می‌کند:

- سرویس مرجع: [cinemaplus-app.vercel.app](https://cinemaplus-app.vercel.app/)

## اجرای محلی

چون پروژه استاتیک است، کافی است آن را با یک سرور ساده اجرا کنید. برای مثال:

```bash
python3 -m http.server 8080
```

سپس آدرس زیر را باز کنید:

```text
http://localhost:8080
```

## ساختار فایل‌ها

- [index.html]: صفحه اصلی
- [search.html]: جستجو و فیلتر نتایج
- [details.html]: جزئیات فیلم یا سریال
- [playlists.html]: لیست پلی‌لیست‌ها
- [playlist-details.html]: جزئیات پلی‌لیست
- [arad-font.css]: تنظیمات فونت فارسی
- [AradVF.woff2]: فایل فونت

## مشارکت

اگر می‌خواهی در توسعه پروژه مشارکت کنی، تغییراتت را در یک branch جدا اعمال کن و بعد Pull Request بفرست.
