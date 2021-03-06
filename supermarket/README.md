<div dir="rtl">

# سوپرمارکت
در این سوال می‌خواهیم یک برنامه برای مدیریت سوپرمارکت بنویسیم که به مغازه‌دار در مدیریت مغازه و اجناس و سفارشات کمک کند. جزئیات مورد نیاز در ادامه می‌آید:

 صاحب مغازه می‌خواهد بتواند اجناس خود را در برنامه ثبت کند. هر جنس دارای موارد زیر است:
- نام کالا
- نوع (کیلویی / تعداد)
- قیمت خرید
- قیمت فروش
- موجودی (وزن / تعداد)

همچنین هرروز تعدادی مشتری به مغازه مراجعه می‌کنند و کالاهای مورد نیاز خود را سفارش می‌دهند. هر سفارش دارای موارد زیر می‌باشد:
- نام مشتری
- تاریخ سفارش
- لیست کالاها و تعداد هر کالا
- وضعیت سفارش (درحال پردازش، دریافت شده، به پایان رسیده)
- زمان ثبت سفارش
- نحوهٔ پرداخت (نقدی، کارت)

صاحب مغازه می‌خواهد برنامه‌ای که شما می‌نویسید قابلیت‌های زیر را داشته باشد:
1. هرزمان که خواست با وارد کردن یک دستور مجموع کل فروش را ببیند.
2. همچنین مجموع کل سودی که تاکنون داشته باید قابل محاسبه باشد.
3. مغازه دار باید لیست کل کالا‌های موجود را به همراه میزان موجودی آن ببیند.
4. همچنین او میخواهد که هر زمان که خواست با وارد کردن یک دستور لیست تمامی کالاهایی که قبلا موجود بودند و به اتمام رسیده اند را نمایش دهید. که نسبت به خرید آنها اقدام کند.
5. با وارد کردن نام یک مشتری تعداد سفارشات او و همچنین مجموع فروشی که داشته را نمایش دهد.
6. بتواند لیست ۵ کالای سودده مغازه را ببیند
   1. لیست ۵ کالا برحسب سودی که هر کالا تا کنون داشته از زیاد به کم مرتب شده باشد.
   2. درصورتی که مغازه کمتر از ۵ کالا داشت همان کالا‌ها را نمایش دهد.

در این مرحله بیشتر به دنبال پیاده سازی منطق فروشگاه هستیم و می‌خواهیم ورودی و خروجی و ارتباط برنامه با کاربر در کنسول باشد. اما **باید فروشگاه را طوری پیاده سازی کنید که بعدا امکان تغییر رابط کاربری آن وجود داشته باشد.** بدین منظور پیشنهاد می‌شود که از **معماری MVC** استفاده کنید. معماری MVC یک **الگوی طراحی** است که برای آشنایی بیشتر با آن می‌توانید [صفحهٔ Wikipedia آن](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) را ببینید.

دستوراتی که باید پیاده سازی کنید در این قسمت مشخص شده است:

### خروج:
برای خروج باید کاربر دستور زیر را وارد کند:
</div>

```
exit
```
<div dir="rtl">

تا زمانی که این دستور وارد نشده، شما باید یک دستور از کاربر بگیرید و آن را اجرا کنید. اگر دستور وارد شده نامعتبر بود (مطابق هیچ یک از الگو‌های داده شده نبود) عبارت `Invalid command` را در یک خط چاپ کنید.


### افزودن کالا:
برای افزودن کالا کاربر باید دستور زیر را وارد کند:
</div>

```
add [countable|uncountable] good [good name]
```
<div dir="rtl">
مانند:
</div>

```
add uncountable good sugar
```

<div dir="rtl">
سپس شما باید میزان موجودی را بپرسید. اگر کالا از نوع countable بود چاپ کنید:
</div>

```
Enter count:
```

<div dir="rtl">
و اگر از نوع uncountable بود چاپ کنید:
</div>

```
Enter amount:
```
<div dir="rtl">

سپس برای کالای قابل شمارش (بسته‌ای) باید از مغازه دار یک عدد صحیح و برای کالای غیرقابل شمارش (کیلویی) از مغازه دار یک عدد `double` بگیرید که بیانگیر وزن کالا (برحسب کیلوگرم) می‌باشد.
اگر عدد وارد شده نامعتبر بود دوباره عبارت `enter  amount‍` یا `enter count` را چاپ کنید و از کاربر ورودی بگیرید.

سپس باید قیمت کالا را از کاربر بگیرید. بدین منظور در یک خط عبارت
</div>

```
Enter sell and buy price:
```
<div dir="rtl">
 را چاپ کنید.
سپس کاربر در یک خط دو عدد صحیح را با فاصله وارد می‌کند که به ترتیب بیانگر قیمت فروش و قیمت خرید کالا است.
اگر ورودی نامعتبر بود دوباره این عبارت را چاپ کنید و از کاربر ورودی بگیرید.

سپس باید موجودی کالای مورد نظر را به میزان داده شده افزایش دهید. اگر کالا از قبل موجود بود، مقدار آن را افزایش دهید و اگر موجود نبود آن را ایجاد کنید. همچنین اگر کالا موجود بود باید قیمت خرید و فروش آن به قیمت جدید تغییر کنند.

دقت کنید که ممکن است یک کالا هم به صورت بسته‌بندی (بسته‌ای) و هم به صورت باز (کیلویی) موجود باشد. مثلا شکر هم بسته‌ای و هم کیلویی داشته باشیم که نباید اشتباه شوند.

سپس باید خروجی به صورت زیر چاپ شود:

</div>

```
Uncountable good [good name] added. Total inventory: [amount] kg
Countable good [good name] added. Total inventory: [count] item
```
<div dir="rtl">
 مثال:
