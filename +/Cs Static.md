---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---
- معنى Static: إني هقدر أنادي عليها من خلال الـ Class نفسه مش لازم أعمل Object منه عشان أقدر أنادي عليها ودا بيحصل لو هي مش معتمدة على Object معين أو بتختلف بإختلافهم
## Instance vs Static
Instance method => Object Member method (Non static)
![[Cs Class#Instance members]]
![[Cs Class#Static Members]]
- كمان استخدمنا الـ Static في الـ [[Cs Operator Overloading]] وكمان الـ [[Cs Casting Operator]]
## Why static class
امتا اعمل method static لما يكون ناتج الـ method مش بيختلف بإختالف الـobject

![[Pasted image 20241011051605.png]]
**Static Class:** is a just Container For Static Members (Attribute, Property, Constructor, Method) and Constants
You Can't Create Object From This Class (Helper or utility Class) اصال طبيعي مش
No Inheritance for this Class مش هينفع لأنه مساعد ليا مش أكتر
**Static Constructor** (Maximum Only One Static Constructor Per Class)
Can't Specify Access Modifiers or Parameters for Static Constructor
Will be Executed Just Only One Time Per Class Lifetime Before the first Usage of Class
**Usages Of Class:**
1. Call Static Method or Static Property
2. Create Object From This Class
3. Create Object From Another Class Inheriting From This Class
## Example
- هنعمل Utility class: بيبقا فيها حاجات مثلًا هتساعدني في الشغل
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
    ///ctor : static Ctor in il
    ///Max only one static ctor per class
    ///We use it to initialize static attributes
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
    ///Static Attributes Allocate in Heap before First usage 
    //to Class till end of program (or unreachable in case of reference Types)
    ///Static members initialized to default values by Default


    ///Class Member Property : Static Property
    ///Static Property GET and SET One of These:
    ///1. Static Attribute
    ///2. Constant
    public static double PI { get { return pi; } }

	private const double pi = 3.14;

    public static double CircleArea(double R)
    {
        return pi * R * R;
    }
}
```