---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---
- لو عندي في الـ [[Cs Inheritance]]، بيبقا فيه أب وإبن وممكن يبقا فيه حفيد كمان
- الـ Sealed دا آخر واحد ومينفعش بعده حاجة تورث منه
```cs
class Parent
{
    public virtual void Print() 
        => Console.WriteLine("Hello Parent");
}
class Child : Parent
{
    public sealed override void Print()
        => Console.WriteLine("Hello Child");
}
sealed class GrandChild : Child
{
    public override void Print()
        => Console.WriteLine("Hello Child"); 
    // ERROR: We cannot override or inherite sealed
}
class AnotherOne : GrandChild // ERROR: مقدرش أورث منه
{

}
```