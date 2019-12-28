# PersianDateModelBinder
PersianDateModelBinder for validate date time shamsi

سفارشی سازی model binder پیش فرض ASP.NET MVC

در همین مثال فرض کنید تاریخ را به صورت شمسی از کاربر دریافت می‌کنیم. خاصیت تعریف شده هم DateTime میلادی است. به عبارتی model binder حین تبدیل رشته تاریخ شمسی دریافتی به تاریخ میلادی با شکست مواجه شده و نهایتا خاصیت this.ModelState.IsValid مقدارش false خواهد بود. برای حل این مشکل چکار باید کرد؟
برای این منظور باید نحوه پردازش یک نوع خاص را سفارشی کرد. ابتدا با پیاده سازی اینترفیس IModelBinder شروع می‌کنیم. توسط bindingContext.ValueProvider می‌توان به مقداری که کاربر وارد کرده در میانه راه دسترسی یافت. آن‌را تبدیل کرده و نمونه صحیح را بازگشت داد.
نمونه‌ای از این پیاده سازی را در ادامه ملاحظه می‌کنید:
 
 
سپس برای معرفی PersianDateModelBinder جدید تنها کافی است سطر زیر را
```c#
ModelBinders.Binders.Add(typeof(DateTime), new PersianDateModelBinder());
```
به متد Application_Start قرار گرفته در فایل Global.asax.cs برنامه اضافه کرد. از این پس کاربران می‌توانند تاریخ‌ها را در برنامه شمسی وارد کنند و model binder بدون مشکل خواهد توانست اطلاعات ورودی را به معادل DateTime میلادی آن تبدیل کند و استفاده نماید.
تعریف مدل بایندر سفارشی در فایل Global.asax.cs آن‌را به صورت سراسری در تمام مدل‌ها و اکشن‌متدها فعال خواهد کرد. اگر نیاز بود تنها یک اکشن متد خاص از این مدل بایندر سفارشی استفاده کند می‌توان به روش زیر عمل کرد:
```c#
public ActionResult Create([ModelBinder(typeof(PersianDateModelBinder))] User user)
```
همچنین ویژگی ModelBinder را به یک کلاس هم می‌توان اعمال کرد:
```c#
[ModelBinder(typeof(PersianDateModelBinder))]
public class User
{
}
```
