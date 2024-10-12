---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
Link: https://www.youtube.com/watch?v=ri4T1PYLn0E&list=PLsV97AQt78NQYhO7NqlBTrJX_Nsk3SmyY&index=6
---

موضوع مهم وصعب شوية في البرمجة اسمه **Multithreading**، والموضوع ده يعتبر معقد جداً في البرمجة بشكل عام وفي .NET بشكل خاص. 
بس مش هنخش في التفاصيل دي كلها النهاردة لإن الطرق اللي هنتكلم عنها النهاردة ما حدش بقى بيستعملها تقريباً. 
دلوقتي، مايكروسوفت بقت عاملة طبقات فوق الطرق القديمة عشان تخلي الموضوع أسهل، وتقدر تتعامل مع **Multithreading** بشكل أبسط وأدق من الطرق القديمة.

طيب ليه بنتكلم عن الأساسيات لو الطرق دي قديمة؟ السبب هو إن لما نجي نتكلم عن الطرق الجديدة في **.NET**، لازم تكون فاهم الأساسيات اللي شغالة من تحت عشان تقدر تستوعب الجديد.

### يعني إيه ثريد (Thread)؟

أول حاجة لازم نعرف يعني إيه كلمة "Thread". الترجمة الحرفية ليها هي "خيط"، 
وفي نظام التشغيل **Thread** هي سلسلة من التعليمات اللي بتتنفذ ورا بعض.
يعني لو عندك برنامج، وكتبت فيه سطور كود تحت بعض، البرنامج بيشتغل خط ورا خط، وكل برنامج بيشتغل جوه حاجة اسمها **Process**. وأي **Process** بيبقى فيها حاجة اسمها **Main Thread**، اللي هو Thread الرئيسي اللي بينفذ كود البرنامج لما باجي أشغل أي Process.

### ليه بنحتاج Multithreading؟
دلوقتي، لو عندك عملية في البرنامج بتاخد وقت طويل في التنفيذ، والـUser مش عايز يستنى البرنامج لحد ما يخلص عشان يقدر يتعامل مع البرنامج تاني، هنا بتيجي فايدة الـ**Multithreading**. 
في الوضع الطبيعي بدون **Multithreading**، البرنامج بيهنج ويفضل واقف لحد ما العملية الطويلة تخلص. 
بس مع **Multithreading**، ممكن تفصل العملية الطويلة دي في **Thread** لوحده، وتشغل بقية البرنامج عادي جداً من غير ما اليوزر يحس بأي بطء.

### أمثلة على Multithreading

واحد من أشهر الأمثلة على **Multithreading** هو لما بتشوف برنامج فيه **Progress Bar**، زي لما تنزل ملف باستخدام **Download Manager**. 
هتلاقي الـUI شغال عادي جداً، وفي نفس الوقت عملية التحميل شغالة في الخلفية.
لو مفيش **Multithreading**، الـUI كان هيهنج لحد ما التحميل يخلص.
### مثال توضيحي
طيب، خلينا نوضح المثال البسيط اللي كان بيتكلم فيه المحاضر عن الطباعة باستخدام لونين مختلفين، وهنشوف الكود قبل وبعد استخدام **Multithreading**.

#### 1. **الطريقة التقليدية بدون Multithreading**:

في الطريقة دي، هنطبع الأرقام باللون الأحمر والأخضر بالتتابع باستخدام حلقتين واحدة ورا التانية:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        // طباعة الأرقام باللون الأحمر
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine($"Red: {i}");
        }

        // طباعة الأرقام باللون الأخضر
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine($"Green: {i}");
        }

        Console.ResetColor();
        Console.WriteLine("تمت الطباعة بالتتابع.");
    }
}
```



#### **شرح الطريقة**:
- في الكود ده، بنطبع الأرقام من 1 إلى 1000 مرتين: مرة باللون الأحمر، وبعد ما يخلص بنطبعهم باللون الأخضر.
- مفيش تزامن بين الطباعة، يعني لازم تخلص طباعة الأرقام باللون الأحمر الأول وبعدين يبدأ طباعة الأرقام باللون الأخضر.

#### 2. **الطريقة باستخدام Multithreading**:

دلوقتي هنشغل الطباعة باللونين الأحمر والأخضر في نفس الوقت باستخدام **Multithreading**:

```csharp
using System;
using System.Threading;

