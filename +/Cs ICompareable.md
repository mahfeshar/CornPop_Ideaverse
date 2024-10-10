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

```