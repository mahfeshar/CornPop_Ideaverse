---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-10-06
---
- هو عبارة عن Code contract بين الـ Developer اللي كتبه والـ Developer اللي هيعمله Implementation 
- Interface → prototype - code contract - no data in
- If class follows an interface we must initialize all interface (methods, properties) in the class
- بيتكتب جوا الـ [[Cs Namespace]] وقولنا الموضوع دا في [[Cs Access Modifiers#Inside Cs Namespace Namespace|Inside Namespace]] 
- مينفعش أعمل Object من الـ Interface بس ينفع أعمل Reference
  لأن أصلًا بيبقا فيه Bodies بس فهو هيعمل ايه؟
```cs
interface IMyType
{
	 int Salary {get; set;}
	 void MyFun();
	 void Print()
	 {
		 Console.WriteLine("Hello World");
	 }
}
```
- اللي بيعمل Implement هو [[Cs Class]] أو [[Cs Struct]]: يعني هيعدي على كل Signature ويكتب الـ Implementation 

---
- الـ Reference من الـ Interface يقدر يشاور على Object من الـ Class بشرط إن الـ Class يكون بي Implement الـ Interface
  ودي الطريقة الوحيدة اللي أقدر أوصل بيها للـ 


## Access modifiers
![[Cs Access Modifiers#Inside Cs Interface Interface]]

## Examples
