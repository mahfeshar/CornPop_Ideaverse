---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-10
---
- اتكلمنا عنها قبل كدا في [[Abstraction]]
- كلمة abstract هنا معناها إن الحاجة ناقصة سواء [[Cs Class]] أو [[Cs Function]] أو [[Cs Properties]]
```cs
abstract class Shape
{
    public decimal Dim01 { get; set; }
    public decimal Dim02 { get; set; }
    // public decimal CalculateArea() { } 
// I can't make like that because I don't know what is the shape
	public abstract decimal CalculateArea();
}

// MAIN
// Shape sh1 = new Shape(); 
// Cannot create object (instance) - not fully implemented
// But we can create reference
Shape sh1;
```
- معرفتش هعمل إيه في الـ method اللي اسمها Area لأني معرفش هستخدم أي قانون فبقا ناقص عندي فبالتالي هستخدم كلمة abstract عشان أقول إنها ناقصة implemented
- وبما إن الـ Class فيها حاجة مش كاملة وهي الـ Method فبالتالي الـ Class نفسه مش كامل وبالتالي لازم أستخدمله كلمة Abstract
  ممكن يبقا الـ Class abstracted برضو وفيه كل حاجة كاملة عادي بس أنا عايز محدش يقدر يوصله 
- مينفعش تعمل object من الـ Abstract class لأنه Not fully implemented (ناقص)
- ممكن يبقا الـ Abstract class **عبارة عن Container code** لحاجات هتيجي في المستقبل
  مثال: لو عندي نوعين Employee واحد Partial, Fully فالـ Employee الأب مش هحتاج أشوفه

