---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-24
---
- اتكلمنا قبل كدا عن الـ [[Inheritance]]
- في الـ CSharp معندناش غير **Single Inheritance** ومفيش حاجة اسمها Multiple يعني بيورث من أب واحد بس
```cs
class Parent
{
    public int X{ get; set; }
    public int Y{ get; set; }

    public Parent(int _X, int _Y)
    {
        X= _X;
        Y = _Y;
    }

    public override string ToString()
    {
        return $"X: {X}, Y: {Y}";
    }

    public int Product()
    {
        return X * Y;
    }
}

class Child : Parent // Child is a parent
{
    public int Z { get; set; }

    // Chaining from empty parameter in parent so we should add it to parent
    // Or we can also chain from another constructor in parent
    public Child(int _X, int _Y, int _Z): base(_X, _Y)
    {
        Z = _Z;
    }
}
```
- اتكلمنا عن [[Cs Constructor#Constructor Chaining|Chaining]] قبل كدا وهنا استخدمناها ان احنا عملنا Chain من الـ Constructor اللي فالكلاس الأب وهو كدا هيروح ينفذ الـ Ctor الأصلي الأول وبعدين يجيلك ينفذ اللي عندك
- لو معملتش كدا **لازم الأب يبقا فيها Empty Parameter Ctor**