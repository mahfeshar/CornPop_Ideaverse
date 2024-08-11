---
up:
  - "[[Programming MOC]]"
related: 
created: 2024-08-05
---

## What is OOP?
- Object Oriented Programming (OOP) is a programming *paradigm* based on the concept of "objects"
- The data is often implemented as attributes. Functions implement as methods.
- In OOP, computer programs are designed by being made up of objects that interact with each other via the methods.
- OOP is a Paradigm or Coding Style
	OOP Paradigm =>Means Structuring Program 
	So The Methods *Functions* and Attributes *Data* are bundled into objects
- Methods => Act as function that use the information of the object
## 4 Concepts (Pillars)
عندنا أربع مبادئ هنحتاج نعرفهم ونفهمهم كويس:
- [[Encapsulation]] 
- [[Abstraction]]
- [[Inheritance]]
- [[Polymorphism]]
# Why OOP?
## Primitively Data Types
- أنواع البيانات البدائية: بتخزن Single simple value
  مثال: Byte, Int, Flaot, Double, Char, Boolean
- مكنتش مشكلة في البداية لأن البرامج كانت بسيطة جدًا بس مع الوقت البرامج بدأت تتعقد لأن المطورين عايزين ي group variables together
### ليه أصلا نعملهم group together ؟
- تخيل معايا اننا عايزين نصمم لعبة شطرنج فأنا دلوقتي هيبقا عندي كذا قطعة وكل قطعة من دي ليها صفات معينة زي اللون وهل اتاكل ولا لا؟ وخصائصه ايه؟
- يعني مثلًا الفيل عندنا فيل أبيض أو أسود ومقدرش أستخدمه لو متاكل وطبعا له حركة معروفة ومثلًا الملك نفس الحوار وهكذا كل قطعة

- فهل المفروض أعمل لكل حاجة من الحاجات دي variable؟
```python
# first feel
Feel1position = 3
Feel1color = "White"
Feel1boolean = false
# We should make this for every piece
```
- الموضوع هيبقا معقد أوي
  فعشان كدا المفروض اتعامل مثلًا مع الفيل على انه شيء object وهكذا مع كل قطعة بكل الخصائص بتاعها دي، كدا الموضوع هيبقا أسهل كتير
## Struct
- مشابه لل array بانه بيسمح انه يخزن أكتر من قيمة واحدة مش زي ال Premitive Data Types بتخزن قيمة واحدة

- الفرق: ان ال array بتخليك تخزن أكتر من حاجة من نفس النوع 
- انما ال struct بيسمحلك انك تخزن data types مختلفة

- فدا هيحللي المشكلة اللي فوق اني أقدر أجمع الخصائص بتاع الفيل كلها في مكان واحد وهو ال struct
```python
struct feel{
	position
	boolean
	color
}
```
- نقدر نقول ان ال struct هي الحاجة اللي قبل ال object ولكن لسا عندي مشكلة في ال struct

- مش بعرف أعرف function جوا ال struct ودي مشكلة
- وكمان مش بيبقا فيه [[Inheritance]] فيها زي ما اتكلمنا عن الموضوع دا في [[Cs Struct#^8c8987|Struct vs Class]]
- يعني الفيل اللي فوق دا محتاج يتحرك يعني محتاج يعمل وظيفة معينة 
## Object
- Object is an instance نموذج of a Class
- Class is a Template اطار for the object

- نفس المثال اللي فوق دا محتاج أعمل عيلة اسمها feel والعيلة دي هتحدد أي object طالع منها ايه الصفات اللي فيه؟
- أي حاجة جوا ال class هتنطبق على اي feel في اللعبة 

- فأنا هبدأ اعمل class احط فيه الحاجات اللي فوق دي 
```python
Class Feel:
	Position
	Color
	Boolean
	Move()
```
- ومش هحط قيم في ال variables دي لأن دا يعتبر حاجة عامة لكل الأربع أفيلة اللي في اللعبة
- الحاجة الوحيدة اللي ممكن أكتب الكود بتاعها كامل هي ال functions 
- لأن كل الفيلة بتتحرك بنفس الطريقة ومش هيختلف من واحد للتاني

- بعد ما أعمل ال class أقدر انشئ كائنات objects منه
  الفيل الأبيض اللي عاليمين - اللي عالشمال - الأسود على اليمين وهكذا
- في الحالة دي أقدر أدي قيم للمتغيرات دلوقتي
```python
Feel1 = new Feel(3, "white", false)
```
- لما بعمل object فالصفات بتاعه بتبقا خاصة بال object دا بس
- انما لما بعمل class الحاجات اللي جواه بتنطبق على أي object (أي فيل من الفيلة)

- فالخلاصة ان ال oop سهلت على المبرمجين انهم يعملو برامج أعقد وأقوى
