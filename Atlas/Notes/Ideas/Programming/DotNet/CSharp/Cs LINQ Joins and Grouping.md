---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-14
---


هنشرح كيفية استخدام **LINQ** في **C#** لتطبيق عمليتي **Join** و**Grouping**. 
الاتنين دول بيستخدموا بشكل كبير لما بيكون عندنا داتا متقسمة على أكثر من مصدر، سواء كان في قواعد البيانات أو حتى في قوائم عادية زي ما هنشوف في المثال اللي جاي.
### **Join**:
فكرة الـ **Join** بتقوم على أنك عندك مصدرين للداتا (زي جدولين في قاعدة بيانات) فيهم بيانات مرتبطة ببعض، وعايز تجمع البيانات دي مع بعضها على أساس شرط معين. زي إنك تكون عندك جدول للموظفين وجدول للإدارات، وكل موظف بيكون مرتبط بإدارة معينة عن طريق **DepartmentID**. 

#### مثال على الـ Join:
في المثال اللي في المحاضرة، كان عندنا قائمتين: 
1. قائمة الموظفين.
2. قائمة الإدارات.

وعايزين نربط كل موظف بالإدارة بتاعته.

```csharp
// نموذج الموظفين
var employees = new List<Employee>
{
    new Employee { Name = "Mohamed", DepartmentID = 1 },
    new Employee { Name = "Ahmed", DepartmentID = 2 },
    new Employee { Name = "Ayman", DepartmentID = 3 },
    new Employee { Name = "Sara", DepartmentID = 4 }
};

// نموذج الإدارات
var departments = new List<Department>
{
    new Department { DepartmentID = 1, Name = "HR" },
    new Department { DepartmentID = 2, Name = "IT" },
    new Department { DepartmentID = 3, Name = "Finance" },
    new Department { DepartmentID = 4, Name = "Marketing" }
};

// تنفيذ عملية الـ Join باستخدام LINQ
var query = from emp in employees
            join dept in departments 
            on emp.DepartmentID equals dept.DepartmentID
            select new
            {
                EmployeeName = emp.Name,
                DepartmentName = dept.Name
            };

// عرض النتيجة
foreach (var item in query)
{
    Console.WriteLine($"Employee: {item.EmployeeName}, Department: {item.DepartmentName}");
}
```
الـ Join بالطريقة دي زي الـ SQL بالظبط، يعني لو فيه حاجة مش موجودة مش هيعرضها يعني لو قولت ان فيه موظف شغال في الـ Department رقم 9 ودا مش موجود فمش هيعرضه

إنما بالـ Method syntax:
```cs
// className.Join(AnotherClass, FunctionForID, FunctionForAnotherId, (firstParaEmp, secondParaDep)=> new {output});
var query = employees.Join(departments, x=> x.DepartmentId, x=> x.ID).;
```

#### شرح الكود:
- هنا استخدمنا **LINQ Join** لربط الموظفين بالإدارات بتاعتهم بناءً على **DepartmentID**.
- جملة **join** بتعمل الربط بين الـ **employees** و**departments** على أساس تطابق **DepartmentID** في الجدولين.
- بعد الربط، بنختار نرجع اسم الموظف والإدارة باستخدام **select**.

### **Grouping**:
الـ **Grouping** بيستخدم لتجميع البيانات بناءً على قيمة معينة. مثلاً لو عندك مجموعة موظفين في إدارات مختلفة، وعايز تجمع الموظفين اللي في كل إدارة مع بعض.

#### مثال على Grouping:
في المثال ده، هنرجع كل الموظفين في كل إدارة.

```csharp
var groupedQuery = from emp in employees
                   group emp by emp.DepartmentID into empGroup
                   select new
                   {
                       DepartmentID = empGroup.Key,
                       Employees = empGroup.Select(e => e.Name)
                   };

// عرض النتيجة
foreach (var group in groupedQuery)
{
    Console.WriteLine($"Department ID: {group.DepartmentID}");
    foreach (var emp in group.Employees)
    {
        Console.WriteLine($" - {emp}");
    }
}
```

```cs
var groupedQuery = employees
    .GroupBy(emp => emp.DepartmentID)
    .Select(empGroup => new
    {
        DepartmentID = empGroup.Key,
        Employees = empGroup.Select(e => e.Name)
    });

// عرض النتيجة
foreach (var group in groupedQuery)
{
    Console.WriteLine($"Department ID: {group.DepartmentID}");
    foreach (var emp in group.Employees)
    {
        Console.WriteLine($" - {emp}");
    }
}
```

#### شرح الكود:
- هنا استخدمنا **group by** لتجميع الموظفين بناءً على **DepartmentID**.
- الـ**empGroup.Key** بترجع **DepartmentID** لكل جروب.
- بعد كده، بنعرض اسماء الموظفين اللي في كل جروب باستخدام **Select**.

