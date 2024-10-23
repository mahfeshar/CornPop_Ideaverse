---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-14
---
### مراجعة سريعة لمفهوم الـ Generics:
عرفنا إن كل الأنواع (Types) في .NET بتنبع من نوع كبير اسمه **[[Cs System.Object]]**، بمعنى إن كل حاجة في النهاية هي **Object** سواء كانت أنواع مدمجة في .NET زي الأعداد (Integers) أو النصوص (Strings)، أو أنواع انت بتبنيها بنفسك زي الـ **Custom Classes**.

#### الـArrayList كمثال:
وشوفنا دا في درس الـ [[Cs ArrayList]]
لو انت بتستخدم حاجة زي **ArrayList**، فهي قائمة تستطيع تخزين أي نوع من البيانات لأن كل حاجة تعتبر **Object**، فممكن تخزن أرقام، نصوص، أو حتى كائنات من **Classes** مختلفة. 
وده بيدي مرونة كبيرة، لكن في نفس الوقت فيه بعض العيوب.

#### عيوب الـ ArrayList:
- الـ**Boxing و Unboxing**: لما تخزن نوع بيانات زي الأعداد (int) في **ArrayList**، بيحصل **Boxing** لتحويل القيمة لنوع **Object**، ولما تسترجعها بيحصل **Unboxing**. العمليات دي بتأثر على الأداء (Performance) حتى لو بشكل غير ملحوظ في التطبيقات الصغيرة.
- الـ**Type Safety**: بما إن **ArrayList** بتخزن أي نوع من البيانات، مفيش حماية على مستوى النوع (Type Safety). 
  ممكن تضيف أي نوع من البيانات بدون أي قيود، وده ممكن يؤدي لأخطاء في وقت التشغيل (Runtime Errors).

