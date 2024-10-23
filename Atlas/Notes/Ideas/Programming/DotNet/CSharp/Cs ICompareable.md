---
up:
  - "[[Cs Interface]]"
related: 
created: 2024-10-10
---
```cs
int[] numbers= {2, 5, 3, 10, 7, 6, 8, 9, 4, 1};
Array.Sort(numbers);
foreach (int num in numbers)
    Console.Write(num + ", ");
// 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```
دا بيحصل بسبب الـ Interface اللي اسمه `ICompareable` ودا مفيهوش غير function واحدة وهي الـ `CompareTo`
```cs
public interface IComparable 
{
	int CompareTo(object obj);
}
```

- ولو في الـ Class بتاعك انت مش واخد من الـ Interface دا هيجيبلك إيرور
- هي دي الـ Function اللي من خلالها بحدد هيعمل Sort على أي أساس

```cs
class Employee : IComparable
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Salary { get; set; }

    public int CompareTo(object? obj)
    {
        if (this.Salary > ((Employee)obj).Salary)
            return 1;
        else if (this.Salary < ((Employee)obj).Salary)
            return -1;
        else
            return 0;
    }
}

// MAIN
Employee[] employees =
{
    new Employee() {Id = 1, Name = "John", Salary = 10_000},
    new Employee() {Id = 2, Name = "Mary", Salary = 30_000},
    new Employee() {Id = 3, Name = "Peter", Salary = 20_000}
};
int result = employees[0].CompareTo(employees[1]);
Console.WriteLine($"Expected result = -1, actual result = {result}");

Console.WriteLine("==========");
Console.WriteLine("Before sort:");
foreach (Employee emp in employees)
    Console.WriteLine(emp.Name + " " + emp.Salary);

Array.Sort(employees);
Console.WriteLine("==========");
Console.WriteLine("After sort:");
foreach (Employee emp in employees)
    Console.WriteLine(emp.Name + " " + emp.Salary);
```

- ولازم نعمله (إجبار)، ونمضي على العقد (Contract)
## Generic ICompareable
لو شوفنا في اللي فوق هي بتاخد [[Cs System.Object]] ودا بيعمل مشاكل لما نيجي نعمل [[Cs Type Casting]]
فممكن كنا نحل المشكلة دي عن طريق [[Cs is]] ثم بعد كدا اخترعوا [[Cs as]]

---
بس برضو دا مش أحسن حل في وجود الـ [[Cs Generics]]
عملوا الـ interface انه ياخد T وتقدر تحط فيه أي حاجة فدا سهل الموضوع كتير

```cs
static class Helper <T> where T : IComparable<T>
{
    static public void Swap (ref T a, ref T b)
    {
        T temp = a;
        a = b;
        b = temp;
    }
    static public void BubbleSort(T[] x)
    {
        for (int i = 0; i < x?.Length; i++)
        {
            for (int j = 0; j < x?.Length - i - 1; j++)
            {
                if (x[j].CompareTo(x[j+1]) == 1)
                {
                    Swap(ref x[j], ref x[j+1]);
                }
            }
        }
    }
}
class Employee : IComparable<Employee>
{
    public int CompareTo(Employee? other)
    {
        if (other == null) return 1; 
        return this.Salary.CompareTo(other.Salary); 
        // int.CompareTo(int)
        // if (m_value < value) return -1;
		// if (m_value > value) return 1;
		// return 0;
    }

    public int Id { get; set; }
    public string Name { get; set; }
    public int Salary { get; set; }
}
```