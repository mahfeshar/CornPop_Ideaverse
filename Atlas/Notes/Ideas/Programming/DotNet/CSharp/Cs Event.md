---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
---
## الأحداث (Events) في C#

تعتبر الأحداث من المفاهيم الأساسية في البرمجة بلغة C#، وخصوصًا في تطوير التطبيقات المتقدمة.

### What is Event?
الـ Events هي إشعارات أو تنبيهات تحدث عندما يحدث شيء مهم في البرنامج. 
بمعنى آخر، عندما يحصل حدث معين في الكود، يتم إعلام النظام بذلك ليتمكن من التفاعل مع هذا الحدث. 
على سبيل المثال، إذا تمت سرقة محفظتك، يمكنك أن تقول: "يا جماعة، أنا اتسرقت"، وهذا بمثابة إشعار. 
وبناءً عليه، أي شخص مهتم بهذا الحدث يمكنه اتخاذ إجراء بناءً على المعلومات المتاحة.

### [[Cs Delegates]]
 نوع من أنواع الكود يُستخدم لتحديد الوظائف التي ستُنفذ عندما يحدث الحدث. 
 يوفر Delegate وسيلة مرنة للإشارة إلى دالة معينة أو أكثر، مما يسهل التعامل مع الأحداث.

### [[Single Responsibility Principle]]

مبدأ المسؤولية الواحدة ينص على أن كل كلاس (Class) يجب أن يكون لديه سبب واحد فقط للتعديل. 
على سبيل المثال، إذا كان لديك كلاس مسؤول عن حساب الرواتب، فإن مهمته الوحيدة يجب أن تكون حساب الرواتب، وليس إرسال إيميلات أو تسجيل معلومات في السجلات. يمكننا استخدام الأحداث لتفويض هذه المسؤوليات.

```csharp
public void CalculateSalaries(List<Employee> employees, Func<Employee, bool> predicate)
{
    foreach (var employee in employees)
    {
        if (predicate(employee))
        {
            var salary = employee.BasicSalary + employee.Bonus - employee.Deductions;
            // هنا يجب ألا نقوم بعمليات أخرى مثل إرسال إيميل أو تسجيل لوج
            // We can use event
        }
    }
}
```

### How to declare Event

عند تعريف حدث في الكود، هناك خطوات معينة يجب اتباعها:

1. **إنشاء حدث**: يجب تحديد اسم الحدث ونوع البيانات التي سيتم تمريرها مع الحدث.
2. **تعريف الـ Event Handler**: هو الكود الذي سيتم تنفيذه عندما يحدث الحدث.

```csharp
// تعريف المندوب (Delegate)
public delegate void NameEventHandler(int para1, int para2);

// تعريف الحدث
public event NameEventHandler NameEvent;

// استدعاء (Trigger) الحدث
NameEvent(para1, para2); // أو
NameEvent.Invoke(para1, para2);

// Delegate ==> Null 
if (NameEvent != null)
{
    NameEvent.Invoke(para1, para2);
}

// أو استخدام Null Propagation
NameEvent?.Invoke(para1, para2);
```

### Event Members

- **الحدث (Event)**: هو الإشعار أو التنبيه.
- **معالج الحدث (Event Handler)**: هو الكود الذي ينتظر الحدث ليتم تنفيذه.
- **استدعاء الحدث (Trigger)**: هو عملية الإشعار نفسها.

### Full Example

استخدام الأحداث في تطبيق حساب الرواتب:

#### 1. تعريف الحدث

سنبدأ بتعريف حدث خاص بحساب الراتب.

```csharp
public class SalaryCalculator
{
    public delegate void SalaryCalculatedEventHandler(object sender, SalaryEventArgs e);
    public event SalaryCalculatedEventHandler SalaryCalculated;

    public void CalculateSalary(Employee employee)
    {
        // حساب الراتب
        decimal salary = employee.BaseSalary + employee.Bonus;
        
        // إشعار بأن الراتب قد تم حسابه
        OnSalaryCalculated(employee, salary);
    }

    protected virtual void OnSalaryCalculated(Employee employee, decimal salary)
    {
        SalaryCalculated?.Invoke(this, new SalaryEventArgs(employee, salary));
    }
}
```

#### 2. تعريف بيانات الحدث

```csharp
public class SalaryEventArgs : EventArgs
{
    public Employee Employee { get; }
    public decimal Salary { get; }

    public SalaryEventArgs(Employee employee, decimal salary)
    {
        Employee = employee;
        Salary = salary;
    }
}
```

#### 3. تعريف Event Handler

```csharp
public void OnSalaryCalculated(object sender, SalaryEventArgs e)
{
    Console.WriteLine($"راتب {e.Employee.Name} تم حسابه، والراتب هو {e.Salary}");
}
```

#### 4. الاستخدام في البرنامج الرئيسي

الآن سنجمع كل شيء معًا في البرنامج الرئيسي.

```csharp
class Program
{
    static void Main(string[] args)
    {
        SalaryCalculator calculator = new SalaryCalculator();
        calculator.SalaryCalculated += OnSalaryCalculated; // الاشتراك في الحدث

        // إنشاء موظف وهمي
        Employee employee = new Employee { Name = "أحمد", BaseSalary = 1000, Bonus = 200 };

        // حساب الراتب
        calculator.CalculateSalary(employee);
    }

    public static void OnSalaryCalculated(object sender, SalaryEventArgs e)
    {
        Console.WriteLine($"راتب {e.Employee.Name} تم حسابه، والراتب هو {e.Salary}");
    }
}
```

### الخلاصة

تعتبر أداة قوية جدًا لتنظيم الكود وتحسين أدائه في تطبيقات C#. 
عن طريق استخدام الأحداث، يمكنك تفويض المسؤوليات بوضوح، مما يسهل عليك إدارة وتطوير تطبيقاتك بشكل أكثر كفاءة.