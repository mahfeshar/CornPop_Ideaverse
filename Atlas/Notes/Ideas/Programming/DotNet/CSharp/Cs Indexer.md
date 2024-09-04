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
```
اقدر من خلالها اعمل overloading اني أستخدم أكتر من واحدة لنفس ال object باختلاف ال parameters اللي داخله او باختلاف عددهم

مثال على ال indexer هو ال strings 
```cs
String Str = "123";
if (Str[0] == 1) ; //read : get
Str[0] = '2'; //Error: we cannot change it, no set: Read Only
```