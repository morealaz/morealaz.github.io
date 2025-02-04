<div dir="auto">
<h1>تنظیمات فونت لینوکس</h1>
<h2>مقدمه</h2>
<p>
تنظیمات فونت در لینوکس بر عهده برنامه <a href="https://www.freedesktop.org/wiki/Software/fontconfig/">fontconfig</a> میباشد. این برنامه فونتهای سیستم را بر اساس الویت بندیهایی که قابل تنظیم میباشد مرتب میکند و در اختیار سایر برنامه ها قرار می دهد. مشکل اصلی که اکثر کاربران فارسی زبان لینوکس در ارتباط با <strong>fontconfig</strong> دارند عدم نمایش صحیح حروف فارسی می باشد که معمولا به دو دلیل زیر اتفاق می‌افتد:

<ul>
<li>نصب نبودن فونت مناسب بر روی سیستم که حروف فارسی را ساپورت کند</li>
<li>عدم وجود فایل تنظیمات <strong>fontconfig</strong> برای انتخاب فونت مناسب  برای نمایش حروف فارسی</li>
</ul>
</p>

<h2>نصب فونت</h2>
<p>
نصب فونت در لینوکس به دو روش انجام میگیرد:

<ol>
<li>از طریق مدیر بسته توزیع</li>
<li>به صورت دستی توسط کاربر</li>
</ol>

<h3>نصب از طریق مدیر بسته توزیع لینوکس</h3>
در این روش همانند نصب سایر برنامه ها در لینوکس با استفاده از مدیر بسته، از بسته های فونت موجود در مخازن توزیع استفاده میکنیم. مزیت این روش استفاده از مدیر بسته برای مدیریت نصب فونتها می باشد و فونتهای نصب شده برای کل کاربران سیستم قابل استفاده می باشند. البته ممکن است فونت مورد نظر ما به صورت بسته در مخازن موجود نباشد که در این صورت از روش دستی برای نصب استفاده میکنیم.

<h3>نصب به صورت دستی توسط کاربر</h3>
در این روش کافی است فایل مربوط به فونت با پسوند <code>ttf</code> یا <code>otf</code> را در مسیرهای خاصی در سیستم کپی نماییم که قابل استفاده توسط <strong>fontconfig</strong> باشند. این روش به دو صورت قابل انجام است:

<h4>نصب برای کاربر</h4>
در این روش فایلها در دایرکتوری <code>home</code> کاربر در مسیر

<pre dir="ltr">
~/.local/share/fonts/
</pre>

کپی می شوند. با این روش فونتها فقط توسط کاربر فعلی قابل استفاده می باشند و کاربران دیگر سیستم به آنها دسترسی ندارند.
بعد از نصب فونتها برای تازه سازی <code>cache</code>  دستور زیر را باید اجرا نمایید:

<pre dir="ltr">
$ fc-cache 
</pre>

<h4>نصب برای کل سیستم</h4>
در این روش فایلها در مسیر

<pre dir="ltr">
/usr/local/share/fonts/
</pre>

کپی می شوند. با این روش فونتها توسط تمام کاربران سیستم قابل دسترسی و استفاده می باشند.
بعد از نصب فونتها برای تازه سازی <code>cache</code>  دستور زیر را باید اجرا نمایید:

<pre dir="ltr">
$ sudo fc-cache -s
</pre>

</p>
<p>
بعد از نصب فونتهای لازم کاربر میتواند در تنظیمات برنامه های مختلف در صورت امکان فونت مورد نظر خود را انتخاب کرده و از آن استفاده نماید ولی عیب این روش این است که اولا ممکن هست تمام برنامه ها امکان تنظیم فونت را نداشته باشند و از فونتهای پیش فرض سیستم استفاده کنند و ثانیه چون با انتخاب یک فونت از آن برای نمایش تمام کاراکترها استفاده می شود ممکن است کاراکترهای لازم برای زبانهای دیگر و عناصر دیگر مثل اموجی در فونت شما وجود نداشته باشد ویا اینکه از آنها خوشتان نیاد که در این صورت امکان انتخاب وجود ندارد.
</p>
<p>
با استفاده از <strong>fontconfig</strong> این امکان برای ما بوجود می آید که تنظیمات یکدستی برای کل سیستم داشته باشیم و سلسله مراتبی برای فونتهای پیش فرض سیستم مشخص کنیم که بر اساس آن از فونتهای مختلف برای نمایش کارکترهای مختلف استفاده شود.
</p>
<p>
روشی که برای تنظیمات بکار می بریم به این صورت است که برای ۳ خانواده کلی فونت یعنی خانواده های:

<ul dir="ltr">
<li>sans-serif</li>
<li>serif</li>
<li>monospace</li>
</ul>

فونتهای مورد نظر خود را به ترتیب اولویت مشخص میکنیم. به این ترتیب هر زمان برنامه ای نیاز به استفاده از یکی از این خانواده فونتها مثلا <code>sans-serif</code> داشت، به ترتیب اولویت از فونتهای مشخص شده استفاده می شود و هرگاه کاراکتری مورد نیاز بود که در آن فونت موجود نبود از فونت بعدی در لیست اولویت فونتهای آن خانواده استفاده می شود. در نتیجه با انتخاب یکی از این خانواده های فونت کلی به عنوان فونت پیش فرض برنامه های مختلف، می توانیم در تمام برنامه ها تنظیمات فونت یکدستی داشته باشیم.
</p>

