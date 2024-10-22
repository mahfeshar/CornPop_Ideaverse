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

### مثال تطبيقي أكبر:
خلينا نطبق كل اللي شرحناه في مثال عملي أكبر بدمج **Generic Class** مع **Generic Method** و**Constraints**.

#### الكود:
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

#### شرح الكود:
- هنا عندنا كلاس **Calculator** بيستخدم الـ **Generics** في ميثود **Add** و **Subtract** اللي بتقدر تتعامل مع أنواع رقمية مختلفة، سواء أرقام صحيحة أو أرقام عشرية.

#### استخدام الكود:
```csharp
Calculator calc = new Calculator();
int sum = calc.Add<int>(5, 10);
double diff = calc.Subtract<double>(10.5, 5.3);

Console.WriteLine(sum);  // هتطبع 15
Console.WriteLine(diff); // هتطبع 5.2
```

### الخلاصة:
- الـ **Generics** بيسمحوا بكتابة كود مرن وقابل لإعادة الاستخدام بشكل كبير، وبيوفروا عليك كتابة كود مكرر لأنواع بيانات مختلفة.
- بيحلوا مشاكل **Type Safety** اللي بتواجهنا في الـ **ArrayList** وبيساعدوا في تحسين أداء التطبيقات من خلال تجنب عمليات الـ **Boxing** و **Unboxing**.
- كمان، تقدر تستخدم **Constraints** عشان تتحكم في الأنواع اللي بتتعامل معاها في الـ **Generics**.