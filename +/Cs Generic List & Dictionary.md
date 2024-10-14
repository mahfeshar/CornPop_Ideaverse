---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-14
---
الـ Generic شرحناها في الـ [[Generic Type]]
## الـ Generic List والـ Dictionary في C\#

النوعين دول هتحتاجهم كتير في مشاريعك علشان بيسهلوا التعامل مع البيانات بشكل مرن ومنظم. 

### **Generic List:**
الـ **Generic List** هي نسخة متطورة من الـ **[[Cs ArrayList]]** اللي شرحناها قبل كده. 
الفرق الأساسي بين الـ **ArrayList** والـ **Generic List** هو إن الأخيرة بتديلك مرونة أكبر من ناحية نوع البيانات، وكمان بتحافظ على الكفاءة لأنها مش بتحتاج لعمليات الـ **Boxing** و **Unboxing**.

#### إيه هو الـ Generic List؟
بكل بساطة، الـ **Generic List** هي نوع "عام" تقدر تحط فيه أي نوع من البيانات، لكن بشرط إنك تحدد النوع ده من الأول. 
يعني لو قولتله "حط أرقام" مش هيقبل غير أرقام، ولو قولتله "حط نصوص" مش هيقبل غير نصوص.

#### إزاي بنكتب الـ Generic List؟

الكود ده بيوضح إزاي ممكن تعرف **Generic List** وتستخدمها:

```csharp
List<int> numbers = new List<int>(); 
// بنحدد هنا إن الليست هتشيل أرقام فقط
numbers.Add(1);
numbers.Add(2);
numbers.Add(3);

// بنجمع رقم على أول عنصر
int sum = numbers[0] + 10;
Console.WriteLine(sum); // Output: 11
```

هنا، حددنا نوع البيانات اللي هيتخزن جوه الليست إنها أرقام (int). 
ده بيريحك من عمليات التحويل اللي بتعملها في الـ **ArrayList** وبيخلي الكود أسرع.

#### الفرق بين Generic List و ArrayList:
- الـ**ArrayList** تقدر تحط فيها أي نوع من البيانات، بس لما تيجي تستخدم البيانات دي، لازم تعمل لها **Unboxing** وترجعها لنوعها الأصلي.
- الـ**Generic List** بتطلب منك تحدد نوع البيانات من الأول، فمفيش حاجة اسمها **Boxing** و **Unboxing**، وبالتالي الكود أسرع وأكتر أمان.

### **Operations على Generic List**:
الـ **Generic List** بتديك كل المميزات اللي كانت موجودة في الـ **ArrayList** وزيادة. 
تقدر تضيف عناصر، تشيل، تدور على العناصر، وهكذا.

![[Pasted image 20240715110644.png]]
#### مثال:

```csharp
List<string> names = new List<string>();
names.Add("Ahmed");
names.Add("Mona");

// إزالة عنصر من الليست
names.Remove("Ahmed");

// البحث عن عنصر في الليست
int index = names.IndexOf("Mona");
Console.WriteLine(index); // Output: 0
```

العمليات زي **Add** و **Remove** بتشتغل زي ما هي في الـ **ArrayList**، لكن هنا مش محتاج تعمل **Boxing** أو **Unboxing**.

