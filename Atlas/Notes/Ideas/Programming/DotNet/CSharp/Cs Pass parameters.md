## Pass Value Type
- By Value => Read Only
- By Reference => Read & Write
- By Out => Same as Ref, but Write first

![[Pasted image 20240318115829.png]]
### Pass By Value
- اني بمرر القيمة بس وهو بيعمل نسخة بيشتغل عليها في ال function وبعد أما بيخلص بيمسح النسخة دي ومش بيغير في الأصل
```cs
public static void SWAP (int X, int Y)
{
	int Temp = X;
	X = Y;
	Y = Temp;
}

static void Main()
{
	int A = 7, B = 3;
	SWAP(A, B); // by value القيم مش هتتغير
}
```

###  Pass By Reference
وهي اني ببعت المتغير نفسه مش بس القيمة وأي تغيير بيحصل جوا ال function بيحصل برضو في الvariables الأصلية
```cs
public static void SWAP (ref int X, ref int Y)
{
	int Temp = X;
	X = Y;
	Y = Temp;
}

static void Main()
{
	int A = 7, B = 3;
	SWAP(ref A, ref B); // by Reference
	//A = 3, B = 7
}
```

### Pass By Out
- زي ال reference بالظبط بس انت لو جيت في ال reference تدخل مثلًا variable مش محددله قيمة هيديلك إيرور عشان المفروض يقرأ الكلام دا (Read)
- فالحل اني استخدم out
```cs
public static void SumMul(int X , int Y , out int S , out int M)
{
    S = X + Y;
    M = X * Y;
}
int A = 7, B = 3, SResult, MResult;
SumMul(A, B, out SResult, out MResult);

//We can define it at same call
SumMul(A, B, out int SResult, out int MResult);

// _ discard: لو عندي متغير مش هستخدمه
SumMul(10,7, out _, out int SR);
```
## Reference Type (Pass)
### Pass By Value
- هنا بقا مختلفة احنا بنتعامل أول حاجة مع ال heap مش مع ال stack، فلو تفتكر كنا بنقول في [[Cs Value and Reference Types#Reference Types|Reference Types]] ان انت لو شاورت من ref ل ref تاني أكني بالظبط بشاور عليه أو [[Pointer]] ليهم نفس المكان في الميموري
- وبالتالي أي تغيير هيحصل هيسمع في ال variable الأصلي
- فدي باختصار اني بعيد تسمية ال variable باسم تاني والتغيير اللي هيحصل هيحصل في الأصلي

- لو غيرت في القيمة بيسمع في القيمة الأصلية وبيشاورو على نفس الحاجة في ال heap

![[Pasted image 20240318120750.png]]
```cs
public static void RefByValue(int[] Arr)
{
    Console.WriteLine(Arr.GetHashCode()); // Same
    Arr[Arr.Length - 1] = 0;
    Console.WriteLine("In Method");
    foreach (int i in Arr) Console.WriteLine(i); // 1 0
}

//Main
int[] A = [1, 2];
Console.WriteLine(A.GetHashCode()); // Same
RefByValue(A);
Console.WriteLine("In Main");
foreach (int i in A) Console.WriteLine(i); // 1 0 : Changed
```
- لو خليتها تشاور على array تانية قولنا هتبقا زي ال pointer بالظبط ففي ال method هتروح تشاور على حتة تانية في ال heap اللي فيها ال array الجديدة دي وأي تغيير هيحصل هيحصل على ال array الجديدة وملوش أي علاقة بالقديمة ومش هيلمسها
```cs
public static void RefByValue(int[] Arr)
{
    Console.WriteLine(Arr.GetHashCode()); // Same
    int[] newArr = [5, 6, 7, 8];
    Arr = newArr;
    Arr[Arr.Length - 1] = 0; // Change at new one
    Console.WriteLine($"newArr: {Arr.GetHashCode()}"); // diff
    Console.WriteLine("In Method");
    foreach (int i in Arr) Console.WriteLine(i); // new one
}

//Main
int[] A = [1, 2];
RefByValue(A);
Console.WriteLine(A.GetHashCode());
Console.WriteLine("In Main");
foreach (int i in A) Console.WriteLine(i);
```
### Pass By Reference 
- هتبقى نفس الحوار في اللي فوق لو غيرت في القيمة
- الفرق هيظهر اني لو خليت ال array تشاور على واحدة تانية في الحالة دي الأصلية واللي في ال method الاتنين هيروحوا يشاورو على الجديدة دي يعني ال array ال main كمان هتتغير وتبقا بتشاور في ال heap على الجديدة اللي غيرتها في ال method
```cs
public static void RefByValue(ref int[] Arr)
{
    Console.WriteLine(Arr.GetHashCode());
    int[] newArr = [5, 6, 7, 8];
    Arr = newArr; // The main one will be changed
    Arr[Arr.Length - 1] = 0;
    Console.WriteLine($"newArr: {Arr.GetHashCode()}");
    Console.WriteLine("In Method");
    foreach (int i in Arr) Console.WriteLine(i);
}

//Main
int[] A = [1, 2];
Console.WriteLine(A.GetHashCode());
RefByValue(ref A);
Console.WriteLine(A.GetHashCode());
Console.WriteLine("In Main");
foreach (int i in A) Console.WriteLine(i);
```