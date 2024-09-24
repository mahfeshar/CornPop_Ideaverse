---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-04
---

## Variables
- Variables are containers for storing data values.
- متغير يتغير مع الوقت
- We can use any [[Cs Value and Reference Types]] of data types

### Declaring (Creating) Variables
```cs
// type variableName = value;

string name = "Corn";
int myNum = 15;

// Declare without assigning
int myNum;
myNum = 15;

//if you assign a new value to an existing variable, it will overwrite the previous value
int myNum = 15;
myNum = 20; // myNum now is 20

int myNum = 5;
double myDoubleNum = 5.99D;
char myLetter = 'D';
bool myBool = true;
string myText = "Hello";

```

### Multiple Variables
To declare more than one variable of the **same type**, use a comma-separated list:

```cs
int x = 5, y = 6, z = 50;
Console.WriteLine(x + y + z);

// You can also assign the **same value** to multiple variables in one line
int x, y, z;
x = y = z = 50;
```
## Custom (Variables)
### Const
- If you don't want others (or yourself) to overwrite existing values, you can add the `const` keyword in front of the variable type.

```cs
const int myNum = 15;
myNum = 20; //error
```

> **Note:** You cannot declare a constant variable without assigning the value. 
> If you do, an error will occur: A const field requires a value to be provided.
### Implicit Typed Local Variable (var)
- بكل بساطة اني هخلي ال compiler يحدد ال datatype عن طريق ال initial value اللي هديهاله 
- خد بالك ان الC# لغة مينفعش تغير ال variable type في النص، هو التعريف بتاعها اللي في الأول هيفضل عليه على طول (Strongly types)

```cs
double D = 15.3;
Console.WriteLine(D.GetType().Name);
D = "Hello"; //error

var D = 13.5;
Console.WriteLine(D.GetType().Name); // Same type
D = "Hello"; // Same Error
```
- Compiler will Detect Variable Data type Based on Initial Value
- Can't be not Initialized لازم تديله قيمة إبتدائية
- Can't be initialized with null

- تأثيره بيبقا بسيط أوي بس برضو بيأثر على قراءة الكود
- مش هيتم استخدامه غير في الحاجات ال advanced شوية زي ال LINQ والحاجات دي
---
- بيفهم نوع الداتا اللي بديهاله
- على حسب نوع القيمة بيحدد هيروح Heap ولا Stack
- لازم ياخد قيمة في ال compile time
### object
- دايما heap و reference type
- ممكن تعرفه من غير ما تديله قيمة
- مبيفهمش نوع الداتا اللي هو شايلها
- عشان تتعامل مع الداتا لازم تعملها casting
- base data type in C#

```cs
Object x = 5;
```

- We talked about it in details [[Cs System.Object]]

### dynamic 
- دايما heap و reference type زي ال object
- بيفهم نوع الداتا أثناء ال runtime فمش بتحتاج تعمل casting
