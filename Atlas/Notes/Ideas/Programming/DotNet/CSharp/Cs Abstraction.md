---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-10
---
- اتكلمنا عنها قبل كدا في [[Abstraction]]
- كلمة abstract هنا معناها إن الحاجة ناقصة سواء [[Cs Class]] أو [[Cs Function]] أو [[Cs Properties]]
```cs
abstract class Shape
{
    public decimal Dim01 { get; set; }
    public decimal Dim02 { get; set; }
    // public decimal CalculateArea() { } 
// I can't make like that because I don't know what is the shape
	public abstract decimal CalculateArea();
}

// MAIN
// Shape sh1 = new Shape(); 
// Cannot create object (instance) - not fully implemented
// But we can create reference
Shape sh1;
```
- معرفتش هعمل إيه في الـ method اللي اسمها Area لأني معرفش هستخدم أي قانون فبقا ناقص عندي فبالتالي هستخدم كلمة abstract عشان أقول إنها ناقصة implemented
## Abstract Class
- وبما إن الـ Class فيها حاجة مش كاملة وهي الـ Method فبالتالي الـ Class نفسه مش كامل وبالتالي لازم أستخدمله كلمة Abstract
  ممكن يبقا الـ Class abstracted برضو وفيه كل حاجة كاملة عادي بس أنا عايز محدش يقدر يوصله 
- مينفعش تعمل object من الـ Abstract class لأنه Not fully implemented (ناقص) ^0960ec
- ممكن يبقا الـ Abstract class **عبارة عن Container code** لحاجات هتيجي في المستقبل أو بيبقا حاجة Standard لحاجة هتيجي بعد كدا (not fully implemented)
  مثال: لو عندي نوعين Employee واحد Partial, Fully فالـ Employee الأب مش هحتاج أشوفه ^fafd73
```cs
//class created to be base class for childs
// can't intialize object from abstract class
abstract class Person
{
    public string FName { get; set; }
    public string LName { get; set; }

    public Person(string _FName , string _LName)
    {
        FName = _FName;
        LName = _LName;
    }

    public override string ToString()
    {
        return $"{FName} {LName}";
    }
}

//valid
Person P;

//not Valid
//Person P1 = new Person("Ahmed", "Ali");  
```
## Example
```cs
abstract class GeoShape
{
    public int Dim1 { get; set; }
    public int Dim2 { get; set; }

    public GeoShape(int D1 , int D2) { Dim1 = D1; Dim2 = D2; }

    //public virtual Double Area () =0; //C++

    public abstract Double Area(); 
    ///Abstract Method = Virtual + No Impelementation

    public abstract double Perimeter { get; /*set;*/ } 
    ///Abstract ReadOnly Property

}

// Care, it's abstract class because 
// it's inherits abstract property so it's not fully implemented
// We can make it abstract or we can implement the property
abstract class RectBase : GeoShape //: -> inherits + implements
{
    public RectBase(int W=0, int H=0) : base(W, H) { }

	// We will use override to implement abstract method
	// Or we can use it for override virtual method
    public override double Area() 
    {
        return Dim1 * Dim2;
    }
}

class Rect : RectBase
{
    public override double Perimeter { get { return 2 * (Dim1 + Dim2); } }
}

class Square : RectBase
{
    ///Must
    // because perimeter didn't implemented in rectbase
    public override double Perimeter => 4 * Dim2;
    ///Optional
    // because Area implemented in rectbase
    public override double Area()
    {
        throw new NotImplementedException();
    }
}
```

## Abstract Class vs Interface
### Interface
![[Cs Interface#^e9bd02]]
![[Cs Access Modifiers#Inside Cs Interface Interface]]

### Abstract Class
![[Cs Abstraction#^fafd73]]
![[Cs Access Modifiers#Inside Cs Class Class or Cs Struct Struct]]
متاح أيضًا كمان حاجتين:
1. Abstract method
2. Abstract property
