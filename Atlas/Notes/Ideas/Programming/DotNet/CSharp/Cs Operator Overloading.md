---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-11
---

الاوبريتور عندى بتعمل حاجة معينة زي مثال الـ * بتضرب االرقام في بعض وهكذا ف انا محتاج انى اعلمها حاجة جديدة فبعملها overloading
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
بس كدا الكود مش safe بسبب إن الـ Complex لو إديتله قيمة default يبقا 