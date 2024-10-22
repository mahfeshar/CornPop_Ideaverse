---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---

الاوبريتور عندى بتعمل حاجة معينة زي مثال الـ * بتضرب االرقام في بعض وهكذا ف انا محتاج انى اعلمها حاجة جديدة فبعملها overloading
لازم تكون not private **class method** 
```cs
class Complex
{
    public int Real { get; set; }
    public int Imag { get; set; }
    public override string ToString()
    {
        return $"{Real} + {Imag}i";
    }
    // Operator Overloading
    public static Complex operator +(Complex c1, Complex c2)
    {
        return new Complex()
        {
            Real = c1.Real + c2.Real,
            Imag = c1.Imag + c2.Imag
        };
    }
}

// MAIN
Complex c1 = new Complex()
{
    Real = 10,
    Imag = 20
};
Complex c2 = new Complex()
{
    Real = 30,
    Imag = 40
};

Console.WriteLine(c1 + c2); 
// ERROR: We should make casting operator
```
بس كدا الكود مش safe بسبب إن الـ Complex لو إديتله قيمة default يبقا Null
```cs
Complex c1 = default; // NULL
```
- هنستخدم الـ [[Cs Null#Null Propagation (Conditional) Operator|Null Propagation]]
```cs
public static Complex operator +(Complex c1, Complex c2)
{
	return new Complex()
	{
		Real = c1?.Real??0 + c2?.Real??0, 
		// (c1 != null)? c1.Real : null
		// c1 != null ? c1.Real : 0
		Imag = c1?.Imag??0 + c2?.Imag??0
	};
}
```
## ++ operator
- For Prefix and Postfix
```cs
public static Complex operator ++ (Complex C)
{
	return new Complex()
	{
		if (C is not null)
			C.Real++;
		return C;
		//return new Complex()
		//{
		//	Real = C?.Real??0 + 1,
		//	Imag = C?.Imag??0
		//};
	}
}
```

## > Operator
- هنا فيه شرط انك لو هتعمل للأكبر من فلازم تعمل للأصغر من
- وبرضو لو عملت لليساوي فلازم تعمل للا يساوي
```cs
public static bool operator > (Complex left, Complex right)
{
	if (left?.Real == Right?.Real)
		return left?.Imag > right?.Imag;
	return left?.Real > Right?.Real
}
```
## Casting Operator
اتكلمنا عنها في [[Cs Casting Operator]]
اللي تحت دي أمثلة عن إزاي بنعمل Overloading على Casting Operators كانت موجودة بالفعل
### Explicit Casting
دا الأحسن عشان الـ Readability 
```cs
public static /*int*/ explicit operator int(Complex C)
{
	return C?.Real??0;
}
```
### Implicit Casting
```cs
public /*static*/ string implicit operator string(Complex C)
{
	return C?.ToString()?? string.Empty;
}
```