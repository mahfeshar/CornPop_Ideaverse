---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-04
---

## Properties (**Most Used**)
- عرفنا قبل كدا ان الحاجة ال `private` مبقدرش أوصلها غير في ال class اللي انا فيه [[Cs Access Modifiers]]
  بس في بعض الأحيان ببقا محتاج أوصل للمتغيرات دي براها فهنا هنستخدم ال properties

- A property is like a combination of a variable and a method, and it has two methods: a `get` and a `set` method:

- دي حلتلي المشكلتين اللي فوق، اني أقدر استخدمها بنفس شكل الكتابة العادي وكل مشاكل ال public محلولة

```cs
class Person
{
	private string name; //field
	
	public string Name // property
	{
		get { return name; } //get method
		set { name = value; } // set method
		// internal set {name = value.Length > 20? value: value.Substring(0, 20);}
	}
}

class Program
{
	static void Main()
	{
		Person myObj = newPerson();
		myObj.Name = "Corn"; // used property
		Console.WriteLine(myObj.Name); // Corn
		//طريقة الاستخدام اكنك بتستخدم متغير عادي
```

>It is a good practice to use the same name for both the property and the private field, but with an uppercase first letter.

#### Automatic Properties (Short Hand)
- اللي فوق اسمها Full Property
- You do not have to define the field for the property, and you only have to write `get;` and `set;` inside the property.
- لو مش هتستخدم الـ Field نفسه في حاجة استخدم دي، يعني لو مش هتعمل مثلًا Validation أو حاجة اعمله short hand
```cs
class Person
{
	public string Name //property
	{ get; set; }
}
```
- Compiler will generate backing field (Hidden Private Attribute)
لو استخدمنا `ILSpy` هيعرفنا انه عمل Attribute Private عشان الـ Property دي من غير حتى ما أعرف أنا الـAttribute

![[Pasted image 20240805230331.png]]

#### Notes about properties
- ال property ما هي الا method 
  تقدر تعملها كل حاجات ال methods زي ال override وغيره بس الفرق في طريقة الكتابة
- جوا ال property تستخدم ال attribute اللي بيبقا في الغالب small
- جوا ال methods اللي جوا ال class استخدم ال attribute عشان ميعملش overhead 
  ولو فيه filtration مثلا ممكن تعيد الكود او في الحالة دي تستخدم ال property عادي
- برا الclass بنستخدم ال property بقا اللي بتبقا بال Capital
- ال property بتشتغل على single input parameter يعني مقدرش اعملها Overloading
- اقدر أعمل Property يبقا Read-only بس مثلًا من خلال إني أشيل Set أو العكس

#### Code Snippet
- عندنا أكتر من واحد عشان يسهل الكتابة وهي انك تكتب `propfull` وبعدين اتنين tab وهيعملك Field بالـ Property بتاعها
- ولو عالـ Automatic فهي code snippet بتاعها `prop