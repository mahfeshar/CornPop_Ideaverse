---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-14
---
### مقال عن LINQ: عمليات الفرز (Sorting) في C\#

 هتكونوا اتعرفتم على الأساسيات في LINQ وطرق كتابة الكود باستخدام الصيغتين المختلفتين (method syntax و query syntax). [[Cs LINQ Intro]]
 النهاردة، هنركز على كيفية فرز البيانات باستخدام LINQ وإزاي ده بيبسط التعامل مع القوائم بشكل كبير.

### 1. الترتيب التصاعدي والترتيب التنازلي

أول حاجة نبدأ بيها هي عمليات الترتيب الأساسية. 
لو عندك قائمة أرقام، وعايز ترتبها تصاعدي أو تنازلي، LINQ بيخليك تعمل ده بسهولة باستخدام `OrderBy` و `OrderByDescending`.

#### مثال 1: ترتيب الأرقام تصاعديًا

```cs
List<int> numbers = new List<int> { 7, 3, 9, 4, 6 };
var sortedNumbers = numbers.OrderBy(n => n);

var filteredAndSorted = from number in numbers 
						where number > 2 
						orderby number 
						select number

foreach (var num in sortedNumbers)
{
    Console.WriteLine(num);
}
```

النتيجة هنا هتكون:
```
3
4
6
7
9
```

#### مثال 2: ترتيب الأرقام تنازليًا

```cs
var sortedNumbersDesc = numbers.OrderByDescending(n => n);
var filteredAndSorted = from number in numbers 
						where number > 2 
						orderby number descending
						select number

foreach (var num in sortedNumbersDesc)
{
    Console.WriteLine(num);
}
```

النتيجة هتكون العكس:
```
9
7
6
4
3
```

### 2. الفلترة والفرز معًا

الترتيب لوحده كويس، لكن أحيانًا بتحتاج تجمع بين التصفية والفرز في نفس العملية. يعني مثلاً، لو عندك قائمة أرقام وعايز أولاً تصفي الأرقام اللي أكبر من 2 وبعدين ترتبهم.

#### مثال: تصفية الأرقام وترتيبها تصاعديًا

```cs
var filteredAndSorted = numbers.Where(n => n > 2).OrderBy(n => n);
var filteredAndSorted = from number in numbers 
						where number > 2 
						orderby number
						select number

foreach (var num in filteredAndSorted)
{
    Console.WriteLine(num);
}
```

في المثال ده، هنصفي الأرقام الأكبر من 2 وبعدين نرتبهم تصاعدي.

### 3. فرز حسب أكثر من معيار باستخدام `ThenBy`

أحيانًا البيانات بتحتاج تتفرز بناءً على أكتر من معيار. 
هنا بيجي دور `ThenBy` و `ThenByDescending`، اللي بيخلّوك ترتب على أكتر من مستوى. 
مثلاً، لو عندك قائمة موظفين، وعايز ترتبهم أولاً حسب الاسم، وبعدين حسب العمر لو الأسماء متشابهة.

#### مثال: ترتيب الموظفين حسب الاسم ثم حسب العمر

```cs
class Employee
{
    public string Name { get; set; }
    public int Age { get; set; }
    public int Salary { get; set; }
}

List<Employee> employees = new List<Employee>
{
    new Employee { Name = "Ahmed", Age = 35, Salary = 6000 },
    new Employee { Name = "Ahmed", Age = 30, Salary = 4000 },
    new Employee { Name = "Mohamed", Age = 38, Salary = 8000 },
    new Employee { Name = "Ayman", Age = 35, Salary = 7000 }
};

var sortedEmployees = employees.OrderBy(e => e.Name).ThenBy(e => e.Age);

foreach (var emp in sortedEmployees)
{
    Console.WriteLine($"{emp.Name}, {emp.Age}");
}
```

النتيجة هتكون:
```
Ahmed, 30
Ahmed, 35
Ayman, 35
Mohamed, 38
```

في المثال ده، تم ترتيب الموظفين حسب الاسم أولاً، وبعدين حسب العمر لو الأسماء متشابهة.

### 4. استخدام `OrderBy` و `OrderByDescending` مع `ThenBy`

في بعض الحالات، هتحتاج تدمج `OrderBy` مع `ThenBy` عشان ترتب البيانات على أكتر من مستوى، وده بيظهر ليك قوة LINQ في معالجة البيانات بطريقة منظمة وسهلة القراءة.

#### مثال على الترتيب المختلط:
```cs
var sortedEmployees = employees.OrderBy(e => e.Name).ThenByDescending(e => e.Salary);

foreach (var emp in sortedEmployees)
{
    Console.WriteLine($"{emp.Name}, {emp.Salary}");
}
```

في المثال ده، تم ترتيب الموظفين حسب الاسم أولاً، وبعدين حسب المرتب بشكل تنازلي.

### 5. الترتيب العكسي باستخدام Reverse

أحيانًا بعد ما ترتب البيانات، بتحب تقلب الترتيب كليًا. هنا بيجي دور `Reverse()` اللي بيخلّي العناصر تظهر بالعكس.

