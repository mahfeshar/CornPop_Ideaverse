---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---
- هنعمل Utility class: بيبقا فيها حاجات مثلًا هتساعدني في الشغل
- معنى Static: إني هقدر أنادي عليها من خلال الـ Class نفسه مش لازم أعمل Object منه
```cs
class Utility
{
    public int X { get; set; }
    public int Y { get; set; }

    public Utility(int _X , int _Y)
    {
        X = _X;
        Y = _Y;
        //pi = 3.14; 
        ///Object Ctor is not a right place for Initializing Static Members
        Console.WriteLine("Ctor");
    }

    ///Static Ctor
    ///will be executed only Once per class lifetime (Program)
    ///can't specify return Datatype , Access modifier or Input -- 
    //Paramters for static Ctor
    ///cctor : static Ctor in il
    ///Max only one static ctor per class
    static Utility()
    {
        Console.WriteLine("Static Ctor");
        pi = 3.14;
    }

    public static double Cm2Inch (double Cm)
    {
        return Cm / 2.54;
    }

    public static double Inch2Cm (double Inch)
    {
        return Inch * 2.54;
    }

    static double pi;
    ///Static Attributes Allocate in Heap defore First usage 
    //to Class till end of program (or unreachable in case of reference Types)
    ///Static members initialized to default values by Default

    public static double PI { get { return pi; } }


    public static double CircleArea(double R)
    {
        return pi * R * R;
    }

}
```