# دسکتاپ من

![دسکتاپ من](../cover.jpg)

چند روز پیش عکس از دسکتاپم رو توی یه ساب ردیت گذاشتم و خیلی vscode محو شده رو دوست داشتن

پست رو میتونید<a href="https://www.reddit.com/r/unixporn/comments/c0hlt8/kwinkde_neon_my_blurry_setup/">اینجا</a> مشاهده کنید

من همیشه دوست داشتم که محیط توسعم محو و قشنگو جذاب باشه

اما راهی برای اینکار توی لینوکس و دسکتاپ های بر پایه گنوم  پیدا نکردم

# دسکتاپ های تست شده

* KDE Neon
* KDE Plasma
* Ubuntu 18.04

این باید روی بقیه دسکتاپ های گنوم بیس هم کار کنه

# <a href="https://wiki.gnome.org/action/show/Projects/DevilsPie?action=show&redirect=DevilsPie">DevilsPie به کمک ما میاد</a>

DevilsPie نرم افزار خوبه هست که یک سری اسکریپت رو که بهش میدیم زمان باز شدن پنجره ای اجرا میکنه

این یعنی ما میتونیم چیزی رو زمانی که vscode اجرا میشه اجرا کنیم! این جادوشه!

## نصبش کن!

`sudo apt install devilspie`

## پوشه اسکریپت هاش رو بساز

`mkdir ~/.devilspie`

## اسکریپ رو بساز

`nano ~/.devilspie/vscode.ds`

### این کد رو پیست کن

### KDE با blur

```
(if (contains (window_class) "Code")
    (begin
        (spawn_async (str "xprop -id " (window_xid) " -f _KDE_NET_WM_BLUR_BEHIND_REGION 32c -set _KDE_NET_WM_BLUR_BEHIND_REGION 0 "))
        (spawn_async (str "xprop -id " (window_xid) " -f _NET_WM_WINDOW_OPACITY 32c -set _NET_WM_WINDOW_OPACITY 0xdfffffff"))
    )
)
```

### Ubuntu بدون blur
```
( if
( contains ( window_class ) "Code" )
( begin
( spawn_async (str "xprop -id " (window_xid) " -f _NET_WM_WINDOW_OPACITY 32c -set _NET_WM_WINDOW_OPACITY $(printf 0x%x $((0xffffffff * 87 / 100)))") )
)
)
```

`ctrl+o` برای نوشتن فایل

و

`ctrl+x` برای خروج از نانو

## تستش کن

یه ترمینال باز کن و بنویس

`devilspie`

و vscode رو باز کن

vscode رو ببند و devilspie رو با `ctrl + c` متوقف کن

## فعالش کن

با فعال سازی دیگه نیاز نداره که دوباره و هر بار دستور رو توی ترمینال بزنی

`nano ~/.config/autostart/devile.desktop`

### این کد رو پیست کن

```
[Desktop Entry]
Name="devilspie"
GenericName="devilspie"
Comment="Run devilspie at startup"
Exec=/usr/bin/devilspie
Terminal=false
Type=Application
X-Gnome-Autostart=true
```

`ctrl+o` برای نوشتن فایل

و

`ctrl+x` برای خروج از نانو

به این ادرس برو System Settings > Startup and Shutdown > Autostart

و devilspie  رو فعال کن

و در نهایت خاموش و روشن کن

و از blur لذت ببر!

# اضافه

شما میتونی از تم `SynthWave '84` برای قشنگی استفاده کنی!

منبع اسکریپت <a href="https://dev.to/emmanuelnk/how-to-be-cool-and-make-vscode-transparent-56ib">
Emmanuel N Kyeyune</a>