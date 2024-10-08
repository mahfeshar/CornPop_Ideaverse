---
up:
  - "[[Cs Interface]]"
related: 
created: 2024-10-07
---
```cs
class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Salary { get; set; }
}
static void Main(string[] args)
{
    Employee emp01 = new Employee 
    { Id = 1, Name = "John", Salary = 1_000};
    Employee emp02 = new Employee 
    { Id = 2, Name = "Jane", Salary = 2_000};
    Console.WriteLine(emp01.GetHashCode()); // 43942917
    Console.WriteLine(emp02.GetHashCode()); // 59941933
    
    Console.WriteLine("==========");

    emp02 = emp01; // Shallow copy
    Console.WriteLine(emp01.GetHashCode()); // 43942917
    Console.WriteLine(emp02.GetHashCode()); // 43942917

    Console.WriteLine("==========");

    // emp01 = emp02.Clone(); 
    // We don't have here we need to use ICloneable
}
```

- مفيش حاجة اسمها clone غير في الـ [[Cs Arrays#Array Clone|Array clone]] ودي بتستخدم الـ Interface اللي اسمه ICloneable
- بس أي Object تاني لازم أورث منه وأمضي على الـ Contract بتاع الـ Interface الأول وبعدين أعمل Implement بقا للـ Clone دي تعمل ايه بالظبط
- بنستخدم الطرق دي عشان نعمل [[Cs Shallow and deep copy#Deep Copy|Deep Copy]]

```cs
    public abstract partial class Array : ICloneable, IList, IStructuralComparable, IStructuralEquatable


//
// Summary:
//     Supports cloning, which creates a new instance of a class with the same value
//     as an existing instance.
public interface ICloneable
{
    //
    // Summary:
    //     Creates a new object that is a copy of the current instance.
    //
    // Returns:
    //     A new object that is a copy of this instance.
    object Clone();
}
```
- الـ Interface جواه Method واحدة اللي هي الـ Clone
- بيحقق مبدأ الـ [[Single Responsibility Principle]] انك مش هتلاقي غير method واحدة أو ممكن يبقا فيها أكتر من method بس مرتبطين ببعض

```cs
class Employee : ICloneable
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Salary { get; set; }
    public object Clone()
    {
        return new Employee()
        {
            Id = this.Id,
            Name = this.Name,
            Salary = this.Salary
        };
    }
}

// Main
emp01 = (Employee) emp02.Clone(); // Deep Copy

Console.WriteLine("Employee 1");
Console.WriteLine(emp01.GetHashCode()); // 2606490
Console.WriteLine($"{emp01.Id}, {emp01.Name}, {emp01.Salary:c}"); // 1, John, $1,000.00

Console.WriteLine("Employee 2");
Console.WriteLine(emp02.GetHashCode()); // 43942917
Console.WriteLine($"{emp02.Id}, {emp02.Name}, {emp02.Salary:c}"); // 1, John, $1,000.00
```

---
We can also use [[Cs Constructor#Copy Constructor|Copy constructor]]
Or we can use copy with Clone

```cs
public object Clone()
{
	return new Employee(this);
}
```