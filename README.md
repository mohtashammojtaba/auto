# نصب خودکار Passwall2 و AmneziaWG بر روی OpenWrt



## نصب سریع 
### نسخه پایدار
-پسوال۲ و امنزیا همزمان با تمام مخلفات (‌پیشنهاد برای روترهای قوی دارای رم ۵۱۲ مگ به بالا) :
```sh
root@OpenWrt:~# cd /tmp/ && wget -O install.sh https://raw.githubusercontent.com/iranopenwrt/auto/main/install.sh && sh install.sh --passwall2 --ir --rebind --amnezia
```
### نسخه آزمایشی ⚠️ **خطر آجرشدگی**:  
این نسخه شامل آخرین امکانات برای کاربران پیشرفته تر در نظر گرفته شده

```sh
root@OpenWrt:~# cd /tmp/ && wget -O install.sh https://github.com/iranopenwrt/auto/raw/refs/heads/main/install.sh &&  sh install.sh --passwall2 --ir --rebind --amnezia
```


این پروژه یک اسکریپت ساده برای نصب ابزارهای **Passwall2** و **AmneziaWG** روی سیستم‌عامل OpenWrt است.

⚠️ **نکته مهم**: این اسکریپت برای روترهایی طراحی شده که OpenWrt نسخه `24.10.6` روی آن‌ها نصب شده است. اگر نسخه قدیمی‌تری دارید، ابتدا روتر خود را به‌روزرسانی کنید.

---

## پیش‌نیازها

* روتر شما باید **OpenWrt 24.10.6** داشته باشد.
  (برای چک کردن: دستور زیر را در ترمینال روتر اجرا کنید:)

  ```sh
  cat /etc/openwrt_release
  ```
* دسترسی روتر به اینترنت.
* دسترسی SSH به روتر.

