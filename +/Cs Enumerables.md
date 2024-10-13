
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

### الخلاصة:
في الفيديو، الفكرة الأساسية هي إنك ازاي تخلي أي **object** في C# يكون **Enumerable** باستخدام الكلمة المفتاحية **yield**. ده بيساعدنا في كتابة كود بسيط وفعال لعمل **loops** على أي بيانات جوه الأوبجكت، سواء كانت مصفوفات، قوائم، أو حتى كائنات خاصة.

---

بكده نكون شرحنا الموضوع ببساطة وباستخدام الأسلوب العامي، مع شرح الكود اللي اتقال في الفيديو. لو في أي حاجة مش واضحة، ممكن ترجع تشوف الفيديو تاني وإن شاء الله هيكون الموضوع أسهل.