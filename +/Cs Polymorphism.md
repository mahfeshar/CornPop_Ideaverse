---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-28
---
- شرحنا الـ [[Polymorphism]] قبل كدا
- هو مرتبط بصورة كبيرة بالـ [[Cs Inheritance]] لأن فيه مبدأ من المبادئ اللي هنا مينفعش تتحقق غير لما يحصل وراثة وهو مبدأ الـ **Overriding**

## Overloading
- مش محتاج أي حاجة قبلها مطلوبة أو كدا
-  شغالة مع الـ [[Cs Class]] و [[Cs Struct]]
- هو خمس أشكال: 
  (Constructor - Indexer - Method - Operator - Casting operator)
- اتكلمنا عن الـ Constructor overloading في [[Cs Constructor]]
- اتكلمنا عن الـ Indexer Overloading في [[Cs Indexer]]

### Method Overloading
ودي بكل بساطة إن بيبقا عندي أكتر من [[Cs Function]] ليهم نفس الإسم بس مختلفين في:
- عدد 
- نوع 
- ترتيب الـ Parameters 
وكل واحدة بيبقا ليها Behavior مختلف

```cs
/// BEFORE
public static int sum(int a, int b)
{
    return a + b;
}
public static int sum3nums(int a, int b, int c)
{ 
    return a + b + c;
}
// Main
int result = sum(1, 2);
Console.WriteLine(result); // 3
result = sum3nums(1, 2, 3);
Console.WriteLine(result); // 6

/// AFTER
public static int sum(int a, int b)
{
    return a + b;
}

public static int sum(int a, int b, int c)
{ 
    return a + b + c;
}

// Main
int result = sum(1, 2);
Console.WriteLine(result); // 3
result = sum(1, 2, 3);
Console.WriteLine(result); // 6
```
## Overriding
- في نفس المثال اللي قولناه في الـ Inheritance

#### Hide and make new version
- الطريقة دي زي ما قولنا إنها بتعمل function جديدة وبتخفي اللي في الأب نهائي
```cs
// Parent
puplic int Product()
{
	return X * Y;
}

// Child

/// Hide and make a new version
/// The VS will tell you to add new, It will hide product from the parent
public int Product() 
{
    return X * Y * Z;
}

/// TRUE
public new int Product()
{
    return X * Y * Z;
    // return base.Product() * Z;
}
```

#### Override
- دي بتعيد كتابة الحاجة تاني
- شرط: إن الفانكشن الأساسية تبقا **Public virtual**
```cs
//Parent
public virtual int Product()
{
    return X * Y;
}

// Child
public override int Product()
{
    return base.Product() * Z;
}

public override string ToString()
{
    return $"X: {X}, Y: {Y}, Z: {Z}";
}
```