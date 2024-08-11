---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-17
---
 
- هي عبارة عن special method بنستخدمها عشان initialize objects
- بيتم مناداتها أو ما بتعمل create object
- الـ [[Cs Access Modifiers|Access Modifier]] بتاعه في الطبيعي بيبقا Public إلا في Design pattern واحدة 

```cs
class Car
{
	public string model; //field
	public Car() // parameter less - default cons
	{
		model = "Mustang"; // initial value
	}

	public Car(string modelName)
	{
	    this.model = modelName;
	}

	static void Main()
	{
		Car Ford = new Car();
		Console.WriteLine(Ford.model); // Mustang
	}
}
```
- The constructor name must **match the class name**, and it cannot have a **return type**
- All classes have constructors by default: if you do not create a class constructor yourself, C# creates one for you.
	- كل اللي بتعمله ان هي بتدي default value لكل field عندي، يعني ال int ياخد صفر
- ال ctor اللي بيبقا مفهوش برامتر بيبقا اسمها ==parameter less - default ctor==
	- في الطبيعي بياخد كل الـ Attributes ويحطلها القيمة الـ Default بتاع النوع دا
	  يعني لو هي من النوع Int هيديلها صفر

![[Pasted image 20240318153133.png]]

## Constructor Overloading
- ال Overloading: انك يبقا عندك method ليها نفس الإسم بس متغير فيها signatures
- Signatures: What uniquely identify a method (Return type, name, the types and numbers of its parameters)

```cs
public class Car 
{
	public Car () { ... }
	public Car (string name) { ... }
	public Car (int id, string name) { ... }
}
```

## this keyword
- عندي مشكلة إن مينفعش أعرف field من النوع [[Cs List]] وأسيبه مش حاجزله مكان بال new
- دا هيعملي مشكلة لو جيت أضيف عنصر في ال list أو استخدمها عمومًا ولازم أعملها initialization الأول
- الحل إننا نعمل كدا في default constructor 
```cs
public List<Order> Orders;

public Customer()
{
	Orders = new List<order>();
}
```

- هيظهرلي مشكلة تانية إني ممكن أستخدم Constructor تاني فكدا الليست مش هيتعملها initialization
- بالتالي فيه حل إننا لازم نكرر نفس الحوار في كل ال constructors اللي عندنا بس دا مش حل عملي
- الحل التاني اننا نستخدم this

```cs
public class Customer
{
    public int ID;
    public string Name;
    public List<Order> Orders;
    // When you use a list of any type, you should initialize it at ctor

    public Customer()
    {
        Orders = new List<Order>();
    }
    public Customer(int id)
        :this()
    {
        this.ID = id;
    }
    public Customer(int id, string name)
        :this(id)
    {
        this.ID = id;
        this.Name = name;
    }
}
```

- دا بكل بساطة هيخلي أي constructor هتناديه، هيروح ينادي على ال constructor ال default الأول
- نقدر نخلي أي constructor ينادي أي واحد قبله بشرط إني أحط ال parameters جوا القوسين بعد this