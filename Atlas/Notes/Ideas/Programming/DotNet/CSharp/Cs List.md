---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-15
---
- هي زي ال Array بس الفرق انها Dynamic size نفس فكرة ال [[Array#Dynamic Arrays|Dynamic Arrays]]
- هي عبارة عن [[Generic Type]] عشان كدا بنستخدم معاها `<new List <int`
	- لما تيجي تتعامل مع ال generic type لازم تحد ال generic parameter اللي بتبقا بينangle brackets `<>`
- تقدر تعمل list من أي  نوع زي ال char او string أو حتى أي non primitive types زي ال classes

## Syntax
```cs
var numbers = new List<int>();
var numbers = new List<int>() {1, 2, 3, 4};
```

## Methods
![[Pasted image 20240715110644.png]]
- `Add`: Add an object to the list
- `AddRange`: Add a list of objects that can be list or array
- `Remove`: To remove one object from the list
- `RemoveAt`: Remove the object at the given index 
- `IndexOf`: Returns the index of the given object.
- `Contains`: If the list contains the given object or not
- `Count`: Return the number of objects in the list

> [!globe] Tip
> - لما تيجي تحاول تستخدم ال `AddRange` هيقولك انه بياخد `IEnumerable`
> - لازم تعرف ان أي كلمة بادئة بحرف`I` هي عبارة عن [[Interface]] 
> - بس لحد دلوقتي لما تلاقي الكلمة دي اعرف انه يقصد انك تدخل Array أو List


## Example
```cs
using System.Collections.Generic;

#region Lists
// Make new list
var numbers = new List<int>() { 1, 2, 3, 4 };

// Add Items
numbers.Add(1);
numbers.AddRange(new int[3] {5, 6, 7});

// Iterate Items
foreach (var number in numbers)
    Console.WriteLine(number); // 1 2 3 4 1 5 6 7

// The First Index
Console.WriteLine("Index: " + numbers.IndexOf(1)); // Index: 0
// The Last Index
Console.WriteLine("Last Index: " + numbers.LastIndexOf(1)); // Last Index: 4

// Count == Length in simple array
Console.WriteLine("Count: " + numbers.Count); // Count: 8

// Remove
//numbers.Remove(1); // It will remove first 1
//foreach (var number in numbers)
//    Console.WriteLine(number);

// Remove all 1s

// Error
//foreach (var number in numbers)
//{
//    if (number == 1) numbers.Remove(number); //Error
//}
// It will give us exception because we can't change list and iterate it at same time
// In C#, you are not allowed to modify a Collection inside a foreach



for (var i = 0; i < numbers.Count; i++)
    if (numbers[i] == 1) numbers.Remove(numbers[i]);

foreach (var number in numbers)
    Console.WriteLine(number); // 2 3 4 5 6 7

// Remove all items
numbers.Clear();
Console.WriteLine("Count: " + numbers.Count); // Count = 0
#endregion
```

> [!fail]
> - منقدرش نستخدم ال [[Cs Control Flow Statements#Foreach|foreach]] وجواها نمسح حاجة من نفس ال collection هيجيبلي exception اللي اسمه `InvalidOperationException` 
> - في الحالة دي نقدر نستخدم ال for loop العادية

