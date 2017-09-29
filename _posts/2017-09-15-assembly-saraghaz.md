---
layout: post
title: "زبان اسمبلی:‌ سرآغاز"
category: assembly-tutorial-persian
date: 2017-09-15 20:30:11 +0430
tags: [لینوکس,گنو,اسمبلی,اسمبلر,۳۲بیت,CPU,x86,programming,c,unix,linux,assembly]
direction: rtl
lang: fa-IR
---
بنام خداوند جان و خرد - کزین برتر اندیشه برنگذرد

خداوند نام و خداوند جای - خداوند روزی ده رهنمای

تو دوره ای که همه دنبال **انجام دادن** کاری هستن و کمتر کسی به **درستی** و یا
 حتی **چجوری** انجام دادن یه کار توجه می‌کنه، هرچقدر بیشتر راجع به ماشین(حساب)
 بدونید به نفعتونه و در عین حال باعث بازتر شدن دیدتون نسبت به سخت‌افزارهای
 مختلف میشه.

(حالا بماند که من چه خواب‌هایی براتون دیدم و قراره بعد از یکم x86 بریم سراغ RISC
 و اسمبلی رو معماری MIPS.)

تو اسمبلی قرار نیست **برنامه** ای بنویسیم و صرفا میخوایم با دونستنش سیستم(ماشین)
 رو بهتر بشناسیم. (حالا اگه شما برا نوشتن شل-کد لازمش داریو برا همینم اینجایی
 اصلا ایرادی نداره و خیلی هم خوش اومدی رفیق!)

به اندازه کافی توضیحات راجع به این زبون هست و من هم همیشه از متد **اول ببینش،
 بعد بفهمش** استفاده می‌کنم. اول می‌سازیمش بعد تیکه پارش می‌کنیم و می‌ریزیمش رو
 میز و دوباره سرهمش میکنیم. (بی‌دلیل هم که اسمشو نزاشتن اسمبلر!)

شناخت معماری کامپیوتر در حد آشنایی با CPU, RAM, I/O برای شروع کافیه و اولین
 برنامه که قراره بسازیم بیشتر UNIXیه تا علمی و "کامپیوتر-ساینس"ی.

وقتی تو C یه برنامه‌ای رو مینویسید، اگه از نوع کتابخونه(library) نباشه،
 بصورت پیشفرض، اول از همه تابع(function) اصلی یا همون main فراخوانی(اجرا) میشه
 و در نهایت این تابع یه عددی رو به سیستم عامل(shell اگه یجور دیگه نگاه کنیم
 بهش) بر میگردونه.

وقتی عمیق تر نگاه کنیم و ببینیم که چه اتفاقاتی تو کرنل و یوزرلند(userland)
 زمان اجرا یه برنامه میفته، می‌بینید که شما همیشه، حتی خواه-نا-خواه با کرنل
 بصورت مستقیم یا غیر مستقیم در ارتباطید.

شروع این ارتباط کجاست؟ زمانی که یه برنامه(binary) - که ممکنه helloworld باشه یا
 یه بازی - رو اجرا می‌کنید و پایان این ارتباط زمانیه که اون برنامه، موفق یا
 ناموفق، خاتمه کارشو به کرنل(یا حتی خود کاربر) اعلام می‌کنه.

تو UNIX از کجا تشخیص داده می‌شه که اجرای یه برنامه موفقیت آمیز بوده یا نه؟
 از طریق exit code یا status code یا همون return value اون برنامه ولی
 **حواستون باشه** که `()return` و `()exit` باهم خیلی خیلی فرق می‌کنن!

درسته(؟) که  اگه `(exit(0` رو آخر یه برنامه بنویسید به ظاهر فرقی با `return 0`
 نداره اما پشت صحنه این دوتا تابع(function) خیلی باهم فرق دارن. هم شبیهن هم
 نیستن!

تابع `return` نتیجه اجرای یه تابع رو به کسی که اونو صدا میزنه(parent, caller)
 برمیگردونه و از اون طرف، `exit` یه سیستم-کال(system call) بحساب میاد که به
 کرنل میگه **این برنامه کارش تموم شده** و دیگه نیازی به
 بازبودن(در حال اجرا بودن) اون نیست و منابعی که استفاده کرده(PID, FD, RAM, etc.)
 می‌تونن به کرنل برگردونده بشن.

خیلی که سخت نشد؟