#### مثال: عكس الترتيب

```cs
var reversedList = numbers.OrderBy(n => n).Reverse();

foreach (var num in reversedList)
{
    Console.WriteLine(num);
}
```

### 6. **مشاكل الأداء**

لازم تاخد بالك إن الترتيب قبل التصفية ممكن يبطّئ الأداء خصوصًا لو عندك بيانات كبيرة. عشان كده، الأفضل دايمًا إنك تصفي الأول وبعدين ترتب. ده هيوفر وقت لأن الترتيب بيتم على البيانات اللي تصفيت بس، مش على كل القائمة.

### 7. التعبيرات المجهولة (Anonymous Types)

ممكن كمان تستخدم **التعبيرات المجهولة** لو حبيت ترجع بيانات محددة من الكائنات بدل ما ترجع الكائن بالكامل.

#### مثال: استخدام التعبيرات المجهولة لترتيب جزء من البيانات

```cs
var selectedData = employees.OrderBy(e => e.Name).Select(e => new { e.Name, e.Age });

selectedDate = from employee in employyes
				orderby employee.Name
				select new {employeeName = employee.Name,x.Age};

foreach (var emp in selectedData)
{
    Console.WriteLine($"{emp.Name}, {emp.Age}");
}
```

### 8. التحقق من النوع باستخدام `OfType`

الـ `OfType` واحدة من الميزات المهمة اللي بتستخدم لما يكون عندك **List** فيها عناصر من أنواع مختلفة، وعايز ترجع فقط العناصر من نوع معين. 

#### مثال: استخدام `OfType` لتصفية الأنواع

خلينا نبدأ بإننا ننشئ كلاسيس مختلفة:

```cs
class Contractor
{
    public string ContractorName { get; set; }
}

class Employee
{
    public string Name { get; set; }
    public int Age { get; set; }
    public int Salary { get; set; }
}
```

دلوقتي، هنعمل **List** تجمع بين الـ **Employee** و **Contractor**.

```cs
List<object> people = new List<object>
{
    new Employee { Name = "Ahmed", Age = 35, Salary = 6000 },
    new Employee { Name = "Mohamed", Age = 38, Salary = 8000 },
    new Contractor { ContractorName = "Khaled" },
    new Contractor { ContractorName = "Moustafa" }
};
```

لو عايزين نصفي القائمة دي بحيث نرجع فقط الـ **Contractors**، هنا بنستخدم `OfType`:

#### استخدام `OfType` للحصول على الـ Contractors فقط:

```cs
var contractors = people.OfType<Contractor>();

foreach (var contractor in contractors)
{
    Console.WriteLine(contractor.ContractorName);
}
```

النتيجة:
```
Khaled
Moustafa
```

### 9. استخدام Where مع التحقق من النوع

بديل لاستخدام `OfType` هو استخدام `Where` مع `is` للتحقق من النوع، وده بيخليك تتحكم أكتر في الشرط اللي عايز تطبقه.

#### مثال: استخدام `Where` مع `is`:

```cs
var contractorsUsingWhere = people.Where(x => x is Contractor);

foreach (Contractor contractor in contractorsUsingWhere)
{
    Console.WriteLine(contractor.ContractorName);
}
```

النتيجة هي نفسها، ولكن باستخدام `Where`.

### 10. الفرق بين `OfType` و Where مع is

- الـ`OfType`: بترجع لك العناصر اللي هي من النوع المحدد بس. 
  يعني لو حددت `OfType<Contractor>` هترجع فقط العناصر اللي من النوع **Contractor** وتتجاهل الباقي.
  
- الـ**Where مع is**: بيخليك تتحقق من النوع بناءً على شرط معين باستخدام الـ `is`، وبتكون أكتر مرونة في كتابة الشروط أو حتى التحقق من أكتر من نوع لو عايز.

#### مثال على الفرق:

```cs
// OfType: بيجيب الـ Contractors بس
var contractors = people.OfType<Contractor>();

// Where مع is: بيجيب العناصر اللي هي Contractors وبتطبق أي شرط إضافي
var contractorsUsingWhere = people.Where(x => x is Contractor && ((Contractor)x).ContractorName.StartsWith("K"));
```

في المثال ده، **Where** بيزود مرونة أكبر، لأنه ممكن تتحقق من النوع وتطبق شروط إضافية في نفس الوقت.
الفرق الأساسي بين **`OfType`** و **Where مع is** هو في المرونة: **`OfType`** مباشر وبسيط في الاستخدام، بينما **Where مع is** بيديك مرونة أكبر لو عايز تضيف شروط مع التحقق من النوع.
### خلاصة

عمليات الترتيب باستخدام LINQ بتوفر مرونة وسهولة كبيرة في التعامل مع البيانات في C#. 
سواء كنت بتتعامل مع القوائم أو المجموعات الكبيرة، LINQ بيساعدك على فرز البيانات بطريقة فعّالة ومنظمة. 
ومن خلال الفهم الجيد لأدوات الترتيب زي `OrderBy`، و `ThenBy`، و `Reverse`، تقدر تبني حلول مرتبة وسريعة.