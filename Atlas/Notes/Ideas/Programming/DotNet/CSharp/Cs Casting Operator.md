---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---

- اتكلمنا قبل كدا عن الـ [[Cs Type Casting]] وقولنا نبذه عنه برضو في الـ [[Cs Binding#Not Binding]]


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
- يعني احنا دلوقتي بنتكلم عن شكل الـ Data في **الـ Database**
- بس مش دا اللي بيظهر للـ Users بتاع الموقع
- فعشان كدا لازم بنعمل Class تاني وبيبقا اسمه الـ View Model
```cs
class UserViewModel
{
    public int Id { get; set; }
    public string Fname { get; set; }
    public string Lname { get; set; }
    public string Email { get; set; }
}
```
- دلوقتي هيظهر مشكلة إني المفروض هاخد من الـ Database الـ Object من النوع User
- وعشان أظهرها وأحولها انها تظهر للـ HTML لازم أحولها للـ Class اللي هيرجع نفسه اللي هو الـ View Model
- بس مينفعش أخلي reference من Class يشاور على Object لـ Class تاني من غير ما أعمل Casting
	- وزي ما عرفنا عندنا نوعين من الـ Casting اللي هما الـ Implicit والـ Explicit 
- بس في الحالة دي لازم لو حاجة مش معمولة Built-in اني أعملها بإيدي
```cs
// MAIN
User user1 = new User()
{
    Id = 1,
    FullName = "Pop Corn",
    Password = "Password",
    Email = "pop.corn@me.com",
    SecurityStamp = Guid.NewGuid().ToString()
};
// UserViewModel userViewModel = user1; // ERROR
// We should do Casting (Mapping)
UserViewModel userViewModel = (UserViewModel)user1;
// It's also will give me ERROR, we should implement it
```
- عشان نعمل Explicit operator بروح للـ class التاني اللي هو الـ view
- الـ Model الأصلي دا ممكن نسميه Poco class
```cs
public static explicit operator UserViewModel(User user)
{
    string[] names = user.FullName.Split(' ');
    return new UserViewModel()
    {
        Id = user.Id,
        Fname = names[0],
        Lname = names[1],
        Email = user.Email
    };
}
```
