
### إيه هو Enumerable؟
كلمة **Enumerable** معناها إنك بتتعامل مع أوبجكت تقدر تعد عليه. 
يعني أي حاجة تقدر تعمل عليها **for loop** أو **foreach loop**، زي المصفوفات (arrays) أو القوائم (lists). 
الحاجات دي كلها بنسميها **Enumerable**.

#### مثال:
لما يكون عندك مصفوفة أو قائمة، تقدر تعد عليها باستخدام **for loop**، زي ما بنعمل مع الـ **arrays** أو الـ **lists** في البرمجة.

### تحويل الأوبجكت لـ Enumerable
لو عندك أوبجكت وعايز تخليه **Enumerable** بحيث تقدر تعمل عليه **for loop**، لازم تعمل بعض الخطوات. 
غالبًا انت مش هتحتاج تعملها بيدك كتير، لأن في حاجات جاهزة في **.NET** بتخليك تقدر تستخدم الموضوع ده بسهولة، لكن الهدف إنك تفهم ازاي الدنيا شغالة في الخلفية.

### كود تحويل أوبجكت إلى Enumerable:
لو فرضنا إن عندك **class** اسمه `Employee` بيحتوي على معلومات عن الموظف، زي الراتب الأساسي والبدلات والتأمينات. 
وعايزين نخلّي الأوبجكت ده **Enumerable**، بمعنى إنه يبقى قابل للتعامل معاه في **foreach loop** عشان نعد كل بند من بنود الراتب.

#### الكود:
```csharp
public class Employee : IEnumerable<SalaryItem>
{
    private List<SalaryItem> salaryItems = new List<SalaryItem>();

    public void AddSalaryItem(SalaryItem item)
    {
        if (item != null)
        {
            salaryItems.Add(item);
        }
    }

    public IEnumerator<SalaryItem> GetEnumerator()
    {
        foreach (var item in salaryItems)
        {
            yield return item;
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
}

public class SalaryItem
{
    public string Name { get; set; }
    public double Value { get; set; }
}
```

### شرح الكود:

1. **Employee class**:
   - الكلاس `Employee` بيحتوي على **List** من **SalaryItem** اللي بتمثل بنود الراتب.
   - عندنا ميثود اسمها `AddSalaryItem` عشان نضيف بنود الراتب، ودي بناديها لما يكون عندك بند راتب جديد عايز تضيفه.
   - الميثود `GetEnumerator` هي اللي بتحول الـ `Employee` لـ **Enumerable** باستخدام **yield return**. بمعنى تقدر تستخدم **foreach** عشان تعد البنود اللي جوا الموظف.

2. **SalaryItem class**:
   - الكلاس ده بيمثل البند الواحد في الراتب، زي "بدل مواصلات" أو "بدل سكن"، وكل بند له اسم وقيمة.

### اليلد Statement:
الكلمة المفتاحية **yield** في C# هي اللي بتخلينا نعمل **custom enumerators**، ودي بتسهل علينا إننا نكتب كود بسيط بدل ما نكتب كل الكود اللي بيبني Enumerator من الصفر. 
مثلا، لما بنستخدم **yield return**، كل مرة بنعمل **foreach loop**، بنرجع عنصر من عناصر القائمة ونكمل الدورة.

#### مثال توضيحي:
```csharp
private IEnumerable<int> TestYield()
{
    yield return 1;
    yield return 2;
    yield return 3;
}
```

لما نعمل **foreach** على الدالة دي، هيتم طباعة الأرقام 1، 2، 3 بالتتابع، وده لأن **yield return** بيشتغل زي Enumerator جاهز بيعد علينا القيم اللي بنرجعها.

### الفرق بين Enumerator العادي و yield:
الـ **Enumerator** العادي بيتطلب إنك تبني كل حاجة بنفسك، زي تحديد العداد (index) والحالة اللي بتكون فيها دلوقتي في التعداد. لكن **yield** بيخليك تعمل ده بشكل تلقائي وسهل، من غير ما تكتب كل الكود ده بنفسك.

