---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-09-04
---
اتكلمنا عن الـ [[Encapsulation]] وفايدته قبل كدا
## Why Encapsulation 
### Public Attribute
الميزة الوحيدة ليها هي سهولة الاستخدام لإني بستخدم نفس الشكل ونفس المنظر ونفس كل حاجة عشان أستخدمه

```cs
internal struct Employee
{
    public int Id;
    public string Name;
    public decimal Salary;
    public Employee(string _name, int _id, decimal _salary)
    {
        Id = _id;
        Name = _name;
        Salary = _salary;
    }

    public override string ToString()
    {
        return $"Name: {Name}\nID: {Id}\nSalary: {Salary:c}";
    }
}

// Main
Employee employee = new Employee("Mahmoud", 253, 5000);
employee.Id = 50;
Console.WriteLine(employee);

// I want to chage Id to EmpId
```

عيبه: 
- الكود بيبقا tightly coupled يعني لو حبيت أغير اسم ال variable او نوعه او اي حاجة هحتاج أعمل update لكل الكود والعالم الخارجي برضو
  واتكلمنا عنها بالتفصيل [[Encapsulation#^dc45aa|عزل تفاصيل الـ Implementation]]
- تاني مشكلة إن معدش عندي control عالكود بمعنى إني لو عايز أخلي مثلًا الـ Id دا Read-only فالحل بالنسبالي إني اخليه Private ودا هيمنع إني أعمله get أو set وكدا مليش كنترول واتكلمنا عنها في الـ [[Encapsulation#^fde557|المطور له الكنترول كامل]]
  مقدرش اتحكم في ال read & write اني اخلي واحد منهم يبقا public والتاني private
```cs
private int Id;

// Main
Employee.Id = 50; // ERROR
Console.WriteLine(Employee.Id) // ERROR
```
- مقدرش أ filter الداتا اللي رايحة واللي جاية - زي ما ال user دخلها هاخدها
وفيه مشاكل كتير هتظهر فالحل في الـ Encapsulation

### Why Encapsulation?
- Better control of class members (reduce the possibility of yourself (or others) to mess up the code)
- Fields can be made **read-only** (if you only use the `get` method), or **write-only** (if you only use the `set` method)
- Flexible: the programmer can change one part of the code without affecting other parts
- Increased security of data
## What is Encapsulation
- Separate Data Definition(Attributes) from its use (Getter setter, Property)
  افصل تعريف الداتا وخليها Private وبعدها استخدم طريقة تستخدمها برا
It's to make sure that "sensitive" data is hidden from users. 
To achieve this, you must:
- declare fields/variables as `private`
- provide `public` `get` and `set` methods, through **properties**, to access and update the value of a `private` field

## Getter and Setter (Methods)
عشان نحقق ال encapsulation:
- بعمل ال variable private 
- ببدأ استخدم methods عشان اشوفه واتحكم فيه من برا

حلت المشاكل اللي كانت فوق:
- أقدر أخلي الـ Field يبقا Read-only أو اي حاجة تانية باني أغير الـ Access Modifier أو اني امسح Method
- ليا التحكم الكامل على الـ Field ومحدش يقدر يتحكم فيه برا
- لو غيرت الإسم جوا مش هتفرق لأن مش مستخدمه غير في الـ Struct
عيبه:
- شكل الكتابة مش زي اللي فوق (معقدة أكتر)
```cs
private string Name;

public string GetName()
{
    return Name;
}

public void SetName(int newY)
{
    Name = Name.Length <= 20? Name : Name.Substring(0, 20);
}

//Main
Obj.GetName();
Obj.SetName();
```

## [[Cs Properties]]
## [[Cs Indexer]]
## Example: Phone Book
```cs
struct PhoneBook
{
    string[] Names;
    long[] Numbers;
    int size;

    public int Size { get { return size; } }

    public PhoneBook(int _Size) // Ctor
    {
        size = _Size;
        Names = new string[size];
        Numbers = new long[size];
    }


    public void SetEntry (int Index , string Name , long Number ) //Setter method
    {
        if ((Index>=0)&&(Index < size))
        {
            Names[Index] = Name;
            Numbers[Index] = Number;
        }
    }

    public long GetNumber ( string Name) //Getter method
    {
        for (int i = 0; i < Names?.Length; i++)
            if (Names[i] == Name)
                return Numbers[i];
        return -1;
    }

    public long this[string Name] //Indexer: R & W
    {
        get
        {
            for (int i = 0; i < Names?.Length; i++)
                if (Names[i] == Name)
                    return Numbers[i];
            return -1;
        }
        set
        {
            for (int i = 0; i < Names?.Length; i++)
                if (Names[i] == Name)
                    Numbers[i] = value;
        }
    }

    public string this[int Index] // Indexer : R
    {
        get
        {
            if ((Index >= 0) && (Index < size))
                return $"{Names[Index]}:::{Numbers[Index]}";
            return "NA";
        }
    }

    public long this [int Index , string Name] // Indexer : W
    {
        set
        {
            if ((Index >= 0) && (Index < size))
            {
                Names[Index] = Name;
                Numbers[Index] = value;
            }
        }
    }
	// We have overloading indexers
}
```