#### الحل في الـ Generic List:
عشان نتغلب على المشاكل دي، بنستخدم الـ **[[Cs Generic List & Dictionary#**Generic List **|Generic List]]**. 
مثال على كده:
```csharp
List<int> numbers = new List<int>();
numbers.Add(1);
numbers.Add(2);
numbers.Add(3);
```
هنا **List** بقت مخصصة لنوع **int** فقط. 
ده بيمنع إضافة أي نوع آخر من البيانات ويحل مشكلة **Type Safety**.

### إزاي نبني Generic Class بنفسك؟
يعني إزاي تخلي كلاس يستقبل أي نوع (Type) ويتعامل معاه.
#### الكود:
```csharp
public class GenericList<T>
{
    private List<T> items = new List<T>();

    public void Add(T item)
    {
        items.Add(item);
    }

    public int Count
    {
        get { return items.Count; }
    }

    public T GetItem(int index)
    {
        return items[index];
    }
}
```

تقدر تعرف أكتر من Generic Type
```cs
public static void SWAP <T, T1, T2> (ref T num1, ref T num2)
{
	// CODE
}
```
#### شرح الكود:
- الـ**T** هو Placeholder لنوع البيانات اللي المستخدم هيحدده عند إنشاء **`GenericList`**. 
- في الكود ده، أنشأنا **List** داخلية من النوع **T**، وأضفنا ميثود **`Add`** عشان نضيف العناصر، و **`GetItem`** لاسترجاع عنصر معين.

#### استخدام الـ Generic Class:
```csharp
GenericList<int> myList = new GenericList<int>();
myList.Add(10);
myList.Add(20);

Console.WriteLine(myList.GetItem(0));  // هتطبع 10
```

### بناء Generic Method:
كمان ممكن تبني ميثود تستقبل نوع Generic. 
يعني ميثود تكون مرنة إنها تتعامل مع أنواع مختلفة بناءً على اللي المستخدم يحدده.

#### الكود:
```csharp
public T Add<T>(T a, T b)
{
    return (dynamic)a + (dynamic)b;
}
```

#### شرح الكود:
- الميثود دي بتاخد نوع **T** (اللي بيحدده المستخدم)، وتعمل عملية جمع (Addition) بين القيمتين.

#### استخدام الـ Generic Method:
```csharp
int result = Add<int>(5, 10);
double resultDouble = Add<double>(5.5, 10.3);

Console.WriteLine(result);        // هتطبع 15
Console.WriteLine(resultDouble);  // هتطبع 15.8
```

> [!info]
> In Case Generic Type "T" is declared on **method** level, Not Class, Not Interface, Not Struct
> Compiler can detect the type of "T" based on the type of the method Input Parameters
> ```cs
> int A = 5;
> int B = 10;
> Helper.Swap(ref A, ref B)
> double A = 5;
> double B = 10;
> Helper.Swap(ref A, ref B)
> ```
### الـ Constraints على Generics:
في بعض الأحيان، ممكن تحتاج تحط شروط (Constraints) على الأنواع اللي بتتعامل معاها في الـ **Generics**. 
مثلاً، ممكن تضيف شرط إن النوع اللي المستخدم هيبعتوا لازم يكون نوع رقمي.

#### الكود:
```csharp
// Value Type
public T Add<T>(T a, T b) where T : struct
{
    return (dynamic)a + (dynamic)b;
}

// Number
public T Add<T>(T a, T b) where T : INumber<T>
{
	return a + b;
}

// Reference Type
public T Add<T>(T a, T b) where T : class 
{
    // Code
}

// Parameterless ctor
public T Add<T>(T a, T b) where T : new() 
{
    // Code
}

// Class or child for it
public T Add<T>(T a, T b) where T : Employee
{
    // Code
}
```

#### شرح الكود:
- استخدمنا **where T : struct** عشان نحدد إن **T** لازم يكون نوع قيمة (Value Type) زي الأرقام أو البيانات اللي بتخزن في الذاكرة مباشرةً.

### الـ Generics في Classes و Methods:
الـ Generics مش بتسهل بس كتابة كود مختصر وفعال، لكنها كمان بتحل مشكلة **Type Safety** وبتديك مرونة في التعامل مع أنواع مختلفة بدون الحاجة لكتابة كود مكرر.

### Examples:
#### Example 1:
```csharp
public class Calculator
{
    public T Add<T>(T a, T b) where T : struct
    {
        return (dynamic)a + (dynamic)b;
    }

    public T Subtract<T>(T a, T b) where T : struct
    {
        return (dynamic)a - (dynamic)b;
    }
}
```

- هنا عندنا كلاس **Calculator** بيستخدم الـ **Generics** في ميثود **Add** و **Subtract** اللي بتقدر تتعامل مع أنواع رقمية مختلفة، سواء أرقام صحيحة أو أرقام عشرية.

```csharp
Calculator calc = new Calculator();
int sum = calc.Add<int>(5, 10);
double diff = calc.Subtract<double>(10.5, 5.3);

Console.WriteLine(sum);  // هتطبع 15
Console.WriteLine(diff); // هتطبع 5.2
```
#### Example 2
```cs
class Helper
{
    public static void Swap (ref int A, ref int B)
    {
        Console.WriteLine("====Swap====");
        int temp = A;
        A = B;
        B = temp;
    }
}

// MAIN
int a = 5;
int b = 10;
Console.WriteLine($"a = {a}");
Console.WriteLine($"b = {b}");
Helper.Swap(ref a, ref b);
Console.WriteLine($"a = {a}");
Console.WriteLine($"b = {b}");
Console.WriteLine("-----------------------");
double d = 2.2;
double c = 3.3;
Helper.Swap(ref d, ref c); // ERROR
/* 
OUTPUT:
a = 5
b = 10
====Swap====
a = 10
b = 5
*/

// Solution 
class Helper
{
    public static void Swap<T> (ref T A, ref T B)
    {
        Console.WriteLine("====Swap====");
        T temp = A;
        A = B;
        B = temp;
    }
}

/*
OUTPUT:
a = 5
b = 10
====Swap====
a = 10
b = 5
-----------------------
d = 2.2
c = 3.3
====Swap====
d = 3.3
c = 2.2
*/
```
#### Example 3
Read before, [[Cs Equality]]
```cs
static class Helper
{
    public static int SearchArray(int[] arr, int value)
    {
        for (int i = 0; i < arr?.Length; i++)
        { 
            if (arr[i] == value)
                return i;
        }
        return -1;
    }
}

// MAIN
int[] array = { 1, 2, 6, 4, 10, 13, 20 };
double[] doubles = { 2.1, 10.2, 12.3 };
Console.WriteLine(Helper.SearchArray(array, 10)); // 4
Console.WriteLine(Helper.SearchArray(array, 5));  // -1
Console.WriteLine(Helper.SearchArray(doubles, 10.2)); // ERROR

// SOLUTION: Is to make it Generic But
class Employee
{
    
    public int Id { get; set; }
    public string Name { get; set; }
    public int Salary { get; set; }
    public Employee(int _id, string _name, int _salary)
    {
        Id = _id;
        Name = _name;
        Salary = _salary;
    }
}

static class Helper <T>
{
    public static int SearchArray(T[] arr, T value)
    {
        for (int i = 0; i < arr?.Length; i++)
        { 
            if (arr[i].Equals(value))
                return i;
        }
        return -1;
    }
}

// MAIN
Employee[] employees = {
    new (15, "Ahmed", 13_000),
    new (20, "Salma", 50_000),
    new (35, "Corn", 5_000)
};
Console.WriteLine(Helper<Employee>.SearchArray(employees, new(35, "Corn", 5_000))); // -1
// The address is not equals
```

المشكلة اللي هتحصل ان فيه حاجات مفيش فيها الـ `\==` فدا بيعمل مشاكل إنه ميعرفش هيعملها ازاي فعشان كدا 
الحل اننا نستخدم الـ Equals اللي بيورثها من الـ Object عشان هي موجودة في كله
وبعد كدا أقدر أعملها Overloading في الـ Class بتاعي
#### Example 4

### الخلاصة:
- الـ **Generics** بيسمحوا بكتابة كود مرن وقابل لإعادة الاستخدام بشكل كبير، وبيوفروا عليك كتابة كود مكرر لأنواع بيانات مختلفة.
- بيحلوا مشاكل **Type Safety** اللي بتواجهنا في الـ **ArrayList** وبيساعدوا في تحسين أداء التطبيقات من خلال تجنب عمليات الـ **Boxing** و **Unboxing**.
- كمان، تقدر تستخدم **Constraints** عشان تتحكم في الأنواع اللي بتتعامل معاها في الـ **Generics**.