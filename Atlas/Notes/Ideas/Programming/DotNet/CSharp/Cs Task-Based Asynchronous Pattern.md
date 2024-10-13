---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
---

نمط البرمجة غير المتزامنة المعروف باسم **Task-Based Asynchronous Pattern (TAP)** في لغة C#. 
هذا النمط يُستخدم لكتابة كود غير متزامن يسمح بتشغيل المهام بدون حجب (Blocking) للثريد الأساسي، وهو يعتمد بشكل رئيسي على الكلاسات الخاصة بـ Task في .NET Framework. نبدأ أولًا بشرح مفهومين مهمين، وهما:

- الـ**Synchronous**: وهو الكود الذي يتم تنفيذه بشكل متسلسل بحيث ينتظر كل سطر من الكود حتى ينتهي السطر الذي يسبقه قبل أن ينتقل للسطر التالي. يُطلق عليه أيضًا "Blocking Code" لأنه يُوقف التنفيذ حتى يتم الانتهاء من العملية.

- الـ**Asynchronous**: وهو الكود الذي يتم تنفيذه بدون انتظار السطور الأخرى حتى تكتمل. يُطلق عليه أيضًا "Non-Blocking Code"، حيث يمكن أن يبدأ تنفيذ سطر جديد بينما السطر الآخر لا يزال قيد التنفيذ.

### مفهوم Task
كلمة **Task** في C# تمثل عملية أو قطعة من الكود تُنفذ بشكل غير متزامن. 
تشبه مفهوم **Promise** في JavaScript أو **Future** في لغات أخرى مثل Java. 
يتم استخدام **Task** لتنفيذ عملية معينة في الخلفية (Background) دون التأثير على الثريد الأساسي. 
عندما تُنشئ **Task**، يُسمح للكود بمواصلة العمل بينما تنتظر المهمة الخلفية أن تُكمل عملها.

على سبيل المثال، في الدروس السابقة عن **Threading**، تم التعامل مع إنشاء وإدارة **Threads** بشكل مباشر، وهو ما كان معقدًا وصعبًا في بعض الأحيان. 
لكن مع **TAP**، يتم إخفاء التعقيدات المتعلقة بإدارة الـ **Thread** بواسطة **Thread Pool**.

### كيفية إنشاء Task
لإنشاء **Task**، يمكن استخدام دالة **Task.Run()** التي تأخذ دالة لتنفيذها بشكل غير متزامن:

```csharp
Task.Run(() => ProcessBatch1());
//       Delegate
```

### استخدام async و await
لتسهيل كتابة الكود غير المتزامن، توفر C# كلمتين رئيسيتين هما **async** و **await**. 
عند استخدام **async** مع الميثود، يتم الإشارة إلى أنها ستحتوي على عمليات غير متزامنة. 
و**await** يُستخدم لانتظار **Task** حتى تنتهي:

```csharp
public async Task ExampleMethod()
{
	// دي أصلًا بترجع تاسك 
	// عشان أستنى تاسك تخلص
    await Task.Delay(1000); // تنتظر 1000 مللي ثانية
    Console.WriteLine("Task completed");
}
```

- الـ async task خليتها زيها زي الـ void بالظبط مش لازم تعمل Return لحاجة
- الـ await قبلها حاجة وبعدها حاجة تانية خالص
  يعني الكود اللي قبلها بيتنفذ في نفس الـ Thread بتاع الـ Caller اللي هو ممكن يبقا Main
  إنما بعدها بيعمل Thread جديد
- يعني من الأخر بتعمل block للـ Thread بتاع التاسك وبيرجع للـ Caller ينفذ اللي فيه لحد ما الـ Await تخلص وبعدين يرجع يكمل بس في Thread مختلف
- أي Method هتستخدم فيها Await لازم ترجع  `async Task` وبلاش ترجع `async void` غير في حالة واحدة وهي الـ `EventHandler` اللي في الـ [[Cs Event]]
### الفرق بين Synchronous و Asynchronous
في **Synchronous Code**، يتم حجب (Blocking) الثريد الأساسي حتى تنتهي العملية. على سبيل المثال:

```csharp
Thread.Sleep(1000); // حجب الثريد لمدة 1000 مللي ثانية
Console.WriteLine("Completed");
```

في هذا المثال، لا يُمكن تنفيذ أي شيء آخر حتى ينتهي **Thread.Sleep()**. 
بينما في **Asynchronous Code**، يمكن بدء عدة مهام في وقت واحد:

```csharp
await Task.Delay(1000); // بدون حجب للثريد
Console.WriteLine("Task completed");
```

### استخدام CancellationToken لإلغاء المهام
عند العمل مع المهام، قد نحتاج إلى إلغائها في حالات معينة. يُستخدم **CancellationToken** لإرسال إشارة إلى المهام بأن يتم إيقافها.

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
await Task.Run(() => ProcessData(cts.Token), cts.Token);
```

عند استدعاء **cts.Cancel()**، سيتم إرسال إشارة إلى المهمة لإيقافها. هنا النقطة المهمة أن المهمة نفسها هي المسؤولة عن اتخاذ القرار بشأن متى وكيف يتم إيقافها، وليس الـ **CancellationToken**.

### التعامل مع Task Status
كل **Task** لها حالة (Status) يمكن التحقق منها باستخدام خاصية **Status**. الحالات الممكنة تشمل **WaitingToRun**، **Running**، و **Canceled**.

```csharp
if (task.Status == TaskStatus.RanToCompletion)
{
    Console.WriteLine("Task completed successfully.");
}
```

### استخدام Task.WhenAll و Task.WhenAny
إذا كان لديك عدة مهام تريد تشغيلها بالتوازي، يمكنك استخدام **Task.WhenAll()** لانتظار جميع المهام حتى تكتمل:

```csharp
await Task.WhenAll(task1, task2, task3);
```

أو يمكنك استخدام **Task.WhenAny()** لانتظار أول مهمة تكتمل من بين عدة مهام:

```csharp
await Task.WhenAny(task1, task2, task3);
```

### الخاتمة
نمط **Task-Based Asynchronous Pattern** يوفر طريقة أكثر سلاسة ومرونة لكتابة الكود غير المتزامن في C#، ويُغني عن التعقيدات المتعلقة بإدارة الثريدات. كما أنه يُعد جزءًا أساسيًا عند بناء تطبيقات تعتمد على العمليات الخلفية مثل خدمات الويب أو التطبيقات التي تحتاج إلى أداء عالٍ دون التأثير على تجربة المستخدم.

# More
### شرح TAP باستخدام Task.Run()

كيفية استخدام **Task.Run()** لتنفيذ العمليات بشكل غير متزامن. 
في المثال التالي، نرى كيف يتم تشغيل مهام متعددة بدون انتظار بعضها البعض (أي بدون حجب **Blocking** للثريد الأساسي):

```csharp
Task.Run(() => ProcessBatch1());
Task.Run(() => ProcessBatch2());
```

أن **Task.Run()** يُستخدم عادة لبدء مهمة في الخلفية، وأنه يمكن استخدامه في سيناريوهات متعددة، لكنه ليس الأسلوب الأكثر استخدامًا دائمًا، حيث توجد طرق أخرى سنشرحها لاحقًا.

### شرح Synchronous vs Asynchronous

الفرق بين **Synchronous** و **Asynchronous**. 
في البرمجة المتزامنة **Synchronous**، يتم تنفيذ الأسطر واحدًا تلو الآخر، وكل سطر ينتظر السطر الذي يسبقه لينتهي.
بينما في البرمجة غير المتزامنة **Asynchronous**، يمكن تنفيذ عدة أسطر معًا بدون انتظار.

في المثال التالي، يتم تنفيذ العمليات بشكل متزامن:

```csharp
Thread.Sleep(1000); // حجب الثريد لمدة 1000 مللي ثانية
Console.WriteLine("Completed");
```

بينما في المثال غير المتزامن، يتم استخدام **Task.Delay()** لتنفيذ التأخير بدون حجب الثريد:

```csharp
await Task.Delay(1000); // بدون حجب الثريد
Console.WriteLine("Task completed");
```

### التحويل إلى Task باستخدام async و await

لجعل الكود غير متزامن بشكل فعال، نستخدام **async** و **await** في كتابة الميثودات، وأوضح كيف يتم تحويل ميثود عادية إلى ميثود غير متزامنة. 
مثلًا، في هذا المثال:

```csharp
public async Task ExampleMethod()
{
    await Task.Delay(1000);
    Console.WriteLine("Task completed");
}
```

### توضيح باستخدام Breakpoints

مثلاً، عند تشغيل **Task.Run()** ووجود عدة مهام، يمكن رؤية أن المهام يتم تنفيذها في **Thread** منفصل لكل واحدة منها.

```csharp
Task.Run(() => ProcessBatch1()); // يتم تنفيذها في ثريد منفصل
Task.Run(() => ProcessBatch2()); // يتم تنفيذها في ثريد منفصل
```

في هذه الحالة، يتم تشغيل كل مهمة في ثريد منفصل عبر **Thread Pool**.

### استخدام CancellationToken داخل Task

ثم عاد المحاضر لشرح كيفية إلغاء المهام باستخدام **CancellationToken** داخل مهام **Task**. أضاف المحاضر فحصًا عند تنفيذ المهام للتحقق من حالة الإلغاء:

```csharp
CancellationTokenSource cts = new CancellationTokenSource();
await Task.Run(() => ProcessData(cts.Token), cts.Token);

if (cts.Token.IsCancellationRequested)
{
    Console.WriteLine("Task canceled.");
}
```

في هذه الحالة، إذا تم طلب الإلغاء عبر **cts.Cancel()**، سيتم إيقاف المهمة بناءً على التحقق من حالة الإلغاء داخل **Task**.

### تحسين الأداء باستخدام Task.WhenAll و Task.WhenAny

لتشغيل عدة مهام في نفس الوقت والانتظار حتى تنتهي جميعها، **Task.WhenAll()** التي تسمح بانتظار إتمام جميع المهام:

```csharp
await Task.WhenAll(task1, task2, task3); // انتظار جميع المهام
```

أو يمكن استخدام **Task.WhenAny()** لانتظار أول مهمة تنتهي:

```csharp
await Task.WhenAny(task1, task2, task3); // انتظار أول مهمة تنتهي
```

### توضيح استخدام async و await مع Delays

الـ **Task.Delay()** داخل الMethods لتوضيح كيف يتم تأخير المهام بدون حجب:

```csharp
await Task.Delay(100); // تأخير بسيط لإظهار الفارق في التنفيذ
```

هذا التأخير يسمح بملاحظة كيف يتم تنفيذ المهام بشكل غير متزامن دون تعطيل الثريد الأساسي.

### التعامل مع Task Completion Status

في النهاية، قدم المحاضر شرحًا حول كيفية فحص حالة المهام باستخدام **Task.Status** للتأكد مما إذا كانت المهمة قد اكتملت أو ألغيت أو لا تزال قيد التنفيذ:

```csharp
if (task.Status == TaskStatus.RanToCompletion)
{
    Console.WriteLine("Task completed successfully.");
}
else if (task.Status == TaskStatus.Canceled)
{
    Console.WriteLine("Task was canceled.");
}
```

### الخاتمة

كان الشرح يتمحور حول كيفية استخدام **Task-Based Asynchronous Pattern** (TAP) لكتابة كود غير متزامن بطريقة فعّالة في C#. تم توضيح كيفية استخدام **async** و **await**، وكيفية إدارة المهام باستخدام **Task.Run()** و **CancellationToken**. كما تم شرح كيفية التعامل مع المهام المتعددة باستخدام **Task.WhenAll** و **Task.WhenAny**.

باستخدام هذه الأساليب، يمكن كتابة كود أكثر كفاءة وسلاسة في التعامل مع العمليات الخلفية في التطبيقات التي تتطلب أداءً عاليًا.