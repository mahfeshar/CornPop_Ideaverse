---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-11
---
- It's a multi value in one variable with the ==same data type==
- هي عبارة عن [[Cs Value and Reference Types#Reference Types|Reference Types]] يعني لما بعمل array جديدة يبقا بعمل object from array class
  Non-primitive -> Reference -> Heap
## Array Properties
1. Fixed Type
2. Fixed Size ([[Array#Static Arrays|Static Array]])

## Array Types
1. Single Dimensional Array
2. Multi Dimensional Array
3. Jadgged Array
## Create an Array
```cs
int[] Arr;
//Declaration for refrence of int Array 
//Zero Bytes have been allocated in Heap

Arr = new int[5]; // allocated in heap now : To use later
// Will give here initial value and in this case will be 0 (default)
// String -> NULL

int[] Arr = new int[5] { 3, 4, 5, 6, 7 };

int[] Arr = new int[] { 3, 4, 5, 6, 7 };

int[] Arr =  { 3, 4, 5, 6, 7 };
```
## Access the elements and change it
طبعا بتوصل للعناصر من خلال ال index بتاعها
```cs
string[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
Console.WriteLine(cars[0]);
// Outputs Volvo
```
وبرضو بنفس الطريقة أقدر أغير قيمة جواه
```csharp
string[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
cars[0] = "Opel";
Console.WriteLine(cars[0]);
// Now outputs Opel instead of Volvo
```

## Loop through Array
ممكن أستخدم أي طريقة هنا [[Cs Control Flow Statements#Iteration Statements|Iteration Statements]] وخصوصا ال foreach

```cs
int[] arr = new int[3]; // 0 0 0
for(int i = 0; i < arr.Length; i++)
{
	arr[i] = int.Parse(Console.ReadLine());
}

// We can't use foreach in this case
```

## Array as reference

```cs
int[] Arr01 = { 1, 7, 5, 3, 8, 6, 4, 2 };
int[] Arr02 = { 7, 8, 9 };

Console.WriteLine($"Arr01 {Arr01.GetHashCode()}");
Console.WriteLine($"Arr02 {Arr02.GetHashCode()}");

//Arr02 = Arr01;
///Same Object , Two References 
Console.WriteLine("Arr02 = Arr01");

Arr02 = (int[])Arr01.Clone();
///int[] = (int[])object ;
///Derived = Base : Not Valid must use Explicit Casting
/// ref To Base = Derived : Valid
///Arr02 new Object with new(diff) identity but same state as Arr01
Console.WriteLine("After Clone");
Console.WriteLine($"Arr01 {Arr01.GetHashCode()}");
Console.WriteLine($"Arr02 {Arr02.GetHashCode()}");


for (int i = 0; i < Arr02.Length; i++)
    Console.Write($"{Arr02[i]} , ");
Console.WriteLine("");
/*
Arr01 27252167
Arr02 59941933
Arr02 = Arr01
After Clone
Arr01 27252167
Arr02 2606490
1 , 7 , 5 , 3 , 8 , 6 , 4 , 2 ,
*/
```
- اللي حصل ان كل array متخزنة في الأول في ال heap عادي بس في اماكن مختلفة، ولو خليت الأول بيساوي التاني فدا معناه اني بس خليت الأول يشاور على التاني والداتا اللي كانت في الأول بقت unreachable زي ما قولنا قبل كدا 
- انما لو عايز أخزن الداتا في الarray التانية فكدا لازم أخد نسخة من المحتوى بتاعه الأول وأحطه في التاني
- بس في الحالة دي مش هينفع لأن `clone` بترجع من النوع `object` ودا يعتبر الشامل 
  ومن قواعد ال OOP ان ال base = derived انما ال derived != base فكدا لازم أعمل [[Cs Type Casting#Explicit Casting|Explicit Casting]]
* شرح قاعدة ال OPP: مش كل class هو car ولكن كل car عبارة عن class
## Array Methods
![[Pasted image 20240715105514.png]]
### Array Length
```csharp
string[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
Console.WriteLine(cars.Length);
// Outputs 4

int[] Arr01 = { 1, 7, 5, 3, 8, 6, 4, 2 };
Array.Sort(Arr01);
//rank: نوعها ايه
Console.WriteLine($"Size {Arr01.Length} , Number of Dimensions {Arr01.Rank}");
```
### Array copy
`Array.Copy` method is used to copy elements from one array to another. 
This method provides a way to duplicate the contents of an array into another array, **either partially or fully**, depending on the parameters used.
#### Basic Syntax
```cs
public static void Copy(Array sourceArray, Array destinationArray, int length);
```

#### Parameters
- **sourceArray**: The array that contains the data to be copied.
- **destinationArray**: The array that will receive the copied data.
- **length**: The number of elements to copy.

#### Overloads

There are several overloads of the `Array.Copy` method that allow for more flexibility:

1. **Basic Copy**
    
    ```cs
    Array.Copy(sourceArray, destinationArray, length);
	```

2. **Specifying Indices**
    
    ```cs
    public static void Copy(Array sourceArray, int sourceIndex, Array destinationArray, int destinationIndex, int length);
`````
    
    Copies `length` elements from `sourceArray` starting at `sourceIndex` to `destinationArray` starting at `destinationIndex`.


#### Example Usage

Here's an example demonstrating how to use `Array.Copy`:
```cs
using System;

class Program
{
    static void Main()
    {
        int[] sourceArray = { 1, 2, 3, 4, 5 };
        int[] destinationArray = new int[5];

        // Copying the entire array
        Array.Copy(sourceArray, destinationArray, sourceArray.Length);

        // Displaying the contents of the destination array
        foreach (int item in destinationArray)
        {
            Console.WriteLine(item);
        }

        // Copying a part of the array
        int[] partialDestinationArray = new int[3];
        Array.Copy(sourceArray, 1, partialDestinationArray, 0, 3);

        // Displaying the contents of the partial destination array
        foreach (int item in partialDestinationArray)
        {
            Console.WriteLine(item);
        }
    }
}
```
#### Important Considerations

- **Type Compatibility**: Both the source and destination arrays must be of compatible types, otherwise a runtime exception will occur.
- **Bounds Checking**: Ensure that the destination array is large enough to hold the copied elements to avoid an `ArgumentOutOfRangeException`.
- **Shallow Copy**: `Array.Copy` performs a shallow copy, meaning if the array contains reference types, only the references are copied, not the actual objects.
  [[Cs Shallow and Deep copy#Shallow Copy|Shallow Copy]]

Using `Array.Copy` is a straightforward way to duplicate or move data between arrays in C#, providing flexibility through its various overloads and ease of use.

We talked more about [[Cs Shallow and deep copy]]


### Array Clone
دي بستخدمها عشان أعمل [[Cs Shallow and deep copy#Deep Copy|Deep Copy]]
### Sort an Array
هنستخدم ال method اللي اسمها `Sort()` وبترتب تصاعدي وال method  دي موجودة جوا class ال `Array`
```csharp
// Sort a string
string[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
Array.Sort(cars);
foreach (string i in cars)
{
  Console.WriteLine(i);
}
 
```

```csharp
// Sort an int
int[] myNumbers = {5, 1, 8, 9};
Array.Sort(myNumbers);
foreach (int i in myNumbers)
{
  Console.WriteLine(i);
}
```

- We can reverse an array with `Reverse` function.
```cs
int[] arr = {10, 20, 30};
Array.Reverse(arr); // 30 , 20 , 10
```
- If I want to sort desc: So we will use `Sort` by default asc, and then `Reverse`
```cs
int[] arr = {20, 100, 50, 10};
Array.Sort(arr); // 10, 20, 50, 100
Array.Reverse(arr); // 100, 50, 20, 10
```
### System.Linq Namespace
بتخليني أعمل فيلتر على الداتا وأنا بشتغل على ال DB مثلًا
Other useful array methods, such as `Min`, `Max`, and `Sum`, can be found in the `System.Linq` namespace
```csharp
using System;
using System.Linq;

namespace MyApplication
{
  class Program
  {
    static void Main(string[] args)
    {
      int[] myNumbers = {5, 1, 8, 9};
      Console.WriteLine(myNumbers.Max());  
      // returns the largest value
      Console.WriteLine(myNumbers.Min());  
      // returns the smallest value
      Console.WriteLine(myNumbers.Sum());  
      // returns the sum of elements
    }
  }
}
```
## Multidimensional Arrays

![[Pasted image 20240715105327.png]]
A multidimensional array is basically an array of arrays.
```csharp
dataType[,] arrayName = new dataType[dimension1, dimension2];
// `dimension1`: The size of the first dimension. (X)
// `dimension2`: The size of the second dimension. (Y)

// OR
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };
```

> **Good to know:** The single comma `[,]` specifies that the array is two-dimensional. 
> A three-dimensional array would have two commas: `int[,,]`.

#### example
```cs
using System;

class Program
{
    static void Main()
    {
        // Create a 3x3 two-dimensional array
        int[,] matrix = new int[3, 3];

        // Initialize the array
        matrix[0, 0] = 1;
        matrix[0, 1] = 2;
        matrix[0, 2] = 3;
        matrix[1, 0] = 4;
        matrix[1, 1] = 5;
        matrix[1, 2] = 6;
        matrix[2, 0] = 7;
        matrix[2, 1] = 8;
        matrix[2, 2] = 9;

        // Display the array elements
        for (int i = 0; i < matrix.GetLength(0); i++)
        {
            for (int j = 0; j < matrix.GetLength(1); j++)
            {
                Console.Write(matrix[i, j] + "\t");
            }
            Console.WriteLine();
        }
    }
}


using System;

class Program
{
    static void Main()
    {
        // Create and initialize a 2x3 two-dimensional array
        int[,] matrix = new int[,]
        {
            { 1, 2, 3 },
            { 4, 5, 6 }
        };

        // Display the array elements
        for (int i = 0; i < matrix.GetLength(0); i++)
        {
            for (int j = 0; j < matrix.GetLength(1); j++)
            {
                Console.Write(matrix[i, j] + "\t");
            }
            Console.WriteLine();
        }
    }
}

```
### Access and change
```csharp
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };
Console.WriteLine(numbers[0, 2]);  // Outputs 2

numbers[0, 0] = 5;  // Change value to 5
Console.WriteLine(numbers[0, 0]); // Outputs 5 instead of 1
```
### Loop through 2D array

```csharp
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };

foreach (int i in numbers)
{
  Console.WriteLine(i);
}
```

### Length
هناك كنا بنستخدم Length انما هنا هنستخدم `GetLength()`
```csharp
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };

for (int i = 0; i < numbers.GetLength(0); i++) 
{ 
  for (int j = 0; j < numbers.GetLength(1); j++) 
  { 
    Console.WriteLine(numbers[i, j]); 
  } 
}
```

## Jagged Array
[C# Jagged Array](https://www.programiz.com/csharp-programming/jagged-array)