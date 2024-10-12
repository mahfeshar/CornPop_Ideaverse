---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
---
- معناها التفويض (إني بفوض حد عشان يعملي حاجة معينة)
- من المفاهيم الأساسية والمهمة التي سيكون لها استخدام واسع في المشاريع المستقبلية. 
- **الـ Delegates** تعتبر كـ "مرجع أو مؤشر على دالة" (Method Reference or Pointer)، بمعنى أنك تستطيع استدعاء دالة دون الحاجة إلى معرفة اسمها أو مكان وجودها، فقط ما تحتاجه هو "signature" الخاص بها (عدد البرامترات ونوع البيانات).

## Example: Calculator
### المشكلة:
عندنا دالة تقوم بأربع عمليات رياضية أساسية: **الجمع، الطرح، الضرب، والقسمة**. 
يتم تنفيذ هذه العمليات باستخدام جمل **if-else** لتحديد العملية بناءً على رمز العملية الذي يتم تمريره كمدخل. 
ومع ذلك، هذه الطريقة بها مشكلة كبيرة، وهي أنه إذا أردت إضافة عملية جديدة مثل "باقي القسمة" (modulus) ستحتاج إلى تعديل الكود وإضافة جملة **if** جديدة. 
هذا يجعل الدالة غير مرنة وتتطلب تعديلًا مستمرًا في كل مرة تحتاج فيها إلى إضافة أو تغيير عملية.
وأيضا مشكلة إن مينفعش تكتر من الـ **else if**.

```cs
static void Main(string[] args)
{
    int num1 = 10;
    int num2 = 2;
    Calculator(num1, num2, '+'); // 12
	Calculator(num1, num2, '-'); // 8
	Calculator(num1, num2, '*'); // 20
	Calculator(num1, num2, '/'); // 5
	//Calculator(num1, num2, '%');
}

static void Calculator(int a, int b, char op)
{
    int result = 0;
    if (op == '+')
        result = a + b;
    else if (op == '-')
        result = a - b;
    else if (op == '*')
        result = a * b;
    else if (op == '/')
        result = a / b;
    else 
        throw new ArgumentException("Invalid Operator");

    Console.WriteLine(result);
}
```
### حل المشكلة باستخدام Delegates:
لتجاوز هذه المشكلة، يتم تقديم **الـ Delegates** كحل يجعل الدالة أكثر مرونة. 
بدلاً من الاعتماد على جمل **if-else** المعقدة، يمكن استخدام **Delegate** ليكون بمثابة وسيط يمكنه تنفيذ أي عملية رياضية تُرسل إليه. 
يمكن للـ Delegate قبول أي عملية حسابية (الجمع، الطرح، الضرب، إلخ) دون الحاجة إلى تعديل الكود الأساسي للدالة.

في المثال، تم تعريف **Delegate** اسمه `CalculateDelegate` يأخذ عددين كمدخلات وينفذ العملية بناءً على الدالة المرتبطة به. 
ثم تم استبدال جمل **if-else** بالدالة، وبدلاً من التعامل مع رمز العملية، يتم تمرير العملية نفسها كدالة (مثل `Add` أو `Subtract`).

```csharp
public delegate int CalculateDelegate(int num1, int num2);

CalculateDelegate del = Add;
int result = del(10, 20);
Console.WriteLine(result);

public static int Add(int a, int b)
{
	return a + b;
}
```

- اللي فوق دا الإستخدام بتاعها والتعريف بتاعها هي بالظبط زي الـ Method signature وبتحدد كل حاجة أكن دا اللي هيتم استخدامه في العادي
- ممكن تخليها تشاور على أي Method ومنها تقدر تباصي الـ Parameter ليها
- لازم الـ Method والـ Delegate يبقوا متفقين في **الـ Return Type ونوع وعدد الـ Parameters**