زمانی که کاربر درخواست اجرا یه برنامرو مطرح می‌کنه، بعد از اینکه shell از درست
 بودن syntax اون دستور(command-line) مطمئن شد، از کرنل می‌خواد تا اون
 برنامرو(که بصورت باینری و به زبان ماشین هست) رو اجرا کنه.

مهمترین فرق زبان‌های کامپایل(ر)ی و مفسری(interpreting) دقیقا همینجاست.
 وقتی شما یه کدی که مثلا تو PHP7 نوشته شده رو اجرا می‌کنید، در اصل
 سیستم عامل(کرنل) برنامه `php` رو اجرا میکنه و اونه(`usr/local/bin/php/` مثلا)
 که سورس کد PHP شما رو می‌خونه.

حالا برعکس اون زمانیه که شما یه کد کامپایل شده رو اجرا می‌کنید. تو این حالت
 دستورات **مستقیما** به CPU(البته از طریق کرنل) فرستاده میشن و هیچ رابط
 و واسطی هم این وسط بجز خود کرنل(که یکی از وظایفش دقیقا همینه!) وجود نداره.

جدا از نوع کد و سرعت(performance) و امنیت اون، یه موضوع خیلی مهم وجود داره
 که باید بهش دقت کنید: Portability

یعنی چی؟ یعنی اینکه کد شما قابل اجرا روی پلتفرم / معماری های دیگه هست یا نه.

تو اسمبلی، **نیست**!

تو C یا PHP یا Python و غیره: **هست**

بازم یعنی چی؟ یعنی اینکه اگه یه کدی رو به زبان C بنویسید، رو کره‌ی ماه هم
 اگه کامپایلر C وجود داشته باشه اون کد قابل تبدیل شدن به زبان ماشین(کامپیوتر)
 آدم فضایی هاست و بعد از کامپایل شدن، بصورت مستقیم(native) می‌تونه رو سیستم
 هاشون اجرا بشه.

همینطور تو PHP: اون رو با استفاده از کامپیوتر خونگیتون که مثلا ویندوزیه
 و معماری x64 داره می‌نویسید ولی روی هاستینگی آپلودش می‌کنید که سخت افزار
 سرورش SPARC یا حتی ARMه و تقریبا هیچ شباهتی به کامپیوتری که روی میزتونه
 نداره.

این وسط زبان مشترکتون چیه؟ PHP

کی اونو اجرا می‌کنه؟ Server

چی رو اجرا می‌کنه؟ برنامه `php` رو. (مثل `php.exe` بهش نگاه کنید اگه از محیط
 ویندوزی میاید.)

حالا PHP تو چه زبونی نوشته شده؟ C

آیا پلتفرم مقصد(sparc64) کامپایلر C دارد؟ آری

زبان C هم زبان portable به حساب میاد؟ قطعا

حالا قسمت های SPARCیه کامپایلر C روی اون پلتفرم تو چی نوشته میشن؟ تو
 اسمبلی / اسمبلر مخصوص اون سخت افزار.

کدهایی که ما قرار بنویسیم به دو دسته کلی تقسیم میشن:

- وابسته به ماشین یا machine-dependent که MD هم میگن بهشن.

- نا-وابسته به ماشین یا machine-independent که MI هم بهش گفته میشه.

تو اسمبلی کدها نتنها MD هتستن بلکه هر اسمبلر syntax و مدل نوشتار خودشو داره!
 حتی تو C این مسئله وجود نداره و نهایتا بحث هایی مثل `ISO C` / `ANSI C` یا
 استاندارد `C99` و غیره وجود دارن. (و البته POSIX! حتما راجع بهش بخونید.)

با این اوصاف بحث Portability همینجا می‌خوره تو دیوار و بازهم برای یادآوری
 یه بار دیگه میگم که **زبان اسمبلی portable نیست**. (اگه بود که اون خدابیامرز
 زبان C رو نمی‌ساخت!)

بسه دیگه، ها؟ بریم سر اصل مطلب!

برنامه ای که قراره بنویسیم اسمش helloworld نیست و بظاهر هم کاری رو انجام نمیده.
 اسم این برنامه `true(1)`ه و کارشم اینه که فقط اجرا بشه. اونم موفقیت آمیز!

برای اینکه این پست خیلی طولانی نشه و تئوری رو از کد جدا نگه دارم، اگه عمری
 باشه تو پست(های!) بعدی سورس کد و نحوه کار و ساختنش رو براتون توضیح میدم.

سلامت و شاد باشید.