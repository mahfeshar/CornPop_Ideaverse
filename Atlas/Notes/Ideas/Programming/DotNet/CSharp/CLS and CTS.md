---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-04
---

## Common Language Specification (CLS)
- CLS is a part of CLR in the .NET Framework.
  بتتكلم على ال specification بتاع ال common language (IL)
- CLS stands for Common Language Specification and it is a subset of CTS. It defines a set of rules and restrictions that every language must follow which runs under the .NET framework.
- من ضمن الحاجات اللي بيتعملها description في ال CLS حاجة اسمها common type system
## Common type system (CTS)
- هو ال type system اللي أي data type هيكومبايل ل IL هيتبعها
- عاملين زي حاجة Standard كدا لكل ال data types لكل لغات البرمجة اللي بنستخدمها في .NET تحت مظلة ال .NET 

![[Pasted image 20240704210039.png]]
- عشان لما يتحولو ل IL بعد كدا الاتنين يتحولو لنفس الحاجة
- اعرف أولًا ان في ال base class library فيها أربع حاجات:
  classes, struct, enum, interfaces
- ال CTS بيقسم ال types لنوعين:
[[Cs Value and Reference Types]]