---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-04
---
## Indexer
- زيه زي ال property بس الفرق بينهم ان هي بتاخد أكتر من parameter سواء ال get, set
- استخدام مخصص لل square brackets `[]`  في ال C#
- عبارة عن property ومش بيبقا ليها اسم لاني بستخدم اسم ال object وبستخدم معاها ال `[]` زي الاراي `Book[input]`
- بستخدمه لما ببقا محتاج **أتعامل مع الـ object على إنه Array**
- مش بحتاج أحدد حاجة هو بيبقا Indexer للـ Object مش لـ Attribute معين مثلًا
- Indexer: is a **Special Property** 
  1. Named always with keyword `this`
  2. Can take **Parameters**
```cs
public long this[/*additional input*/]
{
	get // taking input
	{
		
	}
	set // taking input and value
	{
	
	}
}

public string this [int Index]
{
	get {}
	set {}
}

//string: return for get, input for set

// Note["Corn"] = 012875424123 // We can use object like this
```
- اقدر من خلالها اعمل **overloading** اني أستخدم أكتر من واحدة لنفس ال object باختلاف ال parameters اللي داخله او باختلاف عددهم
 ^bb0e19
- مثال على ال indexer **هو الـ strings**: هو عبارة عن class فالأساس بس بقدر أستخدمه كـ Array

```cs
String Str = "123";
if (Str[0] == 1) ; //read : get
Str[0] = '2'; //Error: we cannot change it, no set: Read Only
```

You can see [[Cs Encapsulation#Example Phone Book|Example: Phone Book]]