</div>

```
Uncountable good rice added. total inventory: 100 kg
Countable good chips added. total inventory: 40 item
```

<div dir="rtl">

### ثبت سفارش:
با وارد شدن دستور زیر باید یک سفارش جدید ایجاد کنید:
</div>

```
new order from [consumer name]
```

<div dir="rtl">

که به جای `[consumer name]` نام مشتری وارد می‌شود.

سپس باید `Enter item:` را چاپ کنید و منتظر بمانید تا کاربر عبارت `end order` را وارد کند. قبل از وارد کردن این عبارت کاربر کالاهای مورد نیاز خود را در فرمت زیر وارد می‌کند:

</div>

```
[count] item, [good name]
[amount] kg, [good name]
```

<div dir="rtl">

اگر پاسخ داده شده در فرمت بالا نبود عبارت زیر را چاپ کنید:

</div>

```
Invalid input format. currect format is: "1 item, juice" or "1.2 kg, corn"
```

<div dir="rtl">

مثال:

</div>

```
2 item, milk
1.5 kg, wheat
```

<div dir="rtl">

برای کالا‌های بسته‌ای به صورت اول و برای کالا‌های کیلویی به صورت خط دوم وارد می‌شوند.
حال شما باید عبارت داده شده را بررسی کنید. اگر کالا به همان میزانی که مشتری درخواست کرده موجود بود چاپ کنید

</div>

```
Item added. Total price: [total price]
```

<div dir="rtl">

به جای `[total price]` قیمت نهایی این item را چاپ کنید.

و آن کالا را به سفارش اضافه کنید. اگر کلا کالا موجود نبود چاپ کنید:

</div>

```
[good name] is unavailable
```

<div dir="rtl">

اما اگر کالا کمتر از میزانی که مشتری درخواست کرده موجود بود چاپ کنید:

</div>

```
Only [count] item of [good name] is available.
Only [amount] kg of [good name] is available.
```

<div dir="rtl">

خط اول برای کالاهای بسته‌ای و خط دوم برای کالا‌های کیلویی.

پس از وارد شدن دستور `end order` و پایان ثبت سفارش، شما باید هزینه تمام شدهٔ سفارش را چاپ کنید. هزینهٔ تمام شده، جمع هزیهٔ تک تک item های موجود در سفارش است. فرمت چاپ خروجی باید به صورت زیر باشد:

همچنین باید از کاربر بپرسید که به صورت نقدی میخواهد پرداخت کند یا کارت بکشد؟

</div>

```
Total price: 10000 IRR
Do you want to pay with cash or credit?
```

<div dir="rtl">

سپس باید کاربر یکی از عبارات `cash` یا `credit` را وارد کند. اگر پاسخ اشتباه بود، سوال خود را تکرار کنید تا پاسخ درست وارد شود.

پس از وارد شدن پاسخ درست عبارت `Tanks for your order` را چاپ کنید و کار به پایان می‌رسد.

### نمایش لیست کالاها:

مغازه دار می‌خواهد با مراجعه هر مشتری بتواند لیست کالا‌های موجود را به همراه میزان موجودی و قیمت به مشتری نشان دهد. برای این کار او دستور زیر را وارد می‌کند.

</div>

```
goods list
```

<div dir="rtl">

پس از وارد شدن این دستور باید شما لیست کالاهای موجود را در یک جدول مانند شکل زیر نمایش دهید:

</div>

```
+-----------------+------------+------------+
| Good name       | Inventory  | Price(IRR) |
+-----------------+------------+------------+
| milk            | 10 item    | 38000      |
| rice            | 86 kg      | 210000     |
| chips           | 15 item    | 30000      |
| egg             | 18 item    | 12000      |
| sugar           | 13 kg      | 80000      |
+-----------------+------------+------------+
```
<div dir="rtl">

برای فرمت چاپ سطرهای جدول می‌توانید از `System.out.format` و فرمت‌های زیر (برای کالاهای قابل شمارش و غیر قابل شمارش) استفاده کنید:

</div>


```
System.out.format("| %-15s | %-7.02f kg | %-10d |%n", name, amount, price);
System.out.format("| %-15s | %-5d item | %-10d |%n", name, count, price);
```

<div dir="rtl">

همچنین خطوط اول و آخر دقیقا به صورت زیر باشند:

</div>


```
+-----------------+------------+------------+
```

<div dir="rtl">

### محاسبهٔ فروش کل:
برای محاسبهٔ کل فروش، فروشنده دستور زیر را وارد می‌کند و شما باید در فرمت زیر پاسخ او را بدهید.
#### ورودی:
</div>

```
total sales [--cash][--credit]
```

<div dir="rtl">

#### خروجی:

درصورتی که عبارت `--credit` وارد شده باشد باید مجموع فروش از طریق کارتخوان را چاپ کنید و اگر عبارت `--cash` وارد شده باشد باید مجموع فروش نقدی را چاپ کنید. 
اگر هیچ کدام وارد نشده بود، مجموع کل فروش را چاپ کنید.
</div>

```
1200000 IRR
```

<div dir="rtl">

### محاسبهٔ سود کل:
همچنین درصورتی که مغازه دار دستور زیر را وارد کند باید میزان کل سود را در همان فرمت قبلی به او نمایش دهید.

در این دستور همواره کل سود نمایش داده می‌شود و تفاوتی بین پرداخت‌های نقدی و اعتباری وجود ندارد.
</div>

```
total profit
```

<div dir="rtl">

</div>

<div dir="rtl">

</div>

<div dir="rtl">

</div>

<div dir="rtl">

</div>

<div dir="rtl">

</div>

<div dir="rtl">

</div>