- ممكن نستخدمها كـ parameter لـ Function تانية وتستخدمها جواها عشان فكرة التعدد واني أقدر استخدمه بطرق مختلفة
```cs
public delegate int CalculatorDelegate(int a, int b);

static void Main(string[] args)
{
    int num1 = 10;
    int num2 = 2;
    Calculator(num1, num2, Add); // 12
    Calculator(num1, num2, Sub); // 8
    Calculator(num1, num2, Mul); // 20
    Calculator(num1, num2, Div); // 5
    //Calculator(num1, num2, '%');
}

static void Calculator(int a, int b, CalculatorDelegate dlg)
{
    int result = 0;
    result = dlg(a, b);
    Console.WriteLine(result);
}
public static int Add(int a, int b)
    { return a + b; }

public static int Sub(int a, int b)
    { return a - b; }

public static int Mul(int a, int b)
    { return a * b; }

public static int Div(int a, int b)
    { return a / b; }
```
- خد بالك من حاجة إن الـ method اللي بتستخدمها مش بتنادي عليها أو بتعملها Invocation إنما بتكتب بس إسمها وبتخليه يشاور عليها
### ميزة الـ Multicasting في Delegates:
هناك ميزة متقدمة تسمى **Multicasting**، وهي القدرة على إسناد أكثر من دالة لنفس الـ **Delegate**. 
يعني هذا أنك تستطيع ربط عدة عمليات بالـ Delegate نفسه، وعند استدعائه، سيتم تنفيذ كل هذه العمليات بالتتابع.

**مثال:** يتم إضافة عمليتي الجمع والطرح لنفس الـ **Delegate**، وعند استدعائه، **يقوم بتنفيذ العمليتين على التوالي**:

```csharp
CalculateDelegate del = Add;
del += Subtract;

int result = del(10, 5); // سيتم تنفيذ الجمع والطرح معًا
// هينفذ اللي في الفانكشن الأولى كله وبعدين ينادي على اللي في الفانكشن التانية كله

del -= Subtract;
```
- خد بالك إنك لو طرحت كله هيديك *Null Reference Exception* يعني مفيش قيمة فيه

### استخدام Lambda Expressions مع Delegates:
كيفية تبسيط الكود باستخدام **[[Lambda Expressions]]**. 
الـ Lambda هي طريقة مختصرة لتعريف الـ Delegates، حيث يتم الاستغناء عن كلمة `delegate` التقليدية واستخدام صيغة أبسط وأسرع. 
هذا الأسلوب يجعل الكود أقصر وأكثر قابلية للفهم.

```csharp
CalculateDelegate del = (x, y) => x + y;
int result = del(10, 20); // يقوم بجمع الرقمين

// ==================
int num1 = 10;
int num2 = 2;
CalculatorDelegate dlg = Add;
Calculator(num1, num2, dlg); // 12
// Anonymous delegate
Calculator(num1, num2, delegate (int a, int b) { return a - b; }); // 8
// Lambda Expression 
// => Big arrow
Calculator(num1, num2, (int a, int b) => a * b); // 20
// BEST (LAMBDA)
Calculator(num1, num2, (a, b) => a / b); // 5
// We can extend and add easily
Calculator(num1, num2, (a , b) => a % b); // 0
```

### مثال عملي على استخدام Delegates:
يتم إنشاء قائمة من الموظفين تحتوي على معلومات مثل الراتب الأساسي والخصومات والمكافآت. الهدف هو استخدام **Delegate** لحساب الرواتب بناءً على شروط معينة.

على سبيل المثال، يتم حساب رواتب الموظفين الذين يقل راتبهم الأساسي عن 2000 جنيه باستخدام **Delegate** يقوم بتحديد الموظفين الذين يلبون هذا الشرط:

```csharp
public delegate bool EmployeeCondition(Employee emp);

void PrintSalaries(List<Employee> employees, EmployeeCondition condition) {
    foreach (var emp in employees) {
        if (condition(emp)) {
            Console.WriteLine($"{emp.Name}: {emp.Salary}");
        }
    }
}

// استدعاء الدالة مع شرط أن يكون الراتب الأساسي أقل من 2000
PrintSalaries(employees, emp => emp.BasicSalary < 2000);
```

هذا الأسلوب يوضح كيف يمكن للـ Delegates أن تمنح مرونة عالية في بناء دوال عامة غير مرتبطة بشروط محددة، مما يجعل الكود أكثر نظافة وأقل تعقيدًا.

### الفائدة من Delegates:
الفوائد لاستخدام **Delegates**:
1. **المرونة**: القدرة على تعديل أو إضافة عمليات جديدة دون الحاجة إلى تغيير الكود الأساسي.
2. **الوضوح**: تقليل التعقيد الناتج عن جمل **if-else** الكثيرة.
3. **إعادة الاستخدام**: يمكن استخدام نفس الـ Delegate في سياقات متعددة وداخل مشاريع مختلفة.
4. **التوسيع**: يمكن بسهولة إضافة ميزات أو عمليات جديدة بدون الحاجة لتعديل الكود بشكل متكرر.