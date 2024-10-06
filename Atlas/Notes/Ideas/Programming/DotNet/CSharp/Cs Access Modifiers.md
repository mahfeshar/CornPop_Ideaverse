---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-20
tags:
  - fcdotnet/access
---

- عبارة عن C# Keywords بتساعدني اني اعمل Indicate the accessibility scope

- أنا جوا ال [[Cs Namespace|Namespace]] بكتب أربع حاجات: 
  Class - Interface ([[Cs Value and Reference Types#Reference Types|Reference Types]]) | Struct - Enum (Value Type)
  وبرضو جوا الحاجات دي بيبقا فيه حاجات تانية زي فانكشنز او متغيرات وهكذا
  محتاج أعرف الحاجات دي هتبقا Accessible لحد فين بالظبط سواء جوا الـLibrary بس ولا لو حد استخدم الـLibrary في بروجكت تاني

![[Pasted image 20240803103104.png]]
## Access Modifiers

### All

| Access Modifier        | الوصول داخل الكلاس | الوصول في نفس الـ Namespace | الوصول في الكلاس Inherited | الوصول من كلاس آخر |
| ---------------------- | ------------------ | --------------------------- | -------------------------- | ------------------ |
| **Public**             | نعم                | نعم                         | نعم                        | نعم                |
| **Private**            | نعم                | لا                          | لا                         | لا                 |
| **Protected**          | نعم                | لا                          | نعم                        | لا                 |
| **Internal**           | نعم                | نعم                         | لا                         | لا                 |
| **Protected Internal** | نعم                | نعم                         | نعم                        | لا                 |
| **Private Protected**  | نعم                | لا                          | نعم (نفس Library فقط)      | لا                 |

#### شرح نظري ومثال لكل Access Modifier:

1. **Public**:
   - الكلمة المفتاحية `public` تعني أن المتغير أو الطريقة يمكن الوصول إليها من أي مكان في البرنامج.
   - **مثال**:
     ```csharp
     public class MyClass
     {
         public int myVar = 5;
     }

     class Program
     {
         static void Main()
         {
             MyClass obj = new MyClass();
             Console.WriteLine(obj.myVar);
         }
     }
     ```

2. **Private**:
   - الكلمة المفتاحية `private` تعني أن المتغير أو الطريقة يمكن الوصول إليها فقط داخل نفس الكلاس.
   - **مثال**:
     ```csharp
     public class MyClass
     {
         private int myVar = 5;

         public void ShowVar()
         {
             Console.WriteLine(myVar); 
             // يمكن الوصول إليها داخل نفس الكلاس
         }
     }

     class Program
     {
         static void Main()
         {
             MyClass obj = new MyClass();
             obj.ShowVar();
         }
     }
     ```

3. **Protected**:
   - الكلمة المفتاحية `protected` تعني أن الوصول مسموح به داخل نفس الكلاس أو الكلاسات المشتقة.
   - **مثال**:
     ```csharp
     public class MyClass
     {
         protected int myVar = 5;
     }

     public class DerivedClass : MyClass
     {
         public void ShowVar()
         {
             Console.WriteLine(myVar);
         }
     }
     ```

4. **Internal**:
   - الكلمة المفتاحية `internal` تعني أن الوصول مسموح به فقط داخل نفس التجميع (Assembly)، سواء كان الكلاس في نفس الـNamespace أو كلاس آخر.
   - **مثال**:
     ```csharp
     internal class MyClass
     {
         internal int myVar = 5;
     }

     class Program
     {
         static void Main()
         {
             MyClass obj = new MyClass();
             Console.WriteLine(obj.myVar); 
             // يمكن الوصول إليها لأنها internal في نفس التجميع
         }
     }
     ```

5. **Protected Internal**:
   - الكلمة المفتاحية `protected internal` تعني أن الوصول مسموح به داخل التجميع أو من خلال كلاسات مشتقة.
   - **مثال**:
     ```csharp
     public class MyClass
     {
         protected internal int myVar = 5;
     }

     public class DerivedClass : MyClass
     {
         public void ShowVar()
         {
             Console.WriteLine(myVar); // يمكن الوصول إليها في كلاس مشتق أو داخل نفس التجميع
         }
     }
     ```

6. **Private Protected**:
   - الكلمة المفتاحية `private protected` تعني أن الوصول مسموح به فقط في نفس التجميع ومن الكلاسات المشتقة.
   - **مثال**:
     ```csharp
     public class MyClass
     {
         private protected int myVar = 5;
     }

     public class DerivedClass : MyClass
     {
         public void ShowVar()
         {
             Console.WriteLine(myVar); // يمكن الوصول إليها لأن الكلاس المشتق في نفس التجميع
         }
     }
     ```
### Private
- الـ Member بيبقا عليه قفل كدا
- مش بيبقا متاح برا الـ Scope اللي انا فيه سواء Class أو Struct
### Internal
- بيبقا عليه علامة قلب
- متقدرش تشاركه برا الـ Project بتاعك
  بمعنى انك لو عملت Library معينة فدي Project تقدر جواها تستخدم الـ Member لو Internal إنما لو استدعيته جوا Project تاني مش هيرضى

### Protected
- بيبقا عليها نجمة كدا
- أي حاجة من الحاجات اللي فيها الـ Protected مقدرش أستخدمهم غير جوا الـClass ومقدرش أستخدمهم في الـ Struct لأنه مش بيسابورت الوراثة
- بستخدمهم عشان الـ [[Cs Inheritance]] وان الحاجات الـ Private تتشاف برا ومكررهاش
- بالنسبة للكلاس اللي هي فيها بتبقا Private
### Private Protected
- بالنسبة للكلاس اللي هي فيها بتبقا +Private
### Internal Protected
- بالنسبة للكلاس اللي هي فيها بتبقا Internal
### Example
```cs
// Library: Common
// Class: TypeA
public class TypeA
{
	private protected int X; // Private
	/*protected*/ int Y; // Private
	internal protected int Z; // Internal
}

// Class: TypeB - in same Library
internal class TypeB : TypeA
{
    public TypeB()
    {
        /*
         * X is Private
         * Y is Private
         * Z is Internal
         */
    }
}
// Library: AnotherLib
// Class: TypeB - in another Library
internal class TypeB : TypeA
{
	public TypeB()
	{
		/*
		 * X is NOT Inherited
		 * Y is Private
		 * Z is Private
		 */
	}
}
```
## Inside [[Cs Namespace|Namespace]]
بنقدر نكتب جوا ال Namespace أربع حاجات:
1. [[Cs Class]]
2. [[Cs Struct]] stands for structure
3. [[Cs Interface]]
4. [[Cs Enums]]

---
معنديش Access Modifiers غير اتنين جوا ال Namespace:
1. Internal (**Default**)
2. Public

>قبل ما تحاول تستخدم أي class أو حاجة موجود في ==Library== تانية لازم إني أضيف ال Library دي للـDependences للبروجكت
  Right click at project -> Build dependencies -> Project dependencies
  Add project reference
  وبعد كدا أعمل using للـLibrary دي
### Internal
- قولنا اننا لو مديناش الحاجة Access Modifier فهو طبيعي هيبقا Internal 
- معناها إني هي ليها Access بس جوا ال Library اللي انا فيها 
  ولو حاولت أعملها Access جوا Library أو بروجكت تاني مش هينفع ومش هقدر أوصله
- لو حاولت أوصل ل class مثلًا في project مختلف هيديلي error
- الحل إنك تعملها public عشان تقدر توصلها في أي Project وأي Library مختلفة


## Inside [[Cs Class|Class]] or [[Atlas/Notes/Ideas/Programming/DotNet/CSharp/Cs Struct|Struct]]
بنقدر نكتب جواهم:
1. Attributes (Fields) -> Member Variables
2. [[Cs Properties]] (Full Property, Automatic Property, Indexer -> Special)
3. [[Cs Function]] (Constructor, Getter Setter, Method)
4. [[Cs Event]]

---
متاح 3 Access Modifiers جوا الـ **Struct**: (نفس بتاع الـ Name Space وهنزود الـ Private)
1. Private (Default)
2. Internal
3. Public

جوا الـ **Class** متاح كل الستة:
1. Private (Default)
2. Private Protected
3. Protected
4. Internal
5. Internal Protected
6. Public

> [!example] Default
> الـ Default فيهم الإتنين هو **Private**

## Inside [[Cs Interface|Interface]]
نقدر نكتب جواها:
1. Signature for Property
2. Signature for Method
3. Default Implemented Method (فانكشن كاملة)

الـ Method بتتكون من جزئين (Signature - Body):
الـ Signature اللي هو اسمها والـ Parameters اللي بتستقبلها وكدا

> [!example] Default
> الـ Default فيها هو **Public**
> لأن بكتب فيها signatures فمحتاج أوصل للـ Implementation

## Inside [[Cs Enums|Enums]]
بنكتب جواها Labels

## Flashcards
ايه هي الـ Access Modifiers
?
عبارة عن C# Keywords بتساعدني اني اعمل Indicate the accessibility scope

---
كم عدد الـ Access Modifiers وقولهوملي
?
عددهم 6
Private - Public - Internal - Protected - Private Protected - Internal Protected

---
نقدر نكتب ايه جوا الـ Namespace وايه الـ Access Modifiers المتاحة وايه الـ Default
?
Class - Interface - Struct - Enum
متاح 2 وهما الـ Internal و الـ Public
والـ Internal هي الـ Default

---
نقدر نكتب ايه جوا الـ Struct و Class وايه الـ Access Modifiers المتاحة وايه الـ Default
?
1. Attributes (Fields) -> Member Variables
2. CSharp Property (Full Property, Automatic Property, Indexer -> Special)
3. CSharp Function (Constructor, Getter Setter, Method)
4. CSharp Event
متاح 3 Access Modifiers جوا الـ **Struct**: (نفس بتاع الـ Name Space وهنزود الـ Private)
1. Private (Default)
2. Internal
3. Public
جوا الـ **Class** متاح كل الستة:
1. Private (Default)
2. Private Protected
3. Protected
4. Internal
5. Internal Protected
6. Public

---
نقدر نكتب ايه جوا الـ Interface وايه الـ Default
?
نقدر نكتب جواها:
1. Signature for Property
2. Signature for Method
3. Default Implemented Method (فانكشن كاملة)
الـ Default فيها هو **Public**
لأن بكتب فيها signatures فمحتاج أوصل للـ Implementation

---
نقدر نكتب ايه جوا الـ Enum:: بنكتب جواها Labels