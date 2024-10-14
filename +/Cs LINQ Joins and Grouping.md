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

### شرح الكود:
- هنا استخدمنا **group by** لتجميع الموظفين بناءً على **DepartmentID**.
- **empGroup.Key** بترجع **DepartmentID** لكل جروب.
- بعد كده، بنعرض اسماء الموظفين اللي في كل جروب باستخدام **Select**.

### الفرق بين Join وGroup:
- **Join**: بيربط الداتا بين مصدرين بناءً على شرط معين، زي مطابقة **DepartmentID** بين الجدولين.
- **Group**: بيجمع الداتا بناءً على قيمة معينة في مصدر واحد، زي تجميع الموظفين في جروب بناءً على الإدارة اللي هم فيها.

### مثال توضيحي لاستخدام Chunk:
تم ذكر مثال مهم جداً لاستخدام **Chunk** في المحاضرة، حيث لو عندك قائمة كبيرة من الموظفين وعايز تقسمهم على مجموعات أصغر (Chunk) علشان تقدر تعالج كل مجموعة بشكل مستقل في مهمة (Task) مختلفة:

```csharp
var employeeChunks = employees.Chunk(2); // تقسيم الموظفين إلى مجموعات من 2

foreach (var chunk in employeeChunks)
{
    Console.WriteLine("New Chunk:");
    foreach (var employee in chunk)
    {
        Console.WriteLine(employee.Name);
    }
}
```

### شرح الـ Chunk:
الميثود **Chunk** بتقسم البيانات إلى مجموعات (Chunks) حسب العدد اللي انت بتحدده. في المثال ده، قسمنا قائمة الموظفين إلى مجموعات كل مجموعة فيها 2 موظفين.

### الخلاصة:
- **Join** بيستخدم لما تكون عايز تجمع بيانات من مصدرين على أساس شرط معين.
- **Group** بيجمع بيانات من مصدر واحد بناءً على قيمة مشتركة.
- **Chunk** بيقسم البيانات لمجموعات أصغر لمعالجتها بسهولة أكبر. 

استخدام الـ **LINQ** بيسهل جداً التعامل مع البيانات ويوفر لك طرق سريعة وفعالة لتنفيذ عمليات معقدة زي **Join** و**Grouping**.