<h2>انجام تنظیمات</h2>
<p>
انجام تنظیمات هم به صورت لوکال و هم به صورت گلوبال قابل اعمال است. در روش لوکال فایل تنظیمات در مسیر 

<pre dir="ltr">
~/.config/fontconfig/fonts.conf
</pre>

 کاربر قرار میگیرد و فقط برای کاربر اعمال می شود ولی در روش گلوبال فایل تنظیمات در مسیر

<pre dir="ltr">
/etc/fonts/local.conf
</pre>

 قرار میگیرد و به کل سیستم اعمال می شود.
</p>
<p>
فرمت فایل تنظیمات از نوع <code>XML</code> می باشد که المانهای خاص خود را برای تنظیمات مختلف دارد. فایل تنظیمات مورد نظر ما به صورت زیر می باشد:
</p>
</div>

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
 <!-- Default font for the Persian language (no fc-match pattern) -->
  <match>
    <test compare="contains" name="lang">
      <string>fa</string>
    </test>
    <edit mode="prepend" name="family">
      <string>Vazirmatn NL</string>
    </edit>
  </match>
  <!-- preferred fonts (first match will be used) -->
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Source Sans Pro</family>
      <family>Source Han Sans</family>
      <family>Vazirmatn NL</family>
      <family>Noto Sans</family>
      <family>DejaVu Sans</family>
      <family>JoyPixels</family>
    </prefer>
  </alias>
  <alias>
    <family>serif</family>
    <prefer>
      <family>Source Serif Pro</family>
      <family>Source Han Serif</family>
      <family>Noto Serif</family>
      <family>DejaVu Serif</family>
      <family>JoyPixels</family>
    </prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer>
      <family>Source Code Pro</family>
      <family>Source Han Mono</family>
      <family>Noto Sans Mono</family>
      <family>DejaVu Sans Mono</family>
      <family>JoyPixels</family>
    </prefer>
  </alias>
  <!-- hinting/antialiasing settings -->
  <match target="font">
    <edit mode="assign" name="antialias">
      <bool>true</bool>
    </edit>
    <edit mode="assign" name="hinting">
      <bool>true</bool>
    </edit>
    <edit mode="assign" name="hintstyle">
      <const>hintslight</const>
    </edit>
    <edit mode="assign" name="lcdfilter">
      <const>lcddefault</const>
    </edit>
    <edit mode="assign" name="rgba">
      <const>rgb</const>
    </edit>
  </match>
</fontconfig>
```

<div dir="auto">
همانطور که مشاهده میکنید در زیر خانواده های <code>sans-serif</code> و <code>serif</code> و <code>monospace</code> فونتهای مورد نظر برای آن خانواده را به ترتیب اولویت از بالا به پایین مشخص میکنیم.
<br/>
 به عنوان نمونه خانواده <code>sans-serif</code> به این صورت در تنظیمات من مشخص شده است:
</div>

```xml
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Source Sans Pro</family>
      <family>Source Han Sans</family>
      <family>Vazirmatn NL</family>
      <family>Noto Sans</family>
      <family>DejaVu Sans</family>
      <family>JoyPixels</family>
    </prefer>
  </alias>
```

<div dir="auto">
به این ترتیب فونت <code>Source Sans Pro</code> به عنوان فونت اصلی خانواده <code>sans-serif</code> مورد استفاده قرار میگیرد و بعد از آن فونت <code>Source Han Sans</code> قرار دارد که برای نمایش کاراکترهای زبانهای آسیای شرقی شامل چینی و ژاپنی و کره ای مورد استفاده قرار میگیرد که در فونت <code>Source Sans Pro</code> موجود نمی باشند. بعد از آن فونت <code>Vazirmatn NL</code> قرار گرفته که نسخه بدون کاراکترهای لاتین فونت وزیرمتن می باشد و چون در دو فونت قبلی کاراکترهای فارسی وجود ندارد از این فونت برای کاراکترهای فارسی استفاده می شود. در انتها هم فونتهای <code>Noto Sans</code> و <code>DejaVu Sans</code> را قرار داده ام که در صورتیکه کاراکتری در یکی از فونتهای قبلی موجود نبود به احتمال زیاد در این فونتها وجود دارد و از آنها استفاده شود.<br/>
ولی اما فونت آخر که فونت <code>JoyPixels</code> می باشد را در انتهای فونتهای هر سه خانواده قرار داده ام. این فونت یک فونت اموجی است که اموجی های رنگی زیادی دارد و کاراکترهای اموجی را برای برنامه ها فراهم میکند.فونتهای اموجی دیگری هم وجود دارد که میتوانید از آنها استفاده کنید مثل فونت <code>Noto Color Emoji</code> و <code>Twemoji</code>.<br/>
بدین ترتیب برای خانواده های دیگر فونت هم فونتهای مورد نظر را مشخص میکنیم

<h2>نکات مهم!!</h2>
<ol>
<li>در انتخاب فونتها دقت کنید که حتما فونت مورد استفاده از نوع خانواده مورد نظر باشد.مثلا از فونت serif در خانواده monospace استفاده نکنید چون خانواده monospace برای محیطهایی استفاده می شود که نیاز به فونتهای هم عرض دارد مثل محیط ترمینال یا ویرایشگر کد.</li>
<li>بعد از انجام این تنظیمات بایستی در تنظیمات برنامه ها و سیستم خود فونت مورد استفاده را از یکی از این خانواده های کلی فونت قرار دهید تا بتوانید از این تنظیمات استفاده کنید.</li>
</ol>
</div>