### الـ**Capacity و Resize في Generic List**:
الـ **Generic List** بيكون عندها حاجة اسمها **Capacity**. 
يعني دي السعة القصوى اللي ممكن الليست تشيلها قبل ما تعمل عملية توسيع (Resize). لما الليست تتملى على الآخر، بتكبر نفسها تلقائيًا عشان تشيل عناصر أكتر.
شرحنا طريقة العمل دي قبل كدا في [[Array#Dynamic Arrays|Dynamic Array]]

#### مثال:
```csharp
List<int> numbers = new List<int>(3); // السعة الأولية 3
numbers.Add(1);
numbers.Add(2);
numbers.Add(3);
numbers.Add(4); // هنا الليست بتعمل Resize تلقائي
```

#### Implementation for capacity
لما بنستخدم الـ **Generic List**، فيه حاجة اسمها **Capacity**، وهي السعة اللي بتحدد عدد العناصر اللي الليست تقدر تشيلهم قبل ما تحتاج تعمل "توسيع" للذاكرة.

1. **التأكد من السعة المطلوبة**: أول حاجة بيتأكد منها الكود هو إذا كانت القيمة الجديدة (الـ **Capacity**) بتساوي الـ **Length** (عدد العناصر الحالي في الليست) ولا لأ. لو بيساويها، مفيش حاجة بيعملها؛ أما لو مش بيساويها، بيبدأ يتأكد من القيمة.

2. **لو القيمة الجديدة صفر**:
    - هنا بيتأكد إذا كانت القيمة اللي أنت اديتهاله أقل من أو تساوي صفر. لو فعلاً صفر، فهو بيعمل ليك **Empty Array** عشان يبدأ من جديد.
    
    ```cs
    _items = s_emptyArray;
    ```

3. **لو القيمة الجديدة أكبر من صفر**:
    - لو القيمة الجديدة أكبر من صفر، فهو بيعمل **Array** جديدة بالقيمة اللي انت اديتهاله، وبيروح ينسخ البيانات اللي كانت موجودة في الـ **Array** القديمة للـ **Array** الجديدة.

    ```cs
    T[] newItems = new T[value];
    if (_size > 0)
    {
        Array.Copy(_items, newItems, _size);
    }
    _items = newItems;
    ```

##### شرح الـ Add Method

الـ **Add** في الـ **Generic List** بيسمحلك تضيف عناصر جديدة. 
الليست بتشتغل بكفاءة طالما لسا عندها مساحة فاضية، ولو المساحة خلصت، هي بتزود نفسها تلقائيًا.

```cs
public void Add(T item)
{
    _version++;
    T[] array = _items;
    int size = _size;
    if ((uint)size < (uint)array.Length)
    {
        _size = size + 1;
        array[size] = item;
    }
    else
    {
        AddWithResize(item);
    }
}
```

- في الأول، بيشوف إذا كانت السعة لسا فيها مكان كافي للعنصر الجديد. لو لسا فيه مكان:
    - بيزود الـ **size** بواحد، ويحط العنصر في المكان الفاضي.

- أما لو السعة اتملت، بيلجأ للـ **`AddWithResize`** عشان يعمل توسيع للذاكرة.

##### شرح الـ `AddWithResize`

الـ **`AddWithResize`** هو اللي بيقوم بعملية التوسيع لو الليست اتملت وما فيش مكان فاضي.

```cs
private void AddWithResize(T item)
{
    Debug.Assert(_size == _items.Length); 
    // يتأكد إن المساحة اتملت
    int size = _size;
    Grow(size + 1);  
    // ينادي على الميثود اللي بتعمل التوسيع
    _size = size + 1;
    _items[size] = item; 
    // يحط العنصر الجديد
}
```

- في الأول بيتأكد إن المساحة اتملت، وبعدين ينادي على **Grow** عشان تعمل التوسيع وتجهز مساحة جديدة للعناصر اللي جايه.

##### شرح الـ Grow

الميثود **Grow** هي اللي بتقوم بالتوسيع الفعلي للليست.

```cs
internal void Grow(int capacity)
{
    Debug.Assert(_items.Length < capacity);

    int newCapacity = _items.Length == 0 ? DefaultCapacity : 2 * _items.Length; 
    // السعة الجديدة بتبقى ضعف السعة القديمة

    if ((uint)newCapacity > Array.MaxLength) newCapacity = Array.MaxLength;

    if (newCapacity < capacity) newCapacity = capacity;

    Capacity = newCapacity;
}
```

- أول حاجة بتعملها **Grow** إنها بتشوف لو الليست فاضية (السعة بصفر)، لو فعلاً فاضية، بتحط السعة الافتراضية اللي هي 4.
  
- لو مش فاضية، بتضاعف السعة (بتضربها في 2). يعني كل ما الليست تتملى، السعة بتزيد للضعف.

- لو السعة الجديدة أكبر من الحد الأقصى (Array.MaxLength)، بيروح يحدد السعة للحد الأقصى المسموح بيه.

### الخلاصة

- **Capacity** في **Generic List** هي السعة اللي الليست تقدر تشيلها قبل ما تحتاج توسع نفسها.
- لما الليست تتملى، بتعمل **Resize** أو توسيع، وده بيحصل بشكل ديناميكي.
- الميثود **Grow** بتقوم بزيادة السعة للضعف في كل مرة الليست تتملى.

بكده، كل ما تضيف عناصر للـ **Generic List**، الليست بتزود نفسها بشكل تلقائي لما تتملى، وده بيخليها مرنة وسهلة في التعامل مع البيانات.
### **Dictionary:**
نيجي بقى للـ **Dictionary**. 
الـ **Dictionary** في C# شبيهة بالقاموس. 
بتخزن البيانات عن طريق **Key** و **Value**. 
يعني بدل ما توصل للبيانات باستخدام **Index** زي الليست، بتستخدم **Key** عشان تجيب **Value**.

#### إزاي بنكتب الـ Dictionary؟

الكود ده بيوضح إزاي ممكن تعرف **Dictionary** وتستخدمها:

```csharp
Dictionary<string, string> passwords = new Dictionary<string, string>();

// إضافة مفتاح (Key) وقيمة (Value)
passwords.Add("Gmail", "mysecretpassword");
passwords.Add("Facebook", "mypassword");

// قراءة قيمة باستخدام المفتاح
Console.WriteLine(passwords["Gmail"]); // Output: mysecretpassword
```

هنا، استخدمنا **Dictionary** علشان نخزن كلمات السر لكل موقع باستخدام اسم الموقع كمفتاح.

### **الـOperations على Dictionary**:
تقدر تضيف، تشيل، وتدور على البيانات باستخدام **Key** بدل ما تستخدم **Index**. وده بيدي الـ **Dictionary** مرونة كبيرة.

#### مثال:

```csharp
// التأكد إذا كان المفتاح موجود قبل الإضافة
if (!passwords.ContainsKey("Gmail"))
{
    passwords.Add("Gmail", "anotherpassword");
}

// إزالة عنصر باستخدام المفتاح
passwords.Remove("Facebook");
```

### **TryGetValue**:
لو مش متأكد إذا كان المفتاح موجود ولا لأ، تقدر تستخدم **TryGetValue** بدل ما تستخدم **ContainsKey** وتعملها في خطوة واحدة.

#### مثال:
```csharp
if (passwords.TryGetValue("Gmail", out string password))
{
    Console.WriteLine(password); // Output: mysecretpassword
}
else
{
    Console.WriteLine("Password not found");
}
```

### **الخلاصة**:
- **Generic List** بتديلك مرونة أكبر من ناحية النوع والتعامل مع البيانات بطريقة أسرع وأكتر أمان من الـ **ArrayList**.
- **Dictionary** بتستخدم لما تكون عايز تخزن بيانات وتوصل لها باستخدام **Key** بدل **Index**.

دي كانت نظرة سريعة على الـ **Generic List** والـ **Dictionary** في C#. جرب بنفسك وابدأ تلعب بالكود عشان تطبق اللي اتعلمته.