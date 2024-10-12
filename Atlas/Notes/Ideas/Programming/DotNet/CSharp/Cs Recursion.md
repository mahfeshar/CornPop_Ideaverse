---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-12
---
- We talked about [[Recursion]] before
- أكتر حاجة بتحتاج تفكر فيها هي إنك امتا توقف البرنامج
## Factorial Example
```cs
static int CalculateFactorial(int number)
{
    if (number <= 1)
        return number;
    return number * CalculateFactorial(number - 1);

	//OR
    //var factorial = 1;
    //for (var i = 1; i <= number; i++)
    //    factorial *= i;
    //return factorial;
}
```

## Hierarchical data
أكبر فائدة للـ Recursion تظهر عندما تكون هناك حاجة لمعالجة **البيانات المتداخلة** أو **الشجرية** (hierarchical data)، مثل:

- عندما يكون لديك **مجلد داخل مجلد داخل مجلد** إلى عدد غير معروف من المجلدات، حيث يتغير العمق بناءً على البنية الفعلية للنظام.
- على سبيل المثال، نظام الملفات في الكمبيوتر الذي يحتوي على مجلدات فرعية بداخل مجلدات أخرى، وقد تمتد هذه البنية بشكل عميق جدًا.  
    في مثل هذه الحالة، يكون Recursion مفيدًا جدًا لأنه يُعالج كل مستوى قبل الانتقال إلى المستوى الفرعي التالي بشكل ديناميكي دون الحاجة إلى معرفة عدد المستويات مسبقًا.

**باختصار**، الـ Recursion يسمح لك بالتعامل مع بنى معقدة ومتداخلة بطريقة بسيطة وواضحة، كما هو الحال في استعراض جميع الملفات والمجلدات الموجودة داخل مسار غير محدد العمق.

### Ex 1
```cs
class Program
{
    static void Main(string[] args)
    {PrintDirectoryContents(@"G:\PassionateCoders\CSharpAdvanced\CSharpAdvanced", 1);
    }

    static void PrintDirectoryContents(string dirPath, int level)
    {
        // طباعة جميع الملفات في المجلد الحالي
        foreach (var filePath in Directory.GetFiles(dirPath))
        {
            string fileName = new FileInfo(filePath).Name;
            Console.WriteLine($"{new string('-', level)} {fileName}");
        }

        // طباعة جميع المجلدات في المجلد الحالي
        foreach (var subDir in Directory.GetDirectories(dirPath))
        {
            string dirName = new DirectoryInfo(subDir).Name;
            Console.WriteLine($"{new string('-', level)} {dirName}");

            // استدعاء الدالة بشكل تكراري لاستعراض المجلدات الفرعية
            PrintDirectoryContents(subDir, level + 1);
        }
    }
}
```

### Ex 2
```cs
class Program
{
    static void Main(string[] args)
    {
        // استدعاء الدالة لحساب حجم المجلد
        long totalSize = CalculateDirectorySize(@"G:\Path\To\Directory");
        Console.WriteLine($"Total directory size: {totalSize} bytes");
    }

    // دالة لحساب حجم المجلد بما في ذلك الملفات والمجلدات الفرعية
    static long CalculateDirectorySize(string dirPath)
    {
        long size = 0;

        // حساب حجم جميع الملفات في المجلد الحالي
        foreach (var filePath in Directory.GetFiles(dirPath))
        {
            size += new FileInfo(filePath).Length;
        }

        // حساب حجم المجلدات الفرعية باستخدام التكرار الذاتي
        foreach (var subDir in Directory.GetDirectories(dirPath))
        {
            size += CalculateDirectorySize(subDir);
        }

        return size;
    }
}
```