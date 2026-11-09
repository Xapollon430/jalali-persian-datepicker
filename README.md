# انتخابگر تاریخ شمسی

`jalali-persian-datepicker` یک انتخابگر تاریخ شمسی برای فرم‌های وب است. کاربر تاریخ را در تقویم فارسی انتخاب می‌کند یا در فیلد متنی می‌نویسد. پکیج مقدار شمسی را به کاربر نشان می‌دهد و معادل میلادی آن را در قالب `YYYY-MM-DD` برای ارسال فرم یا ذخیره‌سازی آماده می‌کند. خروجی فقط شامل تاریخ است. پکیج با جاوااسکریپت خالص نوشته شده و وابستگی اجرایی ندارد.

## پیش‌نمایش

[دموی تعاملی را باز کنید](https://withoutthefiling.github.io/jalali-persian-datepicker/example.html) و یک تاریخ شمسی انتخاب کنید تا معادل میلادی آن را ببینید.

| نمای تقویم | انتخاب ماه | انتخاب سال |
| --- | --- | --- |
| <img src="https://raw.githubusercontent.com/withoutthefiling/jalali-persian-datepicker/main/screenshots/calendar_clean.png" width="220" alt="جدول روزهای تقویم شمسی"> | <img src="https://raw.githubusercontent.com/withoutthefiling/jalali-persian-datepicker/main/screenshots/month_selector_clean.png" width="220" alt="فهرست انتخاب ماه شمسی"> | <img src="https://raw.githubusercontent.com/withoutthefiling/jalali-persian-datepicker/main/screenshots/year_selector_clean.png" width="220" alt="فهرست انتخاب سال شمسی"> |

[![پیش‌نمایش تقویم شمسی با ورودی شمسی و خروجی میلادی](https://raw.githubusercontent.com/withoutthefiling/jalali-persian-datepicker/main/preview.png)](https://withoutthefiling.github.io/jalali-persian-datepicker/example.html)

## امکانات

- رابط فارسی و راست‌چین با ارقام فارسی، شروع هفته از شنبه، و انتخاب مستقیم ماه و سال.
- انتخاب از تقویم یا تایپ تاریخ با ارقام فارسی، عربی یا لاتین. ورودی‌هایی مثل `۱۴۰۵/۷/۲۸` و `1405-07-28` پس از تأیید به شکل `۱۴۰۵/۰۷/۲۸` نمایش داده می‌شوند.
- اعتبارسنجی تاریخ با در نظر گرفتن طول ماه‌ها و سال کبیسه. سال‌های شمسی ۱۰۰۰ تا ۱۹۹۹ پشتیبانی می‌شوند و می‌توانید بازه را با حداقل و حداکثر تاریخ محدود کنید.
- نمایش مقدار میلادی ذخیره‌شده به صورت شمسی هنگام باز کردن فرم ویرایش و همگام‌سازی فیلد میلادی پس از تغییر تاریخ.
- دکمهٔ «انتخاب امروز» بر اساس منطقهٔ زمانی قابل تنظیم، با پیش‌فرض `Asia/Tehran`، و دکمهٔ اختیاری «پاک کردن».
- نمایش شناور کنار ورودی در صفحه‌های بزرگ و نمایش در پایین صفحه وقتی فضای نمایش محدود است. جای تقویم را می‌توان برای فرم‌های داخل مودال تنظیم کرد.
- پیمایش با صفحه‌کلید، برچسب‌های دسترس‌پذیری فارسی، پوستهٔ تیره و امکان تغییر رنگ‌ها با متغیرهای CSS.

## نصب و استفاده

### نصب از GitHub

در ریشهٔ پروژهٔ مصرف‌کننده اجرا کنید.

```bash
npm install git+https://github.com/withoutthefiling/jalali-persian-datepicker.git
```

### نصب محلی با npm

در پوشهٔ خود پکیج، فایل قابل نصب را بسازید.

```bash
npm pack
```

فایل `jalali-persian-datepicker-1.2.0.tgz` را به ریشهٔ پروژهٔ مصرف‌کننده منتقل کنید و همان‌جا نصب را اجرا کنید. اگر نسخهٔ پکیج تغییر کرده، نام فایلی را که `npm pack` چاپ می‌کند به کار ببرید.

```bash
npm install ./jalali-persian-datepicker-1.2.0.tgz
```

### استفاده پس از نصب

این HTML را در فرم بگذارید. ویژگی `name` روی فیلد میلادی است تا هنگام ارسال فرم مقدار `payment_date` به سرور برسد. اگر فرم ویرایش است، تاریخ میلادی ذخیره‌شده را در `value` فیلد مخفی بگذارید و ورودی نمایشی را خالی بگذارید.

```html
<label for="paid-at">تاریخ واریز (شمسی)</label>
<input
  id="paid-at"
  type="text"
  dir="ltr"
  inputmode="numeric"
  autocomplete="off"
  placeholder="۱۴۰۵/۰۷/۲۸"
  data-jalali-datepicker
  data-jalali-alt="#paid-at-iso"
  data-jalali-trigger="#paid-at-trigger"
  data-jalali-clear
>
<button id="paid-at-trigger" type="button">انتخاب تاریخ</button>
<input id="paid-at-iso" type="hidden" name="payment_date">
```

در فایل ورودی جاوااسکریپت پروژه، ماژول و CSS را با ابزار ساختی که از `import` فایل CSS پشتیبانی می‌کند بارگذاری کنید. بعد از اینکه ورودی‌ها در DOM قرار گرفتند، آن‌ها را فعال کنید.

```js
import JalaliPersianDatepicker from 'jalali-persian-datepicker';
import 'jalali-persian-datepicker/style.css';

JalaliPersianDatepicker.mountAll();
```

### استفاده مستقیم در HTML

فایل‌های `index.js` و `style.css` را به همراه پوشهٔ `fonts/` در پوشه‌ای مثل `jalali-datepicker` کنار صفحه کپی کنید. اسکریپت و CSS را در `head` بارگذاری کنید و همان HTML فرم بالا را به کار ببرید.

```html
<link rel="stylesheet" href="./jalali-datepicker/style.css">
<script defer src="./jalali-datepicker/index.js"></script>
```

در این حالت اسکریپت ورودی‌های دارای `data-jalali-datepicker` را بعد از آماده شدن DOM خودکار فعال می‌کند و API از طریق `window.JalaliPersianDatepicker` در دسترس است. برای دیدن نمونهٔ مستقل، [example.html](./example.html) را در مرورگر باز کنید.

### تنظیم از طریق HTML

| ویژگی | کاربرد |
| --- | --- |
| `data-jalali-datepicker` | ورودی را برای شناسایی توسط `mountAll()` علامت می‌زند. |
| `data-jalali-alt="#paid-at-iso"` | انتخابگر CSS فیلدی که تاریخ میلادی را دریافت می‌کند. اگر ورودی نمایشی خالی باشد، تاریخ میلادی معتبرِ اولیه از همین فیلد خوانده می‌شود. |
| `data-jalali-trigger="#paid-at-trigger"` | انتخابگر CSS دکمهٔ اختیاری باز کردن تقویم. خود ورودی نیز با کلیک تقویم را باز می‌کند. |
| `data-jalali-min="2026-10-01"` و `data-jalali-max="2026-10-31"` | حداقل و حداکثر تاریخ مجاز به قالب میلادی `YYYY-MM-DD`. هر دو کران در بازه‌اند و برای انتخاب و ورود دستی اعمال می‌شوند. |
| `data-jalali-timezone="Asia/Tehran"` | منطقهٔ زمانی محاسبهٔ «امروز». |
| `data-jalali-clear` | با افزودن این ویژگی، دکمهٔ «پاک کردن» نمایش داده می‌شود. |

هنگام تایپ، فیلد میلادی همگام می‌شود. اگر تاریخ خالی، نامعتبر یا خارج از بازه باشد، فیلد میلادی خالی می‌ماند. پس از تأیید ورودی دستی، تاریخ معتبر با ارقام فارسی و با قالب سال/ماه/روز نمایش داده می‌شود.

## API جاوااسکریپت

برای پیکربندی یک ورودی از جاوااسکریپت، `mount` را پیش از فعال‌سازی دسته‌ای روی آن اجرا کنید. اگر از اسکریپت مستقیم و فعال‌سازی دستی استفاده می‌کنید، ویژگی `data-jalali-datepicker` را از همان ورودی بردارید تا فعال‌سازی خودکار زودتر انجام نشود.

```js
const picker = JalaliPersianDatepicker.mount('#paid-at', {
  altInput: '#paid-at-iso',
  trigger: '#paid-at-trigger',
  min: '2026-10-01',
  max: '2026-10-31',
  allowClear: true,
  onChange(date) {
    console.log(date?.gregorian ?? '');
  }
});

picker.setDate('2026-10-20');
picker.getDate()?.display; // '۱۴۰۵/۰۷/۲۸'
```

| متد یا گزینه | کاربرد |
| --- | --- |
| `mount(input, options?)` | یک ورودی را با انتخابگر CSS یا عنصر DOM فعال می‌کند و کنترلر آن را برمی‌گرداند. فراخوانی دوباره همان کنترلر را برمی‌گرداند. |
| `mountAll(root?, options?)` | ورودی‌های علامت‌گذاری‌شده زیر `root` را فعال می‌کند و آرایه‌ای از کنترلرها را برمی‌گرداند. پس از افزودن فرم با AJAX می‌توانید `JalaliPersianDatepicker.mountAll(container)` را روی عنصر حاوی فرم اجرا کنید. |
| `getDate()` | شیء تاریخ معتبر یا `null`. فیلدهای `jalali`، `display` و `gregorian` به‌ترتیب تاریخ شمسی با ارقام لاتین، تاریخ شمسی با ارقام فارسی و تاریخ میلادی هستند. در فرم AJAX می‌توانید تاریخ میلادی را با `picker.getDate()?.gregorian` بخوانید. |
| `setDate(iso, { notify: true })` | تاریخ میلادی را به‌صورت شمسی نمایش می‌دهد. مقدار `null` یا رشتهٔ خالی تاریخ را پاک می‌کند. برای تاریخ نامعتبر یا خارج از بازه، `false` و در صورت موفقیت `true` برمی‌گرداند. با `notify: true` رویدادهای `input` و `change` هم ارسال می‌شوند. |
| `open()`، `close()`، `destroy()` | تقویم را باز یا بسته می‌کنند یا کنترلر را از ورودی جدا می‌کنند. |
| `onChange(date)` | هنگام انتخاب از تقویم، پاک کردن یا تأیید ورود دستی فراخوانی می‌شود. برای تاریخ خالی یا نامعتبر مقدار `null` دریافت می‌کند. |
| `altInput`، `trigger`، `min`، `max`، `timeZone`، `allowClear` | معادل تنظیمات HTML هستند. `altInput` و `trigger` عنصر DOM یا انتخابگر CSS می‌پذیرند. |
| `container`، `boundary` | میزبان تقویم و محدودهٔ عمودی جانمایی را با عنصر DOM یا انتخابگر CSS تعیین می‌کنند. میزبان پیش‌فرض نزدیک‌ترین `dialog` یا والد با `role="dialog"` است و در نبود آن `body` به کار می‌رود. می‌توانید بدنهٔ اسکرول‌پذیر مودال را به‌عنوان `boundary` مشخص کنید. |

توابع تبدیل تاریخ جدا از رابط کاربری هم قابل استفاده‌اند. تبدیل تاریخ نامعتبر رشتهٔ خالی برمی‌گرداند.

```js
JalaliPersianDatepicker.toGregorian('۱۴۰۵/۰۷/۲۸'); // '2026-10-20'
JalaliPersianDatepicker.toJalali('2026-10-20');     // '۱۴۰۵/۰۷/۲۸'
JalaliPersianDatepicker.today('Asia/Tehran');      // تاریخ امروز به شمسی با ارقام فارسی
```

## صفحه‌کلید و ظاهر

فونت پیش‌فرض پنجرهٔ تقویم وزیرمتن است. فایل فونت متغیر و [مجوز SIL OFL 1.1](./fonts/OFL.txt) همراه پکیج هستند و فونت از مسیر محلی در CSS بارگذاری می‌شود. [نسخهٔ اصلی Vazirmatn](https://github.com/rastikerdar/vazirmatn/tree/v33.003)

- روی ورودی، کلید جهت پایین تقویم را باز می‌کند و فوکوس را به روز فعال می‌برد.
- در جدول روزها، کلیدهای جهت‌دار برای جابه‌جایی، `Home` و `End` برای رفتن به ابتدا و انتهای هفته، و `PageUp` و `PageDown` برای تغییر ماه هستند. با نگه داشتن `Shift` همراه دو کلید آخر، سال تغییر می‌کند.
- `Enter` روز فعال را انتخاب می‌کند. `Escape` فهرست ماه یا سال را در صورت باز بودن می‌بندد و در خود تقویم، پنجره را می‌بندد.

برای فعال کردن حالت تیره، `data-theme="dark"` یا `data-bs-theme="dark"` را روی یکی از والدهای پنجرهٔ تقویم بگذارید، مثلاً روی `html`. برای هماهنگی با پوستهٔ سایت، متغیرهایی مثل `--jalali-accent`، `--jalali-surface`، `--jalali-ink`، `--jalali-muted` و `--jalali-z-index` را روی `:root` یا میزبان تقویم تنظیم کنید.

## مجوز

کد پکیج با [مجوز MIT](./LICENSE) منتشر می‌شود. مجوز فونت وزیرمتن در [پوشهٔ فونت‌ها](./fonts/OFL.txt) آمده است.