class Program
{
    static void Main(string[] args)
    {
        // إنشاء الـThreads للطباعة بالألوان المختلفة
        Thread thread1 = new Thread(PrintRed);
        Thread thread2 = new Thread(PrintGreen);

        // بدء تشغيل الـThreads
        thread1.Start();
        thread2.Start();

        // انتظار انتهاء الـThreads
        thread1.Join();
        thread2.Join();

        Console.ResetColor();
        Console.WriteLine("تمت الطباعة باستخدام Multithreading.");
    }

    static void PrintRed()
    {
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine($"Red: {i}");
            Thread.Sleep(10);  // تأخير بسيط عشان يظهر التداخل بين الألوان
        }
    }

    static void PrintGreen()
    {
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine($"Green: {i}");
            Thread.Sleep(10);  // تأخير بسيط عشان يظهر التداخل بين الألوان
        }
    }
}
```

#### **شرح الطريقة باستخدام Multithreading**:
- هنا بنستخدم **Thread** لكل عملية طباعة، واحد للطباعة باللون الأحمر والتاني للطباعة باللون الأخضر.
- كل **Thread** بيطبع الأرقام بشكل مستقل عن التاني، وده بيخلي الألوان تظهر كأنها بتطبع مع بعض.
- استخدمنا `Thread.Sleep(10)` عشان نضيف تأخير بسيط ونوضح التداخل بين الطباعة بالألوان المختلفة.

#### **الفرق بين الطريقتين**:
- في الطريقة التقليدية، الأرقام بتطبع بلون واحد في كل مرة، وما فيش تزامن.
- في الطريقة باستخدام **Multithreading**، الألوان بتتبدل بشكل متزامن، وده بيوضح فكرة التوازي في تنفيذ الأكواد.

### مثال عملي
أولاً هنشوف الطريقة التقليدية من غير **Multithreading** وبعد كده هنشوف الفرق لما نستخدم **Multithreading**.

#### 1. **الطريقة التقليدية بدون Multithreading**:

الكود ده بيحسب رواتب 5000 موظف في حلقة واحدة، وكل 1000 موظف بياخدوا وقت طويل شوية في الحساب:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        // حساب رواتب 5000 موظف
        for (int i = 1; i <= 5000; i++)
        {
            // عملية حساب معقدة (مثلاً)
            Console.WriteLine($"حساب مرتب الموظف رقم {i}");
            System.Threading.Thread.Sleep(100);  // بنعمل تأخير عشان نحاكي العملية اللي بتاخد وقت طويل
        }
        
        Console.WriteLine("تم حساب جميع الرواتب.");
    }
}
```

#### **شرح الطريقة**:
- الكود ده بيحسب مرتبات 5000 موظف في حلقة واحدة.
- `Thread.Sleep(100)` بتعمل تأخير لمدة 100 ملي ثانية لكل موظف عشان نحاكي عملية حساب المرتب اللي بتاخد وقت.
- البرنامج هيحسب الرواتب واحد واحد، وهيستنى لحد ما كل موظف يتحسب قبل ما ينتقل للموظف اللي بعده.

#### 2. **الطريقة باستخدام Multithreading**:

دلوقتي هنقسم الموظفين على 5 **Threads**، وكل **Thread** هيحسب رواتب 1000 موظف في نفس الوقت.

```csharp
using System;
using System.Threading;

class Program
{
    static void Main(string[] args)
    {
        // تقسيم الموظفين على 5 Threads
        Thread thread1 = new Thread(() => CalculateSalaries(1, 1000));
        Thread thread2 = new Thread(() => CalculateSalaries(1001, 2000));
        Thread thread3 = new Thread(() => CalculateSalaries(2001, 3000));
        Thread thread4 = new Thread(() => CalculateSalaries(3001, 4000));
        Thread thread5 = new Thread(() => CalculateSalaries(4001, 5000));

        // تشغيل الـThreads
        thread1.Start();
        thread2.Start();
        thread3.Start();
        thread4.Start();
        thread5.Start();

        // انتظار انتهاء جميع الـThreads
        thread1.Join();
        thread2.Join();
        thread3.Join();
        thread4.Join();
        thread5.Join();

        Console.WriteLine("تم حساب جميع الرواتب.");
    }

    static void CalculateSalaries(int start, int end)
    {
        for (int i = start; i <= end; i++)
        {
            // عملية حساب معقدة (مثلاً)
            Console.WriteLine($"حساب مرتب الموظف رقم {i}");
            Thread.Sleep(100);  // بنعمل تأخير عشان نحاكي العملية اللي بتاخد وقت طويل
        }
    }
}
```

