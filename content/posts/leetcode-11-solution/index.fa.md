---
title: "حل سوال 11 لیت‌کد"
slug: "leetcode-11-solution"
date: 2023-07-17T14:00:00+03:30
lastmod: 2023-07-17T14:00:00+03:30
tags: ["leetcode", "لیتکد", "حل سوال 11 لیت‌کد", "container with most water"]
author: "علی ثابت"
draft: false
comments: true
description: "در این پست سوال 11 لیت‌کد (container with most water) رو حل می‌کنیم"
---
برای دسترسی به سؤال 11 لیت‌کد می‌تونید از این [لینک](https://leetcode.com/problems/container-with-most-water/) استفاده کنید. سطح این سؤال Medium است.

![leetcode 11](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-300x300.jpg)

در واقع به دنبال مساحت مستطیلی هستیم که کف‌اش محور x هاست و ارتفاع‌هاش، دو میله هستند. چون قراره داخلش با آب پر بشه، پس میله کوچک‌تر به‌عنوان ارتفاع در نظر گرفته می‌شه. فاصله میله‌ها با هم یک واحد است. مساحت مستطیل هم که می‌دونیم برابر حاصل‌ضرب طول در عرض است. بین مستطیل‌های با شرایطِ گفته شده، بیشترین مقدار ممکن رو می‌خواهیم.

شرایط مسئله
-----------

در این مرحله، شرایط خاص مسئله و حالت‌های edge case رو بررسی می‌کنیم. این شرایط باید در توضیحات سوال یا مثال‌ها مشخص شده باشن یا اینکه از پاسخ‌های پیش فرض استفاده کنیم.

*   ضخامت میله ها رو 0 در نظر میگیریم و تاثیری در مساحت نهایی ندارن.
*   سمت راست و چپ نمودار نمی‌تونن بخشی از ستون ها باشن. ستون ها فقط اونهایی هستن که ارتفاعشون داده شده و البته ممکنه ارتفاع یک ستون 0 هم باشه.
*   ستونهای میانی تاثیری در مساحت ندارن، حتی اگه بلندتر از ستون‌های موردنظر ما باشن، مثلا اگه \[1,7,2,8,1,6\] داشته باشیم، بیشترین مساحت رو ستونهای با ارتفاع 7 و 6 میسازن و اون ستون 8 که وسطشون هست، حائلی بین این دو ستون نخواهد بود و تاثیری در مساحت ناحیه مورد نظر ما نداره.

نوشتن test case
---------------

در حالتی که هیچ ستونی نداریم یا فقط یک ستون داریم، امکان ذخیره‌ی آب وجود نداره و خروجی 0 خواهد بود.

در test case سوم، ستون‌های با ارتفاع 7 و 9 امکان ذخیره‌ی بیشترین آب رو دارن. اگر ارتفاع آب از 7 بیشتر بشه، سرریز خواهد کرد. پس در محاسبه‌ی مستطیل، ارتفاع اون رو 7 در نظر می‌گیریم. از طرفی فاصله‌ی بین ستون‌های 7 تا 9، چهار واحد است. پس مساحت مستطیل موردنظر برابر 7\*4 خواهد بود.

![leetcode 11 testcase](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-testcase-300x119.png)

راه حل منطقی
------------

در این مرحله به دنبال working solution هستیم، یعنی راه حلی منطقی که بتونه مسئله رو حل کنه. به راه حل بهینه فکر نمی‌کنیم. درگیر زبان برنامه نویسی و محدودیت‌های اون هم نخواهیم بود.

در [سوال 1](https://alirsabet.com/algorithm/leetcode-1-solution/)، هر زمان که یک جفت عدد پیدا می‌کردیم که مجموع‌شون برابر target بود، کارمون تموم میشد، اما اینجا مقدار مشخصی برای target وجود نداره و targetمون، مقدار ماکزیمم آبیه که می‌تونیم ذخیره کنیم. پس مجبوریم همه‌ی حالات رو بررسی کنیم. مثال \[7,1,2,3,9\] رو در نظر بگیرید. فرمول کلی برای max اینه:

![leetcode 11 formula](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-formula-300x69.png)

مشابه کاری که در سوال 1 لیت‌کد کردیم، پوینتر اول رو a و پوینتر دوم رو b در نظر میگیریم. قبل از همه اینها هم مقدار max رو برابر 0 در نظر میگیریم و هر بار که عدد به دست اومده برای مساحت از max بیشتر شد، max رو برابر اون عدد جدید قرار میدیم. راه حل همینه و کار میکنه.

تبدیل راه حل به کد
------------------

![leetcode 11 solution](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-solution-300x197.png)

پیچیدگی زمانی و حافظه‌ای
------------------------

در این مرحله به بررسی پیچیدگی زمانی و حافظه ای راه حل می‌پردازیم. یعنی تحلیل می‌کنیم که بین زمان اجرای الگوریتم و حافظه مصرفی آن، چه رابطه ای با اندازه ورودی الگوریتم وجود دارد. مشابه با سوال 1، پیچیدگی زمانی برابر O(n2) و پیچیدگی حافظه‌ای برابر O(1) خواهد بود.

بهینه‌سازی
----------

پیچیدگی زمانی O(n2) خوب نیست و باید به فکر بهینه کردنش باشیم. تکنیکی که به اون نیاز داریم، two shifting pointers است. مثال \[4,8,1,2,3,9\] رو در نظر بگیرید. نمیشه با دیدِ سوال 1 به این مسئله نگاه کنیم، به دو دلیل، اول اینکه در اینجا عدد مشخصِ target رو نداریم و دوم اینکه فاصله‌ی پوینترها در اینجا، بر خلاف مسئله‌ی 1، مهمه. با در نظر گرفتن این نکات، پوینتر اول رو روی 4 و پوینتر دوم رو روی 9 می‌ذاریم تا فاصله‌شون بیشترین مقدار بشه، به این امید که ما رو به بیشترین مساحت ممکن که خواسته‌ی سوال است برسونه. در این حالت مساحت برابر خواهد بود با:

![leetcode 11 example](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-example-300x69.png)

اما اگر پوینتر اول رو روی 8 بذاریم و پوینتر دوم روی همون 9 بمونه چطور؟ مساحت برابر میشه با:

![leetcode 11 example 2](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-example-2-300x69.png)

با اینکه فاصله‌ی پوینترها کمتر شد و در واقع یکی از بُعدهای مستطیل کوچکتر شد، مساحت نهایی (که بیشترین مقدارِ اون، مد نظر ماست) بیشتر شد.

از طرفی با توجه به فرمول، اگر عدد بزرگتر، بزرگتر هم بشه، تاثیری روی قسمت اول فرمول نداره. مثلا min(4,9) و min(4,8) خروجی های یکسانی دارن، با اینکه عدد بزرگتر یعنی 8، بزرگتر هم شده و به 9 رسیده. پس چیزی که مهمه، حرکت دادنِ پوینتریه که روی عدد کوچکتره.

طبق ایده‌ای که به کار بردیم، بهتره پوینترها رو در طرفینِ آرایه قرار بدیم، چون اینطوری حداقل از همون ابتدا یک بخش از فرمولِ محاسبه‌ی مستطیل‌مون رو max کرده‌ایم. مثلا در مثال بالا، پوینتر چپ روی 4 و پوینتر راست روی 9 قرار میگیره. در ابتدا، پوینترها فقط میتونن به طرف مرکز حرکت کنن و نمیتونن به سمت طرفین برن، چون راهی ندارن! مقدار مورد نظرِ سوال رو که در پایان گزارش خواهد شد max = 0 در نظر میگیریم.

پس پوینتر راست روی 9، پوینتر چپ روی 4 و مساحت در این حالت min(4,9) \* (5-0) که میشه 20. چون 20 از 0 بیشتره، پس max = 20.

چون عدد کوچکتر برامون مهمه، پس پوینترِ روی عدد کوچکتر که 4 است رو به راست حرکت میدیم، در این حالت پوینتر راست روی 9، پوینتر چپ روی 8 و مساحت در این حالت min(8,9) \* (5-1) که میشه 32. چون 32 از 20 بیشتره، پس max = 32.

چون عدد کوچکتر برامون مهمه، پس پوینترِ روی عدد کوچکتر که 8 است رو به راست حرکت میدیم، در این حالت پوینتر راست روی 9، پوینتر چپ روی 1 و مساحت در این حالت min(1,9) \* (5-2) که میشه 3. چون 3 از 32 کمتره، پس همچنان max = 32.

چون عدد کوچکتر برامون مهمه، پس پوینترِ روی عدد کوچکتر که 1 است رو به راست حرکت میدیم، در این حالت پوینتر راست روی 9، پوینتر چپ روی 2 و مساحت در این حالت min(2,9) \* (5-3) که میشه 4. چون 4 از 32 کمتره، پس همچنان max = 32.

چون عدد کوچکتر برامون مهمه، پس پوینترِ روی عدد کوچکتر که 2 است رو به راست حرکت میدیم، در این حالت پوینتر راست روی 9، پوینتر چپ روی 3 و مساحت در این حالت min(3,9) \* (5-4) که میشه 3. چون 3 از 32 کمتره، پس همچنان max = 32.

دیگه امکان حرکت دادنِ پوینتر نیست، پس مقدار نهایی max = 32 رو برمیگردونیم. در واقع تفاوتِ این تکنیک با two pointers اینه که در هر حرکت، بنا به منطقی که داریم، یکی از پوینترها حرکت خواهد کرد.

![leetcode 11 optimal solution](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-11-optimal-solution-256x300.png)

در الگوریتمِ بهینه‌شده، آرایه فقط یکبار پیمایش شد که باعث میشه پیچیدگی زمانی اون به O(n) برسه و پیچیدگی حافظه‌ای، O(1) بمونه.