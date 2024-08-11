---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-08-03
---
### Console Application

- A console application is a program that runs in the ==command line interface (CLI)== or terminal. 
- It's primarily used for simple tasks, debugging, utilities, and learning purposes. 
- Console applications have a main entry point, the `Main` method, where the program execution begins.

#### How to Create and Use a Console Application

1. **Creating a Console Application:**
   - Open Visual Studio.
   - Select `Create a new project`.
   - Choose `Console App` and click `Next`.
   - Configure your project (name, location, etc.) and click `Create`.

2. **Basic Structure:**
   ```csharp
   using System;

   namespace ConsoleApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello, World!");
           }
       }
   }
   ```

3. **Running the Console Application:**
   - Press `Ctrl + F5` to run the application.
   - The output "Hello, World!" will be displayed in the console.

### Library

- A library in C# is a collection of [[CSharp Class|classes]], methods, and other resources that can be used by other applications. 
- Libraries do not have a `Main` method; instead, they are referenced and used by other applications, including console applications, web applications, and other libraries.

#### Types of Libraries
- **Class Library:** The most common type, containing reusable classes and methods.
- **.NET Standard Library:** A library compatible across different .NET implementations (.NET Core, .NET Framework, Xamarin, etc.).

#### How to Create and Use a Library

1. **Creating a Class Library:**
   - Open Visual Studio.
   - Select `Create a new project`.
   - Choose `Class Library` and click `Next`.
   - Configure your project (name, location, etc.) and click `Create`.

2. **Basic Structure:**
   ```csharp
   using System;

   namespace MyLibrary
   {
       public class Greeter
       {
           public string Greet(string name)
           {
               return $"Hello, {name}!";
           }
       }
   }
   ```

3. **Building the Library:**
   - Build the project (Build > Build Solution or `Ctrl + Shift + B`).
   - The compiled ==DLL file== will be located in the `bin/Debug` or `bin/Release` folder.

4. **Using the Library in a Console Application:**
   - Create a new Console Application project or open an existing one.
   - Right-click on the project in Solution Explorer and select `Add > Project Reference`.
   - Check the box next to your library project and click `OK`.

5. **Example Usage:**
   ```csharp
   using System;
   using MyLibrary; // Reference to the library

   namespace ConsoleApp
   {
       class Program
       {
           static void Main(string[] args)
           {
               Greeter greeter = new Greeter();
               string message = greeter.Greet("Alice");
               Console.WriteLine(message);
           }
       }
   }
   ```

### Summary

- **Console Application:** Ideal for standalone programs with a `Main` entry point, often used for utilities, scripts, and learning purposes.
- **Library:** Contains reusable code (classes, methods) without a `Main` method, meant to be referenced and used by other applications.

Using libraries allows you to modularize your code, making it reusable and easier to maintain. Console applications are great for straightforward tasks and can leverage libraries to extend their functionality.