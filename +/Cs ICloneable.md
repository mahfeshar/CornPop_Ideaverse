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
- بس أي Object تاني لازم أورث منه وأمضي على الـ Contract بتاع الـ Interface الأول وبعدين أس