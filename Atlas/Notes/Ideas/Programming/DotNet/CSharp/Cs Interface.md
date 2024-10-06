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
  ودي الطريقة الوحيدة اللي أقدر أوصل بيها للـ Default implemented method
- مبستخدم الـ Default implemented method غير في حالة واحدة وهي ان يبقا عندي أكتر من Class ليهم نفس الـ Interface وبيبقا عندهم Function مشتركة
- للوهلة الأولى تحس العملية دي شبه الـ [[Cs Binding]]
- **بستخدمها** في الأغلب لو عندي Function عامة معرفش ممكن يبقا فيها ايه وممكن تتغير زي مثال الـ Series فمثلًا `GetNext` هتتغير وبيبقا زي **عقد** وبجبر الشخص اللي بيعمله انه يمشي على العقد دا

---
حلت مشكلتين عندنا:
- معنديش Multiple [[Cs Inheritance]] في الـ CSharp في الـ [[Cs Class]]
- معنديش [[Cs Inheritance]] في الـ [[Cs Struct]]
### Simple Example
```cs
interface IMyType
{
    public int Salary { get; set; } // Signature of Property
    void MyFunc();
    void Print()
    {
        Console.WriteLine("Hello World");
    }
}
//class MyType : IMyType
//{
//    public int Salary { get => throw new NotImplementedException(); set => throw new NotImplementedException(); }

//    public void MyFunc()
//    {
//        throw new NotImplementedException();
//    }
//}

// => goes to (arrow function) for oneline functions

interface IMyType
{
    public int Salary { get; set; } // Signature of Property
    void MyFunc();
    void Print()
    {
        Console.WriteLine("Hello World");
    }
}
class MyType : IMyType
{
    public int Salary { get => throw new NotImplementedException(); set => throw new NotImplementedException(); }

    public void MyFunc()
    {
        throw new NotImplementedException();
    }
}

// MAIN
IMyType T; // Reference to an Interface
//IMyType T2 = new IMyType(); // ERROR -> Cannot create an object of an Interface
IMyType T3 = new MyType(); // OK -> Upcasting from class to Interface
MyType T1 = new MyType();

T1.MyFunc();
// T1.Print(); //ERROR -> Cannot call a method of an Interface from class

T3.Print(); // OK -> Down casting from Interface to class
```

## Access modifiers
![[Cs Access Modifiers#Inside Cs Interface Interface]]

## Examples
```cs
namespace InterfaceEx1
{
		interface ISeries
		{
				int Current { get; }
				void GetNext();
				void Reset();
		}
		class FibSeries : ISeries
		{
				int current;
				int prev;
				public FibSeries()
				{
						prev = 0;
						current = 1;
				}
				public int Current { get { return current; } }
				public void GetNext()
				{
						int Temp = Current;
						current += prev;
						prev = Temp;
				}
				public void Reset()
				{
						current = 1;
						prev = 0;	
				}
		}
			
		struct SeriesByTwo : ISeries
	  {
		    int current;
		    public int Current { get { return current; } }
		
		    public void GetNext()
		    {
			       current += 2;
		    }
		
		    public void Reset()
		    {
			       current = 0;
		    }
	  }
	  
	  class Program
	  {
			  public static void ProcessSeries (ISeries series)
        {
            for ( int i=0; i < 10; i++)
            {
                Console.Write($"{series.Current} , ");
                series.GetNext();
            }
            Console.WriteLine("");
            series.Reset();
        }
        
        static void MainV1(string[] args)
        {
		        SeriesByTwo series01 = new SeriesByTwo();

            ProcessSeries(series01);

            ISeries series02; ///Valid ,
            //Refrence to any Class\Struct Implementing ISeries Interface
            //series01 = new ISeries(); ///Not Valid
            series02 = new FibSeries();
            ProcessSeries(series02);
        }
	  }  
}
```