#### **شرح الطريقة باستخدام Multithreading**:
- قسمنا الـ5000 موظف على 5 مجموعات (كل مجموعة 1000 موظف).
- لكل مجموعة عملنا **Thread** جديد، وكل **Thread** بيحسب الرواتب بتاعته في نفس الوقت مع الباقي.
- `Thread.Start()` بتبدأ تشغيل كل **Thread**.
- `Thread.Join()` بتستنى لحد ما كل **Thread** يخلص شغله قبل ما يكمل البرنامج.
  
#### **الفرق بين الطريقتين**:
- في الطريقة الأولى (بدون **Multithreading**)، البرنامج هيحسب الرواتب واحد ورا التاني، وده ممكن ياخد 50 دقيقة لو كل 1000 موظف بياخدوا 10 دقايق.
- في الطريقة التانية (بـ **Multithreading**)، كل مجموعة من الموظفين هتتحسب في نفس الوقت، وده هيقلل الزمن المطلوب لـ 10-15 دقيقة تقريباً، لإن كل **Thread** شغال بشكل متوازي مع التاني.

بكده نكون شفنا إزاي استخدام **Multithreading** بيحسن الأداء ويقلل الوقت المستهلك في العمليات اللي بتاخد وقت طويل زي حساب الرواتب.
### Concurrency و Context Switching
نقطة مهمة لازم نفهمها إن الـ**Threads** مش بتشتغل مع بعض في نفس اللحظة، لكنها بتشتغل بطريقة **Concurrency**، يعني نظام التشغيل بيبدل بينهم بسرعة كبيرة جداً لدرجة إنك بتحس إنهم بيشتغلوا مع بعض(بس فعليًا مبيتنفذوش مع بعض). 
دي العملية اللي اسمها **Context Switching**، اللي بتحصل في الـOperating System عشان ينفذ الـThreads بتاعتك.

### التعامل مع Static Resources و Lock

لما تشتغل على **Multithreading**، لازم تاخد بالك كويس جداً من الحاجات الـ**Static** في الكود، زي المتغيرات أو الـObjects اللي بيتم مشاركتها بين الـThreads. 
لإن ممكن يحصل تصرف غير متوقع لو اتنين **Threads** حاولوا يستخدموا نفس الـStatic Resource في نفس الوقت. 
عشان كده، بنستخدم حاجة اسمها **Locks** عشان نضمن إن مفيش **Thread** يدخل على الكود بتاعنا غير لما التاني يخلص.

 الـ **Locks** عشان نضمن إن مفيش مشاكل تحصل لما أكتر من **Thread** يدخلوا على نفس المتغير أو الـ**Resource** في نفس الوقت.

#### المشكلة قبل استخدام الـLocks

لو عندنا كود زي ده، هنلاحظ إن فيه احتمال يحصل مشاكل لما اتنين **Threads** يحاولوا يغيروا نفس الـStatic Resource (زي لون الـConsole) في نفس الوقت:

```csharp
using System;
using System.Threading;

class Program
{
    static void Main(string[] args)
    {
        // إنشاء Thread للطباعة بالأحمر وThread للطباعة بالأخضر
        Thread thread1 = new Thread(PrintRed);
        Thread thread2 = new Thread(PrintGreen);

        // بدء تشغيل الـThreads
        thread1.Start();
        thread2.Start();

        // انتظار انتهاء الـThreads
        thread1.Join();
        thread2.Join();

        Console.ResetColor();
        Console.WriteLine("تمت الطباعة.");
    }

    static void PrintRed()
    {
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Red;  // تغيير اللون للأحمر
            Console.WriteLine($"Red: {i}");
        }
    }

    static void PrintGreen()
    {
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Green;  // تغيير اللون للأخضر
            Console.WriteLine($"Green: {i}");
        }
    }
}
```