### مثال على العادي
خلينا نفترض إن عندنا **class** بيمثل مكتبة فيها مجموعة من الكتب، وعايزين نعمل **Enumerator** يسمح لنا بالتنقل بين الكتب واحد واحد.

#### الخطوات:
1. نبني كلاس **Library** اللي بيحتوي على مجموعة من الكتب.
2. نعمل **Enumerator** اللي بيتعامل مع عملية التنقل بين الكتب.

#### الكود:

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

public class Book
{
    public string Title { get; set; }

    public Book(string title)
    {
        Title = title;
    }
}

public class Library : IEnumerable
{
    private List<Book> books = new List<Book>();

    // إضافة كتاب جديد للمكتبة
    public void AddBook(Book book)
    {
        books.Add(book);
    }

    // هنا بنعمل Implement للـ GetEnumerator عشان نرجع الـ Enumerator
    public IEnumerator GetEnumerator()
    {
        return new LibraryEnumerator(books);
    }
}

public class LibraryEnumerator : IEnumerator
{
    private List<Book> _books;
    private int position = -1;  // الـ Position بيبدأ من -1 لأنه لسه مش على أول عنصر

    // Constructor بياخد القائمة اللي هي الكتب
    public LibraryEnumerator(List<Book> books)
    {
        _books = books;
    }

    // MoveNext() بتحرك المؤشر على الكتاب اللي بعده
    public bool MoveNext()
    {
        position++;
        return (position < _books.Count);
    }

    // Reset() بتعيد المؤشر للبداية
    public void Reset()
    {
        position = -1;
    }

    // Current بترجع الكتاب الحالي اللي واقف عليه المؤشر
    public object Current
    {
        get
        {
            if (position == -1 || position >= _books.Count)
            {
                throw new InvalidOperationException();
            }
            return _books[position];
        }
    }
}
```

#### شرح الكود:

1. **Library class**:
   - عندنا كلاس اسمه **Library**، واللي بيحتوي على قائمة من الكتب (`List<Book>`).
   - أضفنا ميثود `AddBook()` عشان نقدر نضيف كتب للمكتبة.
   - الكلاس ده بيطبق الـ **IEnumerable** عشان نقدر نعمل **foreach** عليه.
   - في الميثود `GetEnumerator()`، بنرجع كائن من نوع **LibraryEnumerator** اللي بنبنيه يدويًا.

2. **LibraryEnumerator class**:
   - هنا بنبني **Enumerator** من الصفر.  
   - الميثود `MoveNext()` بتحرك المؤشر للكتاب اللي بعده.
   - الميثود `Reset()` بترجع المؤشر للبداية، يعني كأننا بنقول للعداد "ابدأ من أول وجديد".
   - الميثود `Current` بترجع الكتاب اللي المؤشر واقف عليه دلوقتي.

#### استخدام الـ Enumerator:

```csharp
public class Program
{
    public static void Main()
    {
        Library library = new Library();
        library.AddBook(new Book("C# Programming"));
        library.AddBook(new Book("Design Patterns"));
        library.AddBook(new Book("Data Structures"));

        // استخدام الـ Enumerator العادي
        IEnumerator enumerator = library.GetEnumerator();

        while (enumerator.MoveNext())
        {
            Book currentBook = (Book)enumerator.Current;
            Console.WriteLine(currentBook.Title);
        }
    }
}
```

#### شرح الكود:
- في الكود ده، أنشأنا مكتبة جديدة وضفنا فيها 3 كتب.
- بعد كده، استخدمنا الـ **Enumerator** للتنقل بين الكتب باستخدام `MoveNext()` و `Current`.
- بنطبع اسم كل كتاب لما المؤشر يتحرك على العنصر اللي بعده.

#### النتيجة:
```
C# Programming
Design Patterns
Data Structures
```

### 