### الفرق بين Join وGroup:
- الـ**Join**: بيربط الداتا بين مصدرين بناءً على شرط معين، زي مطابقة **DepartmentID** بين الجدولين.
- الـ**Group**: بيجمع الداتا بناءً على قيمة معينة في مصدر واحد، زي تجميع الموظفين في جروب بناءً على الإدارة اللي هم فيها.

### Interfaces and LINQ
الـ **LINQ** تعتمد على اثنين من الواجهات ([[Cs Interface]]) الرئيسية التي تُسهل عملها. وهما:

1. **`IEnumerable<T>`**
2. **`IQueryable<T>`**

#### 1. **`IEnumerable<T>`**:
هذه الواجهة تعتبر الأساس الذي تبني عليه الـ **LINQ to Objects**، وتستخدم للعمل مع البيانات التي تكون محملة بالفعل في الذاكرة. لما تكون عندك بيانات جاهزة وموجودة في الميموري (مثل قائمة، مصفوفة، أو كائنات عامة)، تقدر تستخدم LINQ مع **`IEnumerable<T>`** لمعالجة البيانات.

**أهم خصائصها**:
- تستخدم لتنفيذ استعلامات LINQ على كائنات **محملة في الذاكرة**.
- تقوم بتنفيذ الاستعلام **بطريقة متسلسلة**، يعني أنه يتعامل مع البيانات بشكل مباشر.
- تُستخدم في السيناريوهات التي تكون فيها البيانات صغيرة نسبيًا ولا تحتاج للوصول إلى مصدر خارجي (مثل قواعد البيانات).

##### مثال:
```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
var result = numbers.Where(n => n > 3);

foreach (var num in result)
{
    Console.WriteLine(num);
}
```
هنا، الـ `numbers` محملة في الذاكرة، واستخدام LINQ يعتمد على الـ`IEnumerable<int>`.

#### 2. **`IQueryable<T>`**:
أما هذه الواجهة، فهي تستخدم في سيناريوهات **LINQ to SQL** أو **LINQ to Entities** عندما نريد التعامل مع مصادر بيانات خارجية (مثل قواعد البيانات). 
الـ`IQueryable<T>` تختلف عن `IEnumerable<T>` في أنها تقوم بإنشاء استعلام يتم تنفيذه **على المصدر الخارجي** وليس في الذاكرة، وهذا يسمح بتنفيذ استعلامات معقدة وتحسين الأداء.

**أهم خصائصها**:
- تستخدم مع مصادر البيانات الخارجية، مثل قواعد البيانات.
- تقوم بإنشاء استعلام يتم تحويله إلى لغة المصدر (مثل SQL) وتنفيذه هناك.
- تستخدم **التنفيذ المتأخر** (deferred execution)، مما يعني أن الاستعلام لا يتم تنفيذه حتى تطلب النتيجة فعلاً.
- تُستخدم في السيناريوهات التي تحتاج فيها إلى الوصول إلى بيانات كبيرة أو خارجية.

##### مثال:
```csharp
var query = dbContext.Employees.Where(emp => emp.Salary > 5000);
```
هنا، الـ `Employees` ليست محملة في الذاكرة، ولكن الاستعلام يتم تحويله إلى SQL ليتم تنفيذه على قاعدة البيانات.

#### الفرق بين **`IEnumerable<T>`** و **`IQueryable<T>`**:
- ال`IEnumerable<T>` تستخدم مع البيانات الموجودة بالفعل في الذاكرة، أما **`IQueryable<T>`** فتستخدم مع مصادر البيانات الخارجية مثل قواعد البيانات.
- الـ`IQueryable<T>` تتيح تحسين الأداء عن طريق تحويل الاستعلامات إلى SQL أو استعلامات مناسبة للمصدر الخارجي.
- الـ`IEnumerable<T>` تقوم بتنفيذ الاستعلام في الذاكرة مباشرة، بينما `IQueryable<T>` تقوم بإنشاء استعلام يُنفذ في الوقت الذي تحتاج فيه للنتائج.

#### العلاقة مع LINQ:
- الـ**LINQ to Objects** تعتمد على **`IEnumerable<T>`**، وتستخدم للعمل مع البيانات الموجودة بالفعل في الذاكرة.
- الـ**LINQ to SQL** أو **LINQ to Entities** تعتمد على **`IQueryable<T>`**، وتستخدم للوصول إلى البيانات من مصادر خارجية وتنفيذ الاستعلامات هناك.
### الخلاصة:
- الـ**Join** بيستخدم لما تكون عايز تجمع بيانات من مصدرين على أساس شرط معين.
- الـ**Group** بيجمع بيانات من مصدر واحد بناءً على قيمة مشتركة.