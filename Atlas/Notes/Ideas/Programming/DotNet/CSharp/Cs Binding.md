---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-06
---
![[Pasted image 20241006105225.png]]
```cs
TypeA T1 = new TypeA();
TypeB T2 = new TypeB();
// Not Binding: Reference from Parent --> object from Parent
```

- إني أعمل Reference يشاور على Child للـ class اللي بعمل منه Reference
- بمعنى إني أقدر بالـ Reference للـ Class أشاور على نفس الـ Class أو Child له
```cs
// Parent      Child
TypeA T1 = new TypeB(1, 2);
// Reference from Parent --> Object from Child
```
- مش بيشوف غير الجزء اللي الإبن **وارثه من الأب** بس غير كدا مبيشوفش
- هو عبارة عن [[Cs Value and Reference Types#Reference Types|Reference Type]]
	- الـ Reference اللي هو العنوان هيروح في الـ Stack والـ  Object نفسه أو القيمة في الـ Heap
```cs
TypeA T1 = new TypeB();
// Reference   Object
// Address     Value
// Stack       Heap
```
## Override
- عرفنا ان فيه طريقتين للـ Override هنا [[Cs Polymorphism#Overriding|Override]] 
الـ **Static Binding** (Early Binding): 
- لو عملت override عن طريق new هينفذ أول Function عندي بتاع الـ Parent مش هيشوف الـ Override الجديدة وهيعتبر دي Function جديدة بينفرد بيها الـ Child
- Compiler will bind function call based on **Reference Type**  NOT Object Type at **compilation Time**
الـ **Dynamic Binding**: 
- إنما لو بكلمة override هينفذ اللي انت عملته فالأخر وهينفذها (بتاع الإبن)
- CLR will Bind Function Call based on **Object Type** NOT Reference Type at **Run Time**
## Not Binding
مثال:
- لو عندي كلب أقدر أقول عليه إنه حيوان 
- بس مش كل حيوان هقدر أقول عليه انه كلب
- عشان كدا كنا بنستخدم [[Cs Type Casting]] في الحالة اللي زي دي

```cs
// Dog = Animal // مقدرش
// Dog = (Dog) Animal // الحيوان دا بوعدك انه كلب

object O1 = 3;

// int x = O1; // ERROR
// Cause
// O1 = "Ahmed"; // Object can be anything
int x = (int) O1; // بوعدك هيبقا انتجر
// (int): build in casting operator

TypeA T1;
T1 = new TypeA(1);
T1 = new TypeB(1, 2); // Child -> Binding

TypeB = T2;
T2 = new TypeA(); // ERROR
T2 = T1; // ERROR
T2 = (TypeB) T1; 
// بوعدك انه هيبقا الإبن دا بالذات لأن هو عنده أبناء كتير
// This is NOT Binding

// (TypeB): We need to make this casting operator
```

الموضوع دا مرتبط بالـ [[Cs Casting Operator]] شوية لأن لازم أعمل Casting Operator للإبن لما بخليه ياخد Object أب لأن فيه حاجة زيادة بتبقا موجودة 
مثال: الأب عنده A والإبن ورثه منه وكمان زود B 
أنا دلوقتي هعمل ابن من Object أب بس الإبن المفروض يعرف الحاجة الزيادة بتاعته هتبقا بإيه 

## Example
### Example 1
```cs
internal class Employee
{
	public int id { get; set; }
	public string name { get; set; }

	public void MyFunc01()
	{
		Console.WriteLine("I am Employee");
	}

	public virtual void MyFunc02()
	{
		Console.WriteLine($"ID: {id}, Name: {name}");
	}
}

class FullTimeEmployee : Employee
{
	public int salary { get; set; }
	public new void MyFunc01()
	{
		Console.WriteLine("I am FullTime Employee");
	}
	public override void MyFunc02()
	{
		Console.WriteLine($"ID: {id}, Name: {name}, Salary: {salary}");
	}
}
class PartTimeEmployee : Employee
{
	public int HoursOfWork { get; set; }
	public new void MyFunc01()
	{
		Console.WriteLine("I am PartTime Employee");
	}
	public override void MyFunc02()
	{
		Console.WriteLine($"ID: {id}, Name: {name}, HoursOfWork: {HoursOfWork}");
	}
}

// We will try to make function for them
public void ProcessEmployee(FullTimeEmployee emp)
{
	emp.MyFunc01();
	emp.MyFunc02();
}
public void ProcessEmployee(PartTimeEmployee emp)
{
	emp.MyFunc01();
	emp.MyFunc02();
}
// دا مش اوفرلودينج دا عك، لأن الإتنين نفس البودي
// The solution here is BINDING
public void ProcessEmployee(Employee emp)
{
    emp.MyFunc01();
    emp.MyFunc02();
}
```
### Example 2
- خد بالك من انه هينفذ آخر Override كان موجود لو استخدمت الـ Static Binding
```cs
class TypeA
{
    public int A { get; set; }

    public TypeA(int _A=0) { A = _A; }

    public void StaticallyBindedShow ()
    {
        Console.WriteLine("I am Base");
    }
    ///Dynamically Binded
    internal virtual void DynShow () ///non Private Virtual Method
    {
        Console.WriteLine($"Base {A}");
    }
}

class TypeB:TypeA
{
    public int B { get; set; }
    public TypeB(int _A =0 , int _B=0):base(_A)
    {
        B = _B;
    }

    internal override void DynShow()
    {
        Console.WriteLine($"Derived {A} {B}");
    }

    public new void StaticallyBindedShow() { 
		    Console.WriteLine("I am Derived"); 
		}
}

class TypeC : TypeB
{
    public int C { get; set; }

    public TypeC(int _a=0 , int _b=0 , int _c=0):base(_a , _b)
    {
        C = _c;
    }

    internal override void DynShow()
    {
        Console.WriteLine($"Type C {A} {B} {C}");
    }
}

class TypeD : TypeC
{
    //internal new void DynShow() 
    /// new statically binded impelementation
    
    /// new dynamically binded impelementation
    internal new virtual void DynShow() 
    {
        Console.WriteLine("Type D");
    }
}
class TypeE: TypeD
{
    ///override on TypeD Implementation
    internal override void DynShow()
    {
        Console.WriteLine("Type E");
    }
}

class program
{
		static void Main(string[] args)
		{
		  TypeA BaseRef = new TypeA(1);
          BaseRef.StaticallyBindedShow(); ///Base
          BaseRef.DynShow(); ///Base

          TypeB DerivedRef = new TypeB(2, 3);
          DerivedRef.StaticallyBindedShow(); ///Derived
          DerivedRef.DynShow(); ///Derived

          BaseRef = new TypeB(4, 5);
          ///Ref to Base = Derived Object
          //BaseRef.A = 6;
          BaseRef.StaticallyBindedShow();///Base
          ///Statically Binded methods (non virtual) 
          //Compiler Bind Call based in Refrence Type not Object Type
          BaseRef.DynShow();///Derived
          ///Dynamically Binded Method , CLR will bind Function 
          //Call based on Object Type in Runtime  


          BaseRef = new TypeC(6, 7, 8);
          DerivedRef = new TypeC(9, 10, 11);

          BaseRef.DynShow(); ///TypeC
          DerivedRef.DynShow(); ///TypeC


          BaseRef = new TypeD();
          BaseRef.DynShow(); ///TypeC


          TypeD RefD = new TypeD();
          RefD.DynShow(); ///TypeD
		}
}
```