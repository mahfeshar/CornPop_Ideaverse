---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-13
---

- شوفنا في ال [[CSharp String]] اننا لما بنيجي نعمل concatenate أو نزود أي حاجة في ال string هتعمل حرفيًا string جديدة كليًا ودا بيأثر على الأداء والميموري ودا لأن ال string عبارة عن [[Mutable vs Immutable#Immutable Objects|Immutable]]
- الحل كان إننا نستخدم class من نوع `StringBuilder`

## StringBuilder
1. **Initialization**: Create a `StringBuilder` instance.

   ```csharp
   StringBuilder sb = new StringBuilder();
   ```

2. **Appending Strings**: Use `Append()` to add strings.

   ```csharp
   sb.Append("Hello");
   sb.Append(" ");
   sb.Append("World");
   ```

3. **Inserting and Modifying**: Use `Insert()` for inserting and `Replace()` for replacing.

   ```csharp
   sb.Insert(6, "beautiful "); // inde
   sb.Replace("World", "Universe");
   ```

4. **Removing**: Remove characters with `Remove()`.

   ```csharp
   sb.Remove(6, 10); //start index, length
   ```

5. **Getting the Result**: Convert to string using `ToString()`.

   ```csharp
   string result = sb.ToString();
   ```

6. **Clearing**: Clear the `StringBuilder`.

   ```csharp
   sb.Clear();
   ```

### Example

```csharp
using System;
using System.Text;

class Program
{
    static void Main()
    {
        StringBuilder sb = new StringBuilder();
        
        sb.Append("Hello");
        sb.Append(" ");
        sb.Append("World");
        sb.Append("!");
        
        Console.WriteLine(sb.ToString()); // Output: Hello World!
        
        sb.Insert(6, "beautiful ");
        sb.Replace("World", "Universe");
        Console.WriteLine(sb.ToString()); 
        // Output: Hello beautiful Universe
        
        sb.Remove(6, 10);
        Console.WriteLine(sb.ToString()); // Output: Hello Universe
        
        sb.Clear();
        Console.WriteLine(sb.ToString()); // Output: ""
    }
}
```

## ايه اللي يفرقها عن ال String
عندنا اتنين Strategies:
### Array Reallocation and Doubling
- بكل بساطة إن لما ال Array بتتملى بيروح يعمل array جديدة 
	- (بتبقا ضعف ال capacity بتاع القديمة) وشرحنا ليه في [[Amortized analysis]]
- بينقل كل الداتا من القديمة للجديدة وبعدين يزود الداتا الجديدة
- نفس فكرة ال [[Array#Dynamic Arrays|Dynamic Arrays]] في أغلب لغات البرمجة

### Linked List of Small Arrays
في النسخة الجديدة، غيروا بدل ما بنستخدم array واحدة بيبقا حجمها كبير بنعمل شوية arrays صغيرة ونربطهم سوا ب Linked list
- أول ما ال Array تتملى، بتتعمل Array جديدة small وتتحط في آخر ال List
- دا بيحللي مشكلة إني أحتاج مساحة كبيرة ورا بعض في الميموري عشان أخزن فيها Array واحدة فبيحسن ال memory