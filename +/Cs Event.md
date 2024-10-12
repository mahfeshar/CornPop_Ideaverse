---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
---
## Events in C#

تعتبر من المفاهيم المهمة جدًا، وخصوصًا لو كنت شغال على تطبيقات متقدمة. 

### What's Event?

الـ Events هي عبارة عن إشعارات أو تنبيهات بتظهر لما يحصل حاجة مهمة في البرنامج. بمعنى تاني، لو حصل حدث معين في الكود، النظام هيبلغك عشان تقدر تتفاعل معاه. 
مثلاً، لو محفظتك اتسرقت، تقدر تقول "يا جماعة، أنا اتسرقت" كنوع من الإشعار.
وبناءًا عليها أي حد مهتم بالحدث دا بيتصرف على أساسه

### Delegates
اتكلمنا عنه قبل كدا [[Cs Delegates]]
هنا هنستخدمه عشان نحدد الحاجة اللي هتتنفذ لما الـ Event يحصل

### [[Single Responsibility Principle]]
مبدأ المسؤولية الواحدة يعني إن كل كلاس (Class) في الكود لازم يكون عنده سبب واحد بس عشان يتعدل. 
يعني، مثلاً، لو عندك كلاس خاص بحساب الرواتب، مهمته الوحيدة تكون حساب الرواتب، مش إنه يبعت إيميلات أو يسجل لوجات.

```cs
public void CalculateSalaries(List<Emploee> employees, ShouldCalculate predicate)
{
	foreach(var employee in employees)
	{
		if (predocate(employee))
		{
			var salary = employee.BasicSalary + employee.Bonus - employee.Deductions;
			// Send Email
			// Send SMS
			// We can't make log or smth like that
			// only one responsible
			// But we can make event
		}
	}
}
```
### Declare Event

لما تحب تعرف حدث في الكود، بتعمله بالشكل التالي:

1. **إنشاء حدث**: لازم تحدد اسم الحدث ونوع البيانات اللي هيتبعت معاه.
2. **تعريف الـ Event Handler**: ده الكود اللي هيتنفذ لما الحدث يحصل.

```cs
// Event Handler (Deleget)
public delegate void NameEventHandler(int para1, int para2);

// Event
public event NameEventHandler NameEvent;

// Invoke (Fire)
NameEvent(para1, para2);
// OR
NameEvent.Invoke(para1, para2);
// We should handel if deleget not pointing to any method
if (NameEvent is not null)
{
	NameEvent.Invoke(para1, para2);
}
// OR
NameEvent?.Invoke(para1, para2)
```
- الـ Event: هو إشعار أو تنبية
- الـ Event handler: الكود اللي بيسمع ويستنى الإيفينت يدي الإشعار عشان **ينفذ حاجة**
- الـ Trigger  (Raise - Fire) Event: عملية الإشعار نفسها

مثال على ذلك:
```csharp
public class SalaryCalculator
{
    public delegate void SalaryCalculatedEventHandler(object sender, SalaryEventArgs e);
    public event SalaryCalculatedEventHandler SalaryCalculated;

    public void CalculateSalary(Employee employee)
    {
        // حساب الراتب
        decimal salary = employee.BaseSalary + employee.Bonus;
        
        // إشعار إن الراتب اتحسب
        OnSalaryCalculated(employee, salary);
    }

    protected virtual void OnSalaryCalculated(Employee employee, decimal salary)
    {
        SalaryCalculated?.Invoke(this, new SalaryEventArgs(employee, salary));
    }
}
```
استخدمنا الـ [[Cs Null#Null Propagation (Conditional) Operator|Null Propagation]]
### كيف نتعامل مع الأحداث

عند التعامل مع الأحداث، بنستخدم حاجة اسمها "Event Handlers". الـ Event Handler هو الوظيفة اللي هتشتغل لما الحدث يحصل. مثلاً، ممكن يكون عندك Event Handler بيبعت إيميل للموظف بعد حساب راتبه.

#### مثال على الـ Event Handler:

```csharp
public void OnSalaryCalculated(object sender, SalaryEventArgs e)
{
    Console.WriteLine($"راتب {e.Employee.Name} اتحسب، والراتب هو {e.Salary}");
}
```

### أهمية الأحداث

الأحداث بتساعدنا في فصل الكود بطريقة أفضل، لأن الكلاسات تركز على مهامها المحددة فقط. لو عايز تضيف سلوك جديد، كل اللي عليك تعمله هو إضافة Event Handler جديد بدل ما تعدل في الكود الأساسي.

### خلاصة

الأحداث في C# هي وسيلة قوية للتفاعل مع الأحداث المهمة في التطبيق. بفهمك لمفهوم المندوبين ومبدأ المسؤولية الواحدة، هتقدر تنشئ أحداث تتفاعل مع وظائف متعددة، وتضيف سلوكيات جديدة بشكل بسيط وسهل. لو عندك أي أسئلة أو محتاج تفاصيل أكتر، ما تترددش في السؤال!