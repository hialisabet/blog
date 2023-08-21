---
title: "حل سوال 104 لیت‌کد"
slug: "leetcode-104-solution"
date: 2023-07-13T14:00:00+03:30
lastmod: 2023-07-13T14:00:00+03:30
tags: ["leetcode", "لیتکد", "حل سوال 104 لیت‌کد", "maximum depth of binary tree"]
author: "علی ثابت"
draft: false
comments: true
description: "در این پست سوال 104 لیت‌کد (maximum depth of binary tree) رو حل می‌کنیم"
---
برای دسترسی به سوال 104 لیت‌کد میتونید از این [لینک](https://leetcode.com/problems/maximum-depth-of-binary-tree/) استفاده کنید. سطح این سوال Easy است.

![leetcode 104](https://alirsabet.com/wp-content/uploads/2023/07/leetcode-104-300x300.jpg)

شرایط مسئله
-----------

در این مرحله، شرایط خاص مسئله و حالت‌های edge case رو بررسی می‌کنیم. این شرایط باید در توضیحات سوال یا مثال‌ها مشخص شده باشن یا اینکه از پاسخ‌های پیش فرض استفاده کنیم.

*   اگر درخت empty باشد، 0 را به عنوان جواب مسئله برمی‌گردانیم.
*   اگر درخت فقط شامل ریشه (root) باشد، 1 را به عنوان جواب مسئله برمی‌گردانیم.
*   اگر چند عدد به عنوان maximum depth وجود داشته باشند، یکی از اونها رو برمی‌گردانیم، چون در این سوال، خودِ مسیر مهم نیست.

راه حل منطقی
------------

در این مرحله به دنبال working solution هستیم، یعنی راه حلی منطقی که بتونه مسئله رو حل کنه. به راه حل بهینه فکر نمی‌کنیم. درگیر زبان برنامه نویسی و محدودیت‌های اون هم نخواهیم بود. منظور از maximum depth طبق گفته‌ی سوال، تعداد nodeهایی است که در طولانی‌ترین مسیر از ریشه (root) تا دورترین برگ (leaf) وجود دارند. مثلا در شکل زیر، جواب مسئله 5 خواهد بود. یک مورد مهم که باید دقت کنیم، اینه که در این سوال، به مقادیرِ درون nodeها کاری نداریم، فقط طول مسیر برامون مهمه.

![BT](https://alirsabet.com/wp-content/uploads/2023/07/BT-300x171.jpg)

در سوالاتی که به کمک درخت دودویی (Binary Tree) حل می‌شوند، معمولا پنج ابزار اصلی داریم که باید برای حل سوال ازشون استفاده کنیم. دو نوع جستجو به نام‌های جستجوی سطح اول (BFS) و جستجوی عمق اول (DFS) و سه نوع پیمایش به نام‌های پیمایش پیشوندی (Pre-Order)، پیمایش میانوندی (In-Order) و پیمایش پسوندی (Post- order).

آیا لازمه که پیمایش انجام بدیم؟ در 99 درصد موارد بله، بعضی وقت‌ها هم نه. در این سوال لازمه که پیمایش کنیم، چون قراره طول طولانی‌ترین مسیر رو پیدا کنیم و طبیعتا باید اون رو بپیماییم که بتونیم پیداش کنیم. چطور در درخت جستجو انجام بدیم؟ با BFS یا DFS؟

![Sample Binary Tree](https://alirsabet.com/wp-content/uploads/2023/07/Sample-Binary-Tree.png)

طبق BFS، در پیمایش، nodeهای نزدیک برامون اهمیت دارن. مثلا بعد از دیدنِ ریشه، بچه‌هاش رو می‌بینیم. بعدش، بچه‌های بچه‌هاش رو می‌بینیم و همینطور ادامه می‌دیم. یعنی سطح به سطح جلو می‌ریم. مثلا در شکل بالا، اول 2، بعد بچه‌هاش که 7 و 5 هستن، بعد بچه‌های 7 و 5 که 2 و 6 و 9 هستن و همینطور ادامه‌ی ماجرا. اما این چیزی هست که ما میخواهیم؟ نه، طبق صورت سوال، ما دنبال طول طولانی‌ترین مسیر هستیم، یعنی از ریشه تا دورترین برگ. چیزی که در BFS وجود داره اینه که تمرکزش رو روی nodeهای نزدیک، یعنی بچه‌ها گذاشته.

طبق DFS، در پیمایش، یک node رو می‌گیریم و همون رو تا انتها می‌ریم! یعنی می‌ریم سراغ بچه‌اش، بعد بچه‌ی بچه‌اش، بعد بچه‌ی بچه‌ی بچه‌اش و همینطور ادامه‌ی ماجرا. این همون چیزیه که در این سوال بهش نیاز داریم. به مقادیر درون nodeها کاری نداریم، پس در مورد سه نوع پیمایش Pre-Order و In-Order و Post-order صحبتی نمی‌کنیم.

DFS یک رویکرد بازگشتیه، وقتی از بازگشتی حرف می‌زنیم باید دقیقا بدونیم چطور کار می‌کنه (البته میشه DFS رو به شکل iterative هم نوشت، اما پیچیده‌ست). یک تابع بازگشتی، بارها خودش رو صدا می‌زنه تا به شرط پایان برسه، مقدار رو در حالت base case برگردونه و مسیرِ طی شده رو برگرده تا مقدار موردنظر رو حساب کنه.

هر تابع، سه مولفه اصلی داره، ورودی، بدنه و خروجی. ورودی تابع بازگشتی‌ای که ازش صحبت می‌کنیم چیه؟ یک node (و نه بیشتر) و یک عدد count.

به counter‌ای نیاز داریم که تعداد nodeهایی که تا الان دیده‌ایم رو نگه داره. در حالت ابتدایی مقدارش 0 است. وقتی وارد درخت می‌شیم و اولین node که ریشه است رو می‌بینیم، مقدارش به 1 تغییر می‌کنه. سراغ یکی از بچه‌های ریشه می‌ریم و دوباره همین کاری که انجام دادیم رو تکرار می‌کنیم. یعنی counter رو یک واحد بالا می‌بریم و می‌ریم سراغ یکی از بچه‌هاش. وقتی روی هر node هستیم، باید بدونیم تا اینجا که رسیده‌ایم، چندتا node دیده‌ایم، ورودی count که در بالا بهش اشاره شده، این مقدار رو نگه می‌داره.

حالت base case در DFS چیه؟ جایی که صدازدن‌های بازگشتی تموم شده. جوابی که در این حالت برمی‌گرده ممکنه درست یا غلط باشه. منظور از درست یا غلط اینه که ممکنه جواب نهایی (که طول طولانی‌ترین مسیره) در همین تلاش مشخص بشه یا در تلاش‌های بعدی، مهم اینه که الان نمی‌دونیم. هدف چیه؟ برسیم به برگ‌ها. پس شرط پایان الگوریتم هم باید رسیدن به برگ‌ها باشه. جایی که دیگه بچه‌ای وجود نداره.

وقتی در یک node هستیم، طولانی‌ترین مسیری که از اونجا تا انتها وجود داره چقدره؟ کلا دو مسیر برامون وجود داره که جلو بریم، یا راست یا چپ. طول طولانی‌ترین مسیر هم برابر ماکزیممِ یکی از همین دو مسیر خواهد بود.

تبدیل راه حل به کد
------------------

![lletcode 104 solution](https://alirsabet.com/wp-content/uploads/2023/07/lletcode-104-solution-300x119.png)

پیچیدگی زمانی و حافظه‌ای
------------------------

در این مرحله به بررسی پیچیدگی زمانی و حافظه ای راه حل می‌پردازیم. یعنی تحلیل می‌کنیم که بین زمان اجرای الگوریتم و حافظه مصرفی آن، چه رابطه ای با اندازه ورودی الگوریتم وجود دارد.

پیچیدگی زمانی الگوریتم O(n) است، n تعداد nodeهای درون درخت دودویی است و نیازه که همه‌ی nodeها رو بررسی کنیم.

پیچیدگی حافظه‌ای الگوریتم O(h) است که h، ارتفاع درخت دودویی است.

بدترین حالت زمانی رخ میده که درخت به شکل skewed باشه. در این حالت پیچیدگی حافظه‌ای به O(n) میرسه.

![skewed](https://alirsabet.com/wp-content/uploads/2023/07/skewed-300x162.png)

در یک درخت دودویی متوارن، پیچیدگی حافظه‌ای O(log n) است.

![balanced binary tree](https://alirsabet.com/wp-content/uploads/2023/07/binary-tree-300x170.jpg)