📌 اگر روتر شما از نسخه قدیمی OpenWRT استفاده میکند ، از **[Firmware Selector OpenWrt](https://firmware-selector.openwrt.org/)** برای به‌روزرسانی استفاده کنید.
بسته‌های زیر را مانند تصویر زیر در انتهای بسته های لیست شده در installed packages وارد کنید :
```
coreutils coreutils-base64 coreutils-nohup curl ip-full kmod-inet-diag kmod-netlink-diag kmod-nft-socket kmod-nft-tproxy libc libuci-lua lua luci-compat luci-lib-jsonc luci-lua-runtime resolveip unzip wget-ssl kmod-tun dnsmasq-full
```

> [!CAUTION]
> هشدار ! بسته dnsmasq را جهت جلوگیری از تداخل با بسته dnsmasq-full از لیست بسته های نصبی مانند تصویر زیر حذف کنید


> [!TIP]
> پیشنهاد میشود برای جلوگیری از تداخل آی پی در شبکه رنج پیشفرض ۱.۱ را با دستورات انجام شده مطابق با تصویر زیر انجام دهید.
> ```sh
> uci set network.lan.ipaddr='192.168.103.1'
> uci commit network
> ```


<img width="1060" height="919" alt="image" src="https://github.com/user-attachments/assets/ce880844-5d9a-48e4-815c-c6cd01490ec7" />


---

## نحوه استفاده از برنامه

### ۱. دانلود اسکریپت

```sh
cd /tmp/
wget -O install.sh https://github.com/iranopenwrt/auto/releases/latest/download/install.sh
chmod +x install.sh
```

### ۲. اجرای اسکریپت

```sh
./install.sh
```

* ابتدا چک‌های پیش‌نیاز (اینترنت، DNS، اتصال به GitHub) انجام می‌شود. در صورت مواجه شدن با خطا در هر یک از پیشنیازها لازم است نسبت به رفع ایراد اقدام گردد.  
* در صورت چک شدن پیشنیازها از شما پرسیده می‌شود که آیا Passwall2 یا AmneziaWG را نصب کنید (پاسخ با `y/n`).

---

## گزینه‌های اختیاری (اجرای خودکار بدون پرسش)

* `--passwall2`: نصب Passwall2 بدون پرسش.
* `--ir`: فعال‌سازی لیست‌های جغرافیایی ایرانی (توصیه برای کاربران ایرانی).
* `--rebind`: اجازه دادن به سایتهای ایرانی برای استفاده از ضعف امنیتی rebind.
* `--amneziawg`: نصب AmneziaWG بدون پرسش.

### مثال:
نصب امنیزیا وایرگارد بهمراه pbr و آدرسهای آي پی ایران مناسب برای همه روترهای دارای پشتیبانی از آخرین نسخه OpenWrt:
```sh
cd /tmp/ && wget -O install.sh https://github.com/iranopenwrt/auto/releases/latest/download/install.sh && sh install.sh --amnezia --pbr --ir
```

نصب پسوال ۲ بهمراه لیست وبسایتها و آدرسهای آیپی ایران مناسب برای روترهای دارای حداقل پردازنده Arm 64 دو هسته ای و ۲۵۶ مگابایت رم(‌۵۱۲ مگ رم به بالا پیشنهاد میشود):
```sh
cd /tmp/ && wget -O install.sh https://github.com/iranopenwrt/auto/releases/latest/download/install.sh && sh install.sh --passwall2 --ir --rebind
```
 نصب پسوال۲ بهمراه لیست وبسایتها و آدرسهای آیپی ایران و AmneziaWG. برای استفاده ترکیبی از پروتوکل ها حداقل پردازنده Arm 64 چهار هسته ای و ۱ گیگابایت رم:

```sh
cd /tmp/ && wget -O install.sh https://github.com/iranopenwrt/auto/releases/latest/download/install.sh && sh install.sh --passwall2 --ir --rebind --amneziawg
```
---

## پس از نصب

* به رابط وب **LuCI** بروید (معمولاً در `192.168.1.1`).
* در بخش **Services > Passwall2** یا **AmneziaWG**، تنظیمات خود را پیکربندی کنید.
* در صورت نیاز، روتر را ری‌استارت کنید:

  ```sh
  reboot
  ```

---

## خروجی اسکریپت و رفع مشکلات

اسکریپت خروجی‌های رنگی و واضحی تولید می‌کند:

* `[INFO]` (آبی): اطلاعات معمولی، مشکلی نیست.
* `[SUCCESS]` (سبز): موفقیت در عملیات.
* `[WARNING]` (زرد): هشدار (مثلاً نسخه OpenWrt قدیمی است).
* `[ERROR]` (قرمز): خطا (اسکریپت متوقف می‌شود).

### خطاهای رایج و راه‌حل‌ها:

* **No internet connectivity** → بررسی اتصال اینترنت (`ping 8.8.8.8`).
* **DNS resolution failed** → بررسی عملکرد دی ان اس در لوسی.
* **GitHub connectivity failed** → ایراد دسترسی به گیتهاب؛ .
* **Failed to access package** → ایراد دسترسی به رپوها

---

## نمونه خروجی موفق

```text
[INFO] Starting pre-installation checks...
[INFO] Checking internet connectivity by pinging 8.8.8.8...
PING 8.8.8.8 (8.8.8.8): 56 data bytes
...
[SUCCESS] Internet connectivity test passed.
...
[SUCCESS] All requested installations completed.
```

---

## محدودیت‌ها و نکات

* این اسکریپت فقط روی **OpenWrt** کار می‌کند (نه روی فریم‌ور اصلی روترهای کارخانه‌ای).
* بعد از نصب، حتماً برای امنیت پسورد قوی تنظیم کنید.
* مطمئن شوید محدوده آی پی روتر OpenWRT با مودم متصل به آن **متفاوت** باشد

---

## لایسنس

این پروژه تحت لایسنس **GNU General Public License v2** منتشر شده است.
جزئیات در فایل‌های اسکریپت موجود است.

---

اگر مشکلی داشتید، لطفاً در بخش **Issues** این ریپو گزارش دهید.
موفق باشید! 🚀

                        
## Stargazers over time
[![Stargazers over time](https://starchart.cc/iranopenwrt/auto.svg?variant=dark)](https://starchart.cc/iranopenwrt/auto)
