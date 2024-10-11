- اتكلمنا قبل كدا عن الـ [[Cs Type Casting]] وقولنا نبذه عنه برضو في الـ [[Cs Binding#Not Binding]]

الـ Model الأصلي دا ممكن نسميه Poco class
## Manual Mapping
احنا اتكلمنا عن الـ [[Code-first or Database-First#Code-First|code-first]]
- بنبني أول حاجة الـ class بتاعي عادي
- دا الـ Model وهنا الـ Class بيمثل Table في الـ Database
```cs
// Model : is the Class that represents the table in the database
class User
{
    public int Id { get; set; }
    public string FullName { get; set; }
    public string Email { get; set; }
    public string Password { get; set; }
    public string SecurityStamp { get; set; }
}
```
يعني احنا دلوقتي بنتكلم عن شكل الـ Data في **الـ Database**
بس مش دا اللي بيظهر للـ Users بتاع الموقع
فعشان كدا لازم بنعمل Class تاني وبيبقا اسمه الـ View
```cs
class UserViewModel
{
    public int Id { get; set; }
    public string Fname { get; set; }
    public string Lname { get; set; }
    public string Email { get; set; }
}
```
دلوقتي هيظهر مشكلة إني المفروض هاخد من الـ Database الـ Object من النوع User
```cs
// MAIN

```
