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
// Not Binding: Reference from Parent --< object from Parent
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