#### **المشكلة هنا**:
- الـ`Console.ForegroundColor` هو مورد مشترك بين الـThreads، بمعنى إن ممكن يحصل تداخل في الألوان لو الـThread الأول شغال وبيغير اللون للأحمر، وفي نفس الوقت الـThread التاني شغال وبيغير اللون للأخضر.
- النتيجة هتكون إن الألوان هتظهر بشكل غير متوقع، وممكن الـThread التاني يكتب بالألوان اللي المفروض الـThread الأول يستخدمها والعكس صحيح.

#### الحل باستخدام الـLocks

عشان نحل المشكلة دي، بنستخدم حاجة اسمها **Lock**. 
الـLock بتعمل زي "قفل" على الكود، بمعنى إن لما **Thread** معين يدخل على الكود المحمي بالـLock، مفيش **Thread** تاني يقدر يدخل عليه لحد ما الأول يخلص:

```csharp
using System;
using System.Threading;

class Program
{
    // كائن للقفل (Lock) على الكود المشترك
    private static readonly object lockObject = new object();

    static void Main(string[] args)
    {
        // إنشاء Thread للطباعة بالأحمر وThread للطباعة بالأخضر
        Thread thread1 = new Thread(PrintRed);
        Thread thread2 = new Thread(PrintGreen);

        // بدء تشغيل الـThreads
        thread1.Start();
        thread2.Start();

        // انتظار انتهاء الـThreads
        thread1.Join();
        thread2.Join();

        Console.ResetColor();
        Console.WriteLine("تمت الطباعة باستخدام Locks.");
    }

    static void PrintRed()
    {
        for (int i = 1; i <= 1000; i++)
        {
            // استخدام القفل (Lock) لتأمين الكود
            lock (lockObject)
            {
                Console.ForegroundColor = ConsoleColor.Red;  // تغيير اللون للأحمر
                Console.WriteLine($"Red: {i}");
            }
        }
    }

    static void PrintGreen()
    {
        for (int i = 1; i <= 1000; i++)
        {
            // استخدام القفل (Lock) لتأمين الكود
            lock (lockObject)
            {
                Console.ForegroundColor = ConsoleColor.Green;  // تغيير اللون للأخضر
                Console.WriteLine($"Green: {i}");
            }
        }
    }
}
```

#### **شرح الحل**:
- استخدمنا `lock` على كائن ثابت اسمه `lockObject`. الكائن ده بيعمل "قفل" على الكود الموجود جوه الـ`lock` statement.
- لما **Thread** يدخل على الكود المحمي بالـLock، **Thread** تاني مش هيقدر يدخل لحد ما الأول يخلص. لأن هو عبارة عن Variable وبيتم استعماله حاليًا فمقدرش أروح أستخدمه في حتة تانية لحد ما يخلص اللي بيعمهل دلوقتي
- هنا لما **Thread** الأول يغير لون الـConsole للأحمر، الـThread التاني مش هيقدر يغير اللون للأخضر غير لما الأول يخلص.

#### **النتيجة**:
- الألوان هتظهر بالشكل الصحيح، وكل **Thread** هيطبع بالألوان الخاصة بيه بدون تداخل.
- الحل ده بيساعد على تجنب التصرفات الغير متوقعة اللي ممكن تحصل لما أكتر من **Thread** يحاولوا يغيروا نفس الـResource في نفس الوقت.



### Thread Priority

في **Multithreading**، كل **Thread** بيشتغل حسب الأولوية اللي بنحددها له. 
الأولوية دي بتقول لنظام التشغيل أي **Thread** له الأفضلية في التنفيذ لو فيه أكتر من **Thread** بيحاولوا ينفذوا في نفس الوقت. 
لو **Thread** معين ليه أولوية أعلى، نظام التشغيل بيدي له الأفضلية في الحصول على موارد الـCPU، وده معناه إنه ممكن ينفذ أسرع من الـThreads اللي أولوياتها أقل.

زمان كان فيه اعتقاد إنك لو خليت نافذة النسخ (copy window) في ويندوز هي اللي (active)، هينسخ الملفات أسرع. والسبب إن النافذة اللي "active" بتاخد أولوية أعلى في التنفيذ.

#### الكود اللي بيشرح Priority:

```csharp
using System;
using System.Threading;

class Program
{
    static void Main(string[] args)
    {
        // إنشاء Thread للطباعة بالأحمر وThread للطباعة بالأخضر
        Thread thread1 = new Thread(PrintRed);
        Thread thread2 = new Thread(PrintGreen);

        // تحديد الأولويات
        thread1.Priority = ThreadPriority.Highest;  // أعلى أولوية
        thread2.Priority = ThreadPriority.Lowest;   // أقل أولوية

        // بدء تشغيل الـThreads
        thread1.Start();
        thread2.Start();

        // انتظار انتهاء الـThreads
        thread1.Join();
        thread2.Join();

        Console.ResetColor();
        Console.WriteLine("تمت الطباعة باستخدام أولوية Threads مختلفة.");
    }

    static void PrintRed()
    {
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine($"Red: {i}");
            Thread.Sleep(10);  // تأخير بسيط لتوضيح الفرق
        }
    }

    static void PrintGreen()
    {
        for (int i = 1; i <= 1000; i++)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine($"Green: {i}");
            Thread.Sleep(10);  // تأخير بسيط لتوضيح الفرق
        }
    }
}
```

#### **شرح الكود**:
- هنا بنعمل **Thread** للطباعة بالأحمر وواحد للطباعة بالأخضر.
- لكل **Thread** بنحدد أولوية باستخدام `Priority`. في الكود:
  - `thread1.Priority = ThreadPriority.Highest`: بنحدد أعلى أولوية للطباعة باللون الأحمر.
  - `thread2.Priority = ThreadPriority.Lowest`: بنحدد أقل أولوية للطباعة باللون الأخضر.
  
- لما نبدأ تشغيل الـThreads، نظام التشغيل هيعطي أولوية للـThread اللي بيطبع بالأحمر لأنه ليه أعلى **Priority**. بالتالي، هيتنفذ أكتر وبسرعة أعلى مقارنة بالـThread اللي بيطبع بالأخضر.

#### **النتيجة**:
- هتلاحظ في نتيجة الطباعة إن الأحمر بيظهر أكتر لأنه ليه أولوية أعلى، وبالتالي بيحصل على موارد الـCPU أكتر من الأخضر اللي ليه أولوية أقل.
- الفرق في الأولويات ممكن يظهر بشكل أوضح على الأجهزة الأبطأ أو في الحالات اللي فيها عمليات أكتر بتنافس على موارد الجهاز.
- الأولوية مش دايماً هتضمن إن الـThread اللي ليه أولوية أعلى هينفذ قبل التاني 100%، لأن الموضوع بيعتمد على عوامل تانية زي الحالة العامة للنظام والموارد المتاحة. 
- بس بشكل عام، الـThread اللي ليه أولوية أعلى هيحصل على فرصة أكبر في التنفيذ مقارنة باللي ليه أولوية أقل.


### Foreground و Background Threads

فيه نوعين من الـ**Threads**: وهما **Foreground Thread** و**Background Thread**. 
الـ**Foreground Thread** هو اللي بيمنع البرنامج إنه يقفل لحد ما يخلص. 
يعني مثلاً لو عندك **Foreground Thread** شغال، البرنامج مش هيقفل لحد ما الثريد ده يخلص. 
أما **Background Thread**، فالبرنامج ممكن يقفل حتى لو الثريد ده لسه شغال.

### Thread Pool

فيه طريقة تانية كمان لإنشاء **Threads** اسمها **Thread Pool**. دي طريقة أفضل لإنشاء وإدارة الـ**Threads**، بحيث إنها تعيد استخدام الـ**Threads** بدل ما تنشئ **Thread** جديدة كل مرة. وده بيخلي أداء البرنامج أحسن لإنه بيقلل استهلاك الموارد.

### مهم

الـ**Multithreading** مش بيزود سرعة البرنامج، لكنه بيخلي البرنامج أكتر استجابة. 
يعني بدل ما الـUser يحس إن البرنامج هنج لما يدوس على زرار، بيقدر يتعامل معاه عادي والعمليات الطويلة شغالة في الخلفية. 
بس خد بالك، استخدام عدد كبير من الـ**Threads** ممكن يقلل أداء البرنامج بسبب الـ**Context Switching** اللي بيحصل بين الـ**Threads**.

في النهاية، لازم تفهم الأساسيات دي عشان لما تدخل في المواضيع المتقدمة زي **TPL** أو **Task Library**، تكون عارف إيه اللي بيحصل تحت الغطاء.

