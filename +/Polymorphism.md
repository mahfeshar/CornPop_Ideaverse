---
up:
  - "[[OOP]]"
related: 
created: 2024-09-28
---
![[PolyMorphism.jpg]]
- المبدأ  دا بيكمل ال [[Inheritance]] 
- Polymorphism (from Greek, meaning “many forms”) is the ability of an object to take different forms and thus, depending upon the context, to respond to the same message in different ways. 
- Take the example of a chess game; a chess piece can take many forms, like bishop, castle, or knight and all these pieces will respond differently to the `move` message
- بيفيدني اني بقدر أعمل Single action in a different ways ودا بيخلي فيه Interface واحد بيعمل أكتر من حاجة ودا بيساعد برضو في فكرة ال [[Encapsulation]] ان تفاصيل الشغل بتبقا مستخبية شوية
- فيه مبدأين أساسيين فيها وهما:
### Method Overriding
- الأب بيبقا فيه صفة معينة أو method معينة زي صفة الحركة بس الصفة دي متشابهة في الاسم بس مع الابن بس بصفات تانية وبتشتغل بطريقة تانية
- بغير كل حاجة جواه مش هتبقا متشابهه غير في الإسم
- نفس الFunction بنفس الاسم بس في كل Class بيعمل حاجة مختلفة على حسب ال Object اللي هو معمول منها

![[Pasted image 20240414205632.png]]
### Method Overloading
![[Overloading 1.jpg]]
- وجود نفس ال Function في نفس الclass بنفس الاسم (متكرر)
- مش بيأثر على الـ Memory هو بس يخلي الكود **Readable** و **Reusable** 
- بنفرقه عن طريق ال Parameters اللي بياخدها كل واحدة عن التانية، وكل واحد هيقوم بحاجة مختلفة شوية عن الباقي

```python
def Sum(int x, int y):
	return x + y

def Sum (int x, int y, int z):
	return x + y + z

def Sum (float x, float y):
	return x + y
```
- تخيل اني بعمل كل واحدة من دول باسم مختلف عن التاني فهيخلي الكود معقد قد ايه، مع ان كلهم بيعملوا نفس الحاجة انهم بيجمعوا فمش هعرف أفتكر كل الأسماء وهيصعب الكود وقرائة الكود وكل حاجة
```python
Sum2Ints(int x, int y):
	return x + y
Sum3Ints(int x, int y, int z):
	return x + y + z
SumFloat(float x, float y):